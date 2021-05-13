# Troubleshoot high IOPS usage on an ApsaraDB for MongoDB instance

The input/output operations per second \(IOPS\) usage on an ApsaraDB for MongoDB instance is a key metric. If the IOPS usage reaches or is close to 100% on an instance, the instance may respond slowly and even become unavailable. This topic describes how to view IOPS usage and troubleshoot high IOPS usage on an ApsaraDB for MongoDB instance.

## Background information

Typically, to prevent hosts from competing for I/O resources, most cloud database providers use techniques such as control groups \(cgroups\) to isolate I/O resources and limit IOPS. The upper limit of IOPS on instances varies based on instance specifications.

## View IOPS usage

-   View IOPS usage in monitoring charts
    -   On the **Basic Information** page of an instance in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), view the upper limit of IOPS on the instance. For more information about the upper limit of IOPS on instances of different instance specifications, see [t6649.dita\#concept\_wrp\_kg4\_tdb](/intl.en-US/Product Introduction/Instance types.md).
    -   On the **Monitoring Info** page of an instance in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), view the upper limit of IOPS on the instance. In most cases, the data files and the logs of an ApsaraDB for MongoDB instance are stored in the same disk. The IOPS usage of data files is the same as that of log files.
-   View IOPS usage by running commands

    In the monitoring charts, ApsaraDB for MongoDB displays only IOPS-related information such as the upper limit of IOPS. For I/O issues, you must also focus on I/O throughput and latency. To view other I/O metrics, run the `db.serverStatus().systemInfo` command.

    **Note:**

    -   The values of metrics are accumulated after MongoDB is started.
    -   To view more performance metrics of MongoDB, run the `db.serverStatus().systemInfo` command.

## Common causes of I/O issues

I/O issues may be caused by the following common reasons:

-   The memory is insufficient. I/O issues are closely related to the cache size in memory. Larger cache size allows larger volumes of hot cache data. The fewer disk I/O resources required by the system, the lower the probability of I/O bottlenecks. Smaller cache size allows less hot cache data. The system frequently flushes dirty pages to disks, which results in a higher probability of I/O bottlenecks.
-   Parameters and configurations related to disk I/O experience issues. For example, journal logs and runtime logs frequently refresh, the WriteConcern parameter is improperly configured, or the moveChunk operation on a sharded cluster instance is invalid.

    For more information about journal files, visit [https://docs.mongodb.com/manual/core/journaling/](https://docs.mongodb.com/manual/core/journaling/).

    For more information about WriteConcern, visit [https://docs.mongodb.com/manual/reference/write-concern/](https://docs.mongodb.com/manual/reference/write-concern/).


## Optimization strategies for I/O issues

We recommend that you select appropriate instance specifications for ApsaraDB for MongoDB instances and optimize indexing and writing policies of some application systems.

-   Configure appropriate instance specifications for ApsaraDB for MongoDB instances

    The ratio of hot data size to cache size is difficult to predict. In most cases, the maximum CPU utilization and IOPS usage per day are separately within 50%.

-   Optimize indexing

    If queries cause full table scans or use improper indexes, high IOPS usage occurs. For example, large numbers of I/O resources are consumed to export full table data. A large number of indexes generate large volumes of data, which results in the reduction of hot data in the WiredTiger cache. Business data writes require more than one I/O operation to update indexes, which affects I/O performance. In this case, we recommend that you create appropriate indexes. For more information, visit [https://docs.mongodb.com/manual/indexes/](https://docs.mongodb.com/manual/indexes/).

-   Optimize business architecture and O&M

    Take the following optimization measures to prevent disk I/O from becoming a bottleneck of the business architecture:

    -   Control the number of concurrent write/read threads

        MongoDB is a multi-threaded application. Fast concurrent writes speed and complex queries may cause IOPS bottlenecks and even lead to continuous latency on secondary nodes. If I/O bottlenecks are caused by the large volumes of written data, we recommend that you upgrade your instance to an ApsaraDB for MongoDB sharded cluster instance. This way, data is horizontally split by shards to linearly scale out the write performance of the instance.

    -   Write data during off-peak hours

        Regular writes or batch data persistence may cause peak IOPS. In this case, if the current instance configurations do not meet the requirements of peak writes, we recommend that you upgrade the configurations to smoothly write business data. For example, add a random timestamp for each batch write operation.

    -   Perform O&M operations during off-peak hours

        O&M operations that heavily affect performance may cause peak IOPS. We recommend that you perform O&M operations during off-peak hours. Peak IOPS may be caused when you batch write, update, or delete data, add indexes, perform compact operations on collections, or batch export data.


