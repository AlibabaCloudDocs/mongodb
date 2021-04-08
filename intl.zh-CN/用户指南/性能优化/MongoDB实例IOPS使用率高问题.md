# MongoDB实例IOPS使用率高问题

MongoDB实例的IOPS使⽤率是⼀个⾮常重要的监控指标。如果MongoDB实例的IOPS使⽤率达到或接近100%，会导致业务响应缓慢，甚⾄业务不可⽤。本文介绍查看MongoDB实例IOPS使用率的方法，以及导致IOPS使用率高的原因和优化策略。

## 背景信息

⼀般云数据库厂商为了避免宿主机出现I/O争抢，会使⽤CGroup（ Control Groups ）等技术进⾏实例间的I/O隔离和IOPS（Input/Output Operations Per Second）限制，即不同规格的实例配置对应不同的IOPS使⽤上限。

## 查看IOPS使用率

-   监控图查看
    -   在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**基本信息**页面，确认该实例的最⼤IOPS上限。不同实例规格对应的IOPS使⽤上限请参见：[实例规格表](https://help.aliyun.com/document_detail/57141.html)。

        ![通过基本信息查看IOPS上限](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3237666161/p235810.png)

    -   在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**监控信息**页面，确认该实例的最⼤IOPS上限。⼤部分情况下阿⾥云数据库MongoDB的data⽬录和log⽬录使⽤同⼀块盘，所以IOPS使⽤量=data\_iops=log\_iops。

        ![通过监控信息查看IOPS使用量](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3237666161/p235811.png)

-   命令行查看

    在监控图展示上，目前阿里云MongoDB仅限制IOPS，也仅展示IOPS的相关信息。在实际的I/O问题中，还需要关注I/O的吞吐量和延迟情况，通过命令`db.serverStatus().systemInfo`查看I/O相关的其他指标监控。

    **说明：**

    -   所有监控项都是MongoDB启动后的累加值，建议您不要直接查看。
    -   如果您开发了更加详细的MongoDB性能指标，也可以通过命令`db.serverStatus().systemInfo`查看。

## I/O问题的常见原因

常见导致MongoDB磁盘I/O问题的可能原因如下：

-   内存不够。I/O问题与内存的CacheSize⼤⼩息息相关。CacheSize越⼤，表示能够缓存的热数据越⼤，即系统需要的磁盘I/O量越低，则出现I/O瓶颈的概率越低；反之，CacheSize越⼩，表示能够缓存的热数据越少，系统刷脏更加频繁，则出现I/O瓶颈的概率越⼤。
-   与磁盘I/O相关的参数和配置问题。例如MongoDB Journal和运⾏⽇志频繁刷新，写入安全机制（WriteConcern）设置不合理，分⽚集群的MoveChunk错误等。

    关于更多Journal内容可参考：[https://docs.mongodb.com/manual/core/journaling/](https://docs.mongodb.com/manual/core/journaling/)。

    关于更多WriteConcern内容可参考：[https://docs.mongodb.com/manual/reference/write-concern/](https://docs.mongodb.com/manual/reference/write-concern/)。


## I/O问题的优化策略

如果是阿里云MongoDB，建议您根据业务需求选择合适的实例规格，并关注索引的优化和部分应用系统的写入优化。

-   配置合适的实例规格

    由于在配置前很难预估热数据与CacheSize的⽐例设置为多少最合适，通常情况下，在保证MongoDB实例满⾜业务要求的情况下，确保每日的最高CPU使⽤率和IOPS使⽤率控制在50%以内即可。

-   索引优化

    查询全表扫描或使用了不恰当的索引，例如导出全表数据期间，会消耗大量的I/O。创建过多的索引会使数据规模很大，导致WiredTiger Cache缓存的热数据减少，业务数据写操作过程中需要多⼀次I/O操作以更新索引，从而影响I/O性能。为了避免以上情况，建议您创建合适的索引，详情请参见[https://docs.mongodb.com/manual/indexes/](https://docs.mongodb.com/manual/indexes/)。

-   业务架构和运维优化

    在业务架构层⾯，要避免磁盘I/O成为瓶颈，需要优化以下几个方面：

    -   控制并发写入/读取线程数

        MongoDB是多线程应用，过⾼的并发写入速度和复杂查询并发数，容易引起IOPS瓶颈，甚⾄导致Secondary节点持续延迟。如果I/O瓶颈是由于业务写⼊量导致，建议您将MongoDB实例升级至MongoDB分⽚集群模式，通过数据的⽔平拆分来线性扩容MongoDB的写⼊性能。

    -   尽可能避免峰值写⼊

        部分业务由于定期写入或数据批量持久化，容易造成IOPS峰值。针对这种情况，在当前的实例配置不⾜以⽀撑该峰值写⼊的情况下，建议您将业务侧改造为平滑写入，例如给每⼀个批量写⼊操作添加⼀个随机时间⽚。

        ![IOPS峰值数据](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3237666161/p235815.png)

    -   避免业务⾼峰期间做运维操作

        部分对性能影响较⼤的运维操作，从本质上讲也会造成IOPS峰值。如果必须执行此类操作，建议您在业务低峰期执行。容易引起I/O⾼峰的常见操作有批量写⼊、更新、删除数据，添加索引，对集合执⾏Compact操作，批量导出数据等。


