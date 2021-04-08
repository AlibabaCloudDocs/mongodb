# MongoDB实例内存使用率高问题

MongoDB实例的内存使用率是一个非常重要的监控指标。 如果MongoDB实例的内存使用率过高，会导致MongoDB实例内存溢出。本文介绍查看MongoDB实例内存使用率的方法，以及导致内存使用率高的原因和优化策略。

## 背景信息

MongoDB进程启动后，不仅会加载二进制文件和依赖的各种系统库文件到内存，而且负责内存的分配和释放工作，例如客户端的连接管理、请求处理和存储引擎等。默认情况下，MongoDB的内存分配器是Google tcmalloc，内存主要被“Wiredtiger存储引擎”和“客户端连接及请求处理”占用。

## 查看方法

分片集群架构下，各个分片（Shard）的内存使用与副本集架构保持一致，Config Server用于存储配置元数据，Mongos路由节点的内存使用和聚合结果集、连接数大小、元数据大小相关。

副本集架构下，提供多种查看内存使用的方法：

-   监控图分析

    MongoDB副本集由多种角色组成，一个角色可能对应一个或多个物理节点。MongoDB提供主节点（Primary）、从节点（Secondary）和只读节点。

    在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**监控信息**页面，可以查看MongoDB的内存使用率。

    ![分析监控_查看节点内存使用率](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4878666161/p232880.png)

    ![监控信息_WiredTiger引擎](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4878666161/p232904.png)

-   命令行查看

    在MongoDB Shell中使用`db.serverStatus().mem`命令查看和分析内存占用情况，返回示例如下：

    ```
    { "bits" : 64, "resident" : 13116, "virtual" : 20706, "supported" : true }
    //resident 表示该mongod物理节点占⽤的物理内存大小，单位为MB。
    //virtual 表示该mongod物理节点占⽤的虚拟内存大小，单位为MB。
    ```

    由于MongoDB serverStatus中包含了关于WiredTiger引擎和tcmalloc的内存使用详情，所以可以通过`db.serverStatus().wiredTiger.cache`和`db.serverStatus().wiredTiger.tcmalloc`查看。详情请参见[serverStatus](https://docs.mongodb.com/manual/reference/command/serverStatus/)。


## 常见原因

MongoDB内存使用率高的原因如下：

-   引擎内存

    tcmalloc为MongoDB的内存分配器。由于WiredTiger引擎占用的Cache是最大的一部分，所以引擎内存的最大使用内存由配置参数cachesize决定。考虑到兼容性和安全性，阿里云数据库MongoDB为cachesize设置的大小约为实际申请的实例规格大小的60%，具体规格请参见[实例规格参考](#table_737_6ka_9te)。

    如果数据量超过cachesize配置大小的95%，说明系统性能已经处于较为危险状态。WiredTiger在内存使用接近阈值时开始做淘汰工作，避免发生阻塞用户请求的情况，该过程被成为“eviction”。具体规则请参见[eviction参数说明](#table_o68_is2_g21)。

    您可以使用以下方法查看引擎内存的使用情况：

    -   在MongoDB Shell中通过`db.serverStatus().wiredTiger.cache`查看。返回信息中`bytes currently in the cache`后的值为内存大小。返回信息示例如下：

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

    -   在[DAS控制台](https://hdm.console.aliyun.com/?spm=a2c4g.11186623.2.9.1d303f70oyAoxP)的**性能趋势**页面实时查看当前wiredTiger引擎的cache dirty比例。具体请参见[性能趋势]()。
    -   通过MongoDB自带的mongostat工具查看当前wiredTiger引擎的cache dirty比例，请参见[https://docs.mongodb.com/v4.2/reference/program/mongostat/](https://docs.mongodb.com/v4.2/reference/program/mongostat/)。
-   连接和请求占⽤的内存

    如果实例的连接数很⼤，可能会消耗⼀部分的内存，原因如下：

    -   每个连接，后端都有对应处理这个连接上的请求的线程。每个线程最多可以开销1MB的线程栈，通常情况下在几十KB~几百KB。
    -   每个TCP连接在内核层⾯有读缓冲区和写缓冲区，由TCP内核参数tcp\_rmem和tcp\_wmem等确定，这块的内存使⽤⽤户⽆需关⼼。但并发连接越多，默认套接字缓存越⼤，则TCP占⽤内存越⼤。
    -   每接收到⼀个请求，会有个请求上下⽂，整个过程中可能分配很多临时缓冲区，⽐如请求包、应答包、排序的临时缓冲区等，这些在请求结束都会释放，但这个释放只是说归还给内存分配器 tcmalloc，tcmalloc优先会还到⾃⼰的cache⾥；然后逐步再归还给操作系统。 很多情况下，内存使⽤率⾼的原因是tcmalloc未及时归还内存⾄操作系统，这⼀块最⼤可能达到几十GB。关于tcmalloc未归还OS的内存大小，可以通过命令`db.serverStatus().tcmalloc`查看。其中tcmalloc cache⼤⼩=pageheap\_free\_bytes + total\_free\_byte。返回信息示例如下：

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

        关于更多mongodb tcmalloc的更多内容，请参见[https://mongoing.com/archives/34751](https://mongoing.com/archives/34751)。

-   元数据信息占⽤的内存

    MongoDB的数据库、集合、索引等内存元数据等，如果集合和索引数量很多，这⼀块占用的内存也不容忽视。尤其在MongoDB 4.0以前的版本，全量逻辑备份期间可能打开⾮常多的⽂件句柄并且未能及时归还OS导致内存快速上涨，或者低版本的MongoDB在⼤量删除集合后可能未能删除文件句柄导致内存泄漏。

-   创建索引过程中的内存消耗

    正常的业务数据写⼊情况下，Secondary节点会维持⼀个最⼤约256M的buffer⽤于数据回放。在创建索引方面，当Primary节点创建索引完成后，Secondary节点回放过程中可能消耗更多的内存。在 MongoDB 4.2以前，在Primary节点上通过⾮background的⽅式创建索引，后端回放创建索引是串行的，最多可能消耗500M内存；而MongoDB 4.2以后默认废弃了background选项，允许Secondary节点并行回放创建索引，那就会消耗更多的内存，多个索引同时创建时可能导致实例内存溢出。更多关于创建索引期间可能造成的内存消耗，请参见[https://docs.mongodb.com/manual/core/index-creation/\#index-build-impact-on-database-performance](https://docs.mongodb.com/manual/core/index-creation/#index-build-impact-on-database-performance)和[https://docs.mongodb.com/manual/core/index-creation/\#index-build-process](https://docs.mongodb.com/manual/core/index-creation/#index-build-process)。

-   PlanCache内存占⽤

    在某些场景下，例如⼀个请求可能存在的执⾏计划⾮常多，这时plancache可能会消耗⽐较多的内存，在⾼版本MongoDB中可以通过命令`mgset-xxx:PRIMARY> db.serverStatus().metrics.query.planCacheTotalSizeEstimateBytes NumberLong(750695)`查看PlanCache占⽤的内存大小。更多内容请参见[https://jira.mongodb.org/browse/SERVER-48400](https://jira.mongodb.org/browse/SERVER-48400)。


## 解决策略

内存优化并不是尽可能的减少内存使用，而是在保证系统性能正常的前提下，内存足够使用且稳定，在机器资源和性能中达到⼀个最佳的折衷。阿⾥云MongoDB帮助⽤户指定了CacheSize的大小，该值不支持修改。解决内存使用的策略如下：

-   控制并发连接数。根据性能测试结果，数据库中能够创建100个长连接，默认MongoDB Driver可以和后端建⽴100个连接池。当存在很多客户端时，就需要降低每个客户端的连接池大小，⼀般建议与整个数据库建⽴的长连接控制在1000以内，连接太多会导致内存和多线程上下文的开销增加，影响请求处理延时。
-   降低单次请求的内存开销，例如通过创建索引减少集合的扫描、内存排序等。
-   在连接数合适的情况下内存占⽤持续增⾼，建议升级内存配置，避免可能存在内存溢出和大量清除缓存而导致系统性能急剧下滑。
-   如果您在使⽤阿⾥云MongoDB过程中遇到更多可能存在内存泄漏的场景，可以联系阿里云技术⽀持处理。

## 参考

|实例规格|规格大小|实际大小|WiredTiger的cachesize大小|
|----|----|----|----------------------|
|dds.mongo.small|1024GB|2048GB|1GB|
|dds.mongo.mid|2048GB|4096GB|1GB|
|dds.mongo.standard|4096GB|7168GB|2GB|
|dds.mongo.large|8192GB|12288GB|5GB|
|dds.mongo.xlarge|16384GB|24576GB|10GB|
|dds.mongo.2xlarge|32768GB|49152GB|20GB|
|dds.mongo.4xlarge|65536GB|98304GB|40GB|
|dds.mongo.monopolize|450560GB|450560GB|264GB|
|mongo.x8.medium|16384GB|16384GB|10GB|
|mongo.x8.large|32768GB|32768GB|20GB|
|mongo.x8.xlarge|65536GB|65536GB|40GB|
|mongo.x8.2xlarge|131072GB|131072GB|77GB|
|mongo.x8.4xlarge|262144GB|262144GB|154GB|
|dds.sn4.8xlarge.3|131072GB|131072GB|64GB|

|参数|默认值|含义|
|--|---|--|
|eviction\_target|80|当cache used超过eviction\_target，后台evict线程开始淘汰CLEAN PAGE。|
|eviction\_trigger|95|当cache used超过eviction\_trigger，⽤户线程也开始淘汰CLEAN PAGE。|
|eviction\_dirty\_target|5|当cache dirty超过eviction\_dirty\_target，后台 evict线程开始淘汰DIRTY PAGE。|
|eviction\_dirty\_trigger|20|当cache dirty超过eviction\_dirty\_trigger, ⽤户线程也开始淘汰DIRTY PAGE。|

