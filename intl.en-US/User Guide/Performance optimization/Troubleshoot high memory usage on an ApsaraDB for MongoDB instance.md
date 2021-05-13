# Troubleshoot high memory usage on an ApsaraDB for MongoDB instance

Memory usage is a key metric to monitor an ApsaraDB for MongoDB instance. High memory usage on an instance may result in an out-of-memory \(OOM\) error. This topic describes how to view memory usage details and troubleshoot high memory usage on an instance.

## Background information

MongoDB processes load binary files and dependent system library files to the memory. MongoDB processes also allocate and release memory, including managing client connections and storage engines and processing requests. By default, MongoDB uses TCMalloc from Google as a memory allocator. Most of the memory is consumed by the WiredTiger storage engine, client connections, and request processing.

## View memory usage

For a sharded cluster instance, the memory usage on each shard node is the same as that on a replica set instance. The Configserver node stores only configuration metadata. The memory usage on mongos nodes is affected by aggregated result sets, the number of connections, and the size of metadata.

For a replica set instance, you can use the following methods to view the memory usage.

-   View memory usage in monitoring charts

    A replica set instance consists of multiple node roles. Each node role can correspond to one or more physical nodes. ApsaraDB for MongoDB allows you to use primary, secondary, and read-only nodes.

    On the **Monitoring Info** page of an instance in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), view the memory usage on the corresponding node in monitoring charts.

-   View memory usage by running commands

    To view and analyze the memory usage on an instance, run the `db.serverStatus().mem` command in the mongo shell. A response similar to the following one is returned:

    ```
    { "bits" : 64, "resident" : 13116, "virtual" : 20706, "supported" : true }
    //resident indicates the physical memory that is consumed by the mongod process. Unit: MB. 
    //virtual indicates the virtual memory that is consumed by the mongod process. Unit: MB. 
    ```

    MongoDB serverStatus output contains the memory consumed by the WiredTiger storage engine and TCMalloc. To view memory usage details, run the `db.serverStatus().wiredTiger.cache` and `db.serverStatus().wiredTiger.tcmalloc` commands. For more information, see [serverStatus](https://docs.mongodb.com/manual/reference/command/serverStatus/).


## Common causes

The following list describes common causes of high memory usage:

-   High memory usage of the engine

    MongoDB uses TCMalloc as a memory allocator. The WiredTiger storage engine consumes the largest portion of the cache. The maximum memory size of the storage engine is determined by the cachesize parameter. For compatibility and security purposes, ApsaraDB for MongoDB sets the cachesize parameter to 60% of the allocated size. For more information, see [Instance specifications](#table_737_6ka_9te).

    If the size of cached data exceeds 95% of the configured cache size, the system has a high risk of performance degradation. WiredTiger performs evictions when the memory usage approaches the threshold to prevent user requests from being blocked. For more information, see [Table 2](#table_qsa_7cm_bbt).

    You can use the following methods to view the memory usage of the engine:

    -   Run the `db.serverStatus().wiredTiger.cache` command in the mongo shell. The `bytes currently in the cache` value is the memory size. Sample output:

        ```
        {
           ......
           "bytes belonging to page images in the cache":6511653424,
           "bytes belonging to the cache overflow table in the cache":65289,
           "bytes currently in the cache":8563140208,
           "bytes dirty in the cache cumulative":NumberLong("369249096605399"),
           ......
        }
        ```

    -   On the **Performance Trend** page of an instance in the [DAS console](https://hdm.console.aliyun.com/?spm=a2c4g.11186623.2.9.1d303f70oyAoxP), view the percentage of dirty data in the WiredTiger cache. For more information, see [Performance trends]().
    -   Use the mongostat utility that comes with MongoDB to view the current percentage of dirty data in the WiredTiger cache. For more information, visit [https://docs.mongodb.com/v4.2/reference/program/mongostat/](https://docs.mongodb.com/v4.2/reference/program/mongostat/).
-   High memory usage of connections and requests

    If a large number of connections are connected to the instance, the memory may be consumed due to the following reasons:

    -   Each connection has a corresponding thread to process the request in the background. Each thread can use up to 1 MB of stack space. In most cases, the overhead is dozens to hundreds of KB.
    -   Each TCP connection has read and write buffers at the kernel layer. The buffer size is determined by TCP kernel parameters such as tcp\_rmem and tcp\_wmem. You do not need to specify the buffer size. However, more concurrent connections consume larger amounts of socket cache space and results in higher memory usage of TCP.
    -   Each request has a unique context. Multiple temporary buffers may be allocated for request packets, response packets, and ordering. The temporary buffers are gradually released at the end of each request. The buffers are first released to the TCMalloc cache and then gradually released to the operating system. In many cases, memory usage is high because TCMalloc fails to promptly release the memory that requests consume. Requests may consume up to dozens of GB of memory before the memory is released to the operating system. To query the size of memory that TCMalloc has not released to the operating system, run the `db.serverStatus().tcmalloc` command. The TCMalloc cache size is the sum of the pageheap\_free\_bytes and total\_free\_byte values. Sample output:

        ```
        {
           "generic":{
                   "current_allocated_bytes":NumberLong("9641570544"),
                   "heap_size":NumberLong("19458379776")
           },
           "tomalloc":{
                   "pageheap_free_bytes":NumberLong("3048677376"),
                   "pageheap_unmapped_bytes":NumberLong("544994184"),
                   "current_total_thread_cache_bytes":95717224,
                   "total_free_byte":NumberLong(1318185960),
        ......
           }
        }
        ```

        For more information about TCMalloc, visit [https://mongoing.com/archives/34751](https://mongoing.com/archives/34751).

-   High memory usage of metadata

    Metadata includes memory usage of databases, collections, and indexes. You must pay attention to the memory that is consumed by large numbers of collections and indexes. Especially in versions earlier than MongoDB 4.0, full logical backups may open large numbers of file handles. These file handles may not be promptly returned back to the operating system and result in rapid memory usage growth. The file handles may not be deleted after large numbers of collections are deleted and result in memory leaks.

-   High memory usage of index creation

    In normal data writes, secondary nodes maintain a buffer of about 256 MB for data replay. After the primary node creates indexes, secondary nodes may consume more memory for data replay. In versions earlier than MongoDB 4.2, indexes are created in the background on the primary node. Serial replay for index creation may consume a maximum of 500 MB memory. In MongoDB 4.2 and later, indexes cannot be created in the background and secondary nodes can perform parallel replay for index creation. This requires more memory because instance OOM errors may occur when multiple indexes are created at a time. For more information, visit [https://docs.mongodb.com/manual/core/index-creation/\#index-build-impact-on-database-performance](https://docs.mongodb.com/manual/core/index-creation/#index-build-impact-on-database-performance) and [https://docs.mongodb.com/manual/core/index-creation/\#index-build-process](https://docs.mongodb.com/manual/core/index-creation/#index-build-process).

-   High memory usage of PlanCache

    If a request has a large number of execution plans, the PlanCache methods may consume large amounts of memory. To view the memory usage of PlanCache, run the `mgset-xxx:PRIMARY> db.serverStatus().metrics.query.planCacheTotalSizeEstimateBytes NumberLong(750695)` command. For more information, visit [https://jira.mongodb.org/browse/SERVER-48400](https://jira.mongodb.org/browse/SERVER-48400).


## Solutions

The goal of memory optimization is not to minimize memory usage. Instead, memory optimization seeks a balance between resource consumption and performance. Ideally, the memory remains sufficient and stable and system performance is not affected. You cannot change the cachesize value that ApsaraDB for MongoDB configures. We recommend that you use the following methods to optimize memory usage:

-   Control the number of concurrent connections. 100 persistent connections can be created in a database based on the results of performance tests. By default, a MongoDB driver can establish 100 connection pools with the backend. If a large number of clients exist, you must reduce the size of the connection pool for each client. We recommend that you establish no more than 1,000 persistent connections in a database. Otherwise, overheads in the memory and multi-thread context may increase and result in processing latency for requests.
-   Reduce the memory overhead of a single request. For example, you can create indexes to reduce the number of collection scans and perform memory ordering.
-   If the number of connections is appropriate but the memory usage continues to increase, we recommend that you upgrade the memory configurations. Otherwise, system performance may sharply decline due to OOM errors and extensive cache clearing.
-   In scenarios where memory leaks may occur, contact Alibaba Cloud technical support.

## References

|Instance type|Available memory size|Allocated memory size|cachesize value of WiredTiger|
|-------------|---------------------|---------------------|-----------------------------|
|dds.mongo.small|1024 MB|2048 MB|1 GB|
|dds.mongo.mid|2048 MB|4096 MB|1 GB|
|dds.mongo.standard|4096 MB|7168 MB|2 GB|
|dds.mongo.large|8192 MB|12288 MB|5 GB|
|dds.mongo.xlarge|16384 MB|24576 MB|10 GB|
|dds.mongo.2xlarge|32768 MB|49152 MB|20 GB|
|dds.mongo.4xlarge|65536 MB|98304 MB|40 GB|
|dds.mongo.monopolize|450560 MB|450560 MB|264 GB|
|mongo.x8.medium|16384 MB|16384 MB|10 GB|
|mongo.x8.large|32768 MB|32768 MB|20 GB|
|mongo.x8.xlarge|65536 MB|65536 MB|40 GB|
|mongo.x8.2xlarge|131072 MB|131072 MB|77 GB|
|mongo.x8.4xlarge|262144 MB|262144 MB|154 GB|
|dds.sn4.8xlarge.3|131072 MB|131072 MB|64 GB|

|Parameter|Default value|Description|
|---------|-------------|-----------|
|eviction\_target|80|When the used cache size is larger than the eviction\_target value, eviction threads evict clean pages in the background.|
|eviction\_trigger|95|When the used cache size is larger than the eviction\_trigger value, user threads evict clean pages in the background.|
|eviction\_dirty\_target|5|When the size of dirty data in cache is larger than the eviction\_dirty\_target value, eviction threads evict dirty pages in the background.|
|eviction\_dirty\_trigger|20|When the size of dirty data in cache is larger than the eviction\_dirty\_trigger value, user threads evict dirty pages in the background.|

