# MongoDB实例空间使用率高问题

MongoDB实例的空间使⽤率是⼀个⾮常重要的监控指标。如果MongoDB实例的空间被完全使用，将会导致实例不可⽤。本文介绍查看MongoDB实例空间使用情况的方法，以及各种空间使用情况的原因和优化策略。

实例空间使用率达到80%~85%以上时，可通过降低数据库实际占用空间或扩容存储空间的方法避免空间占满的风险。

## 查看空间使用情况

-   副本集架构

    当MongoDB实例为副本集架构时，MongoDB管理控制台提供以下方法查看空间使用情况：

    -   总体概览

        在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**基本信息**页面，查看当前实例总存储空间的使用情况。

        ![查看当前实例总存储空间的使用情况](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4829666161/p236112.png)

    -   监控图分析

        在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**监控信息**页面，选择目标节点，查看对应节点的空间使用情况。

        **说明：** MongoDB副本集实例提供一个可供读写访问的Primary节点（主节点），一个或多个提供高可用的Secondary节点（从节点）、一个隐藏的Hidden节点（隐藏节点）和一个或多个可选的ReadOnly节点（只读节点）。MongoDB节点的空间使用由data\_size和log\_size组成，即ins\_size=data\_size+log\_size。其中：

        -   data\_size是数据磁盘使⽤空间（不包括local库），主要包括collection开头的数据物理⽂件，索引开头的索引物理⽂件和部分元数据物理⽂件，例如WiredTiger.wt。
        -   log\_size包括local库的物理⼤⼩，mongodb运⾏⽇志⼤⼩和部分审计⽇志⼤⼩。
        ![查看节点的空间使用情况](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3829666161/p236408.png)

    -   详细分析

        当MongoDB实例为副本集架构时，可以通过以下两种方法分析空间使用问题。

        -   通过MongoDB自身提供的命令`db.stats()`和`db.$collection_name.stats()`分析。

            MongoDB官方提供的分析命令，详情请参见：

            -   [https://docs.mongodb.com/manual/reference/method/db.stats/](https://docs.mongodb.com/manual/reference/method/db.stats/)
            -   [https://docs.mongodb.com/manual/reference/method/db.collection.stats/](https://docs.mongodb.com/manual/reference/method/db.collection.stats/)
            -   [https://docs.mongodb.com/manual/reference/method/db.collection.storageSize/](https://docs.mongodb.com/manual/reference/method/db.collection.storageSize/)
            -   [https://docs.mongodb.com/manual/reference/method/db.collection.totalIndexSize/](https://docs.mongodb.com/manual/reference/method/db.collection.totalIndexSize/)
            -   [https://docs.mongodb.com/manual/reference/method/db.collection.totalSize/](https://docs.mongodb.com/manual/reference/method/db.collection.totalSize/)
        -   在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**CloudDBA** \> **空间分析**页面分析。

            **说明：** 在**CloudDBA** \> **空间分析**页面，您可以查看以下内容，更多信息请参见[空间分析](https://help.aliyun.com/document_detail/162422.html)。

            -   数据库和表使用空间情况概览、⽇均增⻓量和预测可⽤天数。
            -   异常数据库和表使用空间情况。
            -   详细业务表使用空间情况，包括索引文件大小、数据文件大小，压缩率分析，平均⾏⻓等。
            ![使用“CloudDBA-空间分析”查看空间使用情况](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4829666161/p236429.png)

-   分⽚集群架构

    当MongoDB实例为分片集群架构时，MongoDB管理控制台提供以下方法查看空间使用情况：

    -   监控图分析

        在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**监控信息**页面，选择目标节点，查看对应节点的空间使用情况。

        ![查看各个Shard中各个角色的空间使用情况](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4829666161/p236471.png)

    -   详细分析

        当MongoDB实例为分片集群架构时，通过MongoDB自身提供的命令`db.stats()`和`db.$collection_name.stats()`依次分析各个节点的空间使用情况。


## 执行compact指令导致数据量过大

-   compact⽅法和compact期间对实例的影响

    由于compact执⾏的时间与集合的数据量相关，如果数据量过大，则会使compact的执行时间很长，所以为避免影响业务的读写，建议在业务低峰期执⾏compact。compact方法很简单，首先在备库上执行命令`db.runCommand({compact:"collectionName"})`，然后进行主备切换，以减少compact期间对业务的影响。

    **说明：**

    -   collectionName为集合名称，请根据实际情况替换。
    -   MongoDB 4.4以后的官方版本，compact命令将不再阻塞业务读写，compact命令的使用方法和限制请参见：[https://docs.mongodb.com/manual/reference/command/compact/](https://docs.mongodb.com/manual/reference/command/compact/)、[https://mongoing.com/archives/26907](https://mongoing.com/archives/26907)和[https://help.aliyun.com/document\_detail/96530.html](https://help.aliyun.com/document_detail/96530.html)。
-   compact⽆效

    compact的基本原理并不是⽴⻢开辟新的空间存放数据来替换原来的⽂件，⽽是将数据不断地往前⾯的空间空洞挪动，所以在某些场景下虽然存在空间空洞，但内部的compact算法并不能保证肯定可以复⽤这些空洞，我们称之为compact无效。compact无效的场景和解决方法如下：

    -   在完成compact后，虽然提示操作成功，但实际上磁盘空间并没有回收，对于该场景，建议您通过重建副本的方式解决。
    -   MongoDB 3.4以前的版本，在删除大量数据后，compact⽆法回收索引文件，只对数据⽂件⽣效，对于该场景，建议您将内核版本升级⾄3.4以上。这种场景的确认方法有两种：
        1.  执行命令`db.$table_name.stats().indexSizes`。
        2.  查看索引物理文件大小。

## 日志过大导致空间上涨

-   Journal Log过⼤导致主备空间差距巨⼤

    MongoDB 4.0以前的版本，如果宿主机的open files达到设置上限，则会使MongoDB内部的log server清理线程中断，进而使Journal Log过大导致空间无限上涨，当通过MongoDB的运行日志查看到类似以下内容时，您可以通过将内核版本升级到MongoDB 4.0以上，或者通过重启mongod进程进行临时解决，详情请参见：[https://jira.mongodb.org/browse/WT-4083](https://jira.mongodb.org/browse/WT-4083)。

    ```
    2019-08-25T09:45:16.867+0800 I NETWORK [thread1] Listener: accept() returns -1 Too many open files in system 
    2019-08-25T09:45:17.000+0800 I - [ftdc] Assertion: 13538:couldn't open [/proc/55692/stat] Too many open files in system src/mongo/util/processinfo_linux.cpp 74
    2019-08-25T09:45:17.002+0800 W FTDC [ftdc] Uncaught exception in 'Location13538: couldn't open [/proc/55692/stat] Too many open files in system' in full-time diagnostic data capture subsystem. Shutting down the full-time diagnostic data capture subsystem.
    ```

-   备库延迟和增量备份可能导致从节点⽇志空间持续增⻓

    阿里云MongoDB在出现主备延迟的情况下，oplog可以使用的大小不再受限于配置文件定义的固定集合大小，理论上使得可以达到用户申请磁盘容量的20%，但当备库延迟恢复后，oplog之前占⽤的物理空间并不会回缩。

    阿⾥云MongoDB使⽤物理备份的⽅式在隐藏节点备份MongoDB实例期间会有⼤量的chepoint，进而导致占⽤了更多的数据和⽇志空间。

    对于以上两种场景，通过对oplog单独做compact操作解决，具体如下：

    **说明：** 进行compact期间会阻塞所有的写操作。

    ```
    db.grantRolesToUser("root", [{db: "local", role: "dbAdmin"}])
    use local
    db.runCommand({ compact: "oplog.rs", force: true  })
    ```


## 选择和使用分片不合理导致数据分布不均衡

-   sharding key类型选择不合理

    在⼀个分⽚集群中，⽚键类型的选择⾄关重要，⼀般会使⽤hash分⽚或者ranged分⽚两种类型。通常情况下，在磁盘均衡度⽅⾯，hash分⽚的策略会⽐ranged好很多，因为根据不同的key值，MongoDB通过内部的哈希函数可以使得数据均匀地分布在不同地分⽚上，⽽range分⽚⼀般是根据key的⼤⼩范围进⾏数据分布，所以往往会造成这样的⼀个现象：新插⼊的数据在⼀个热点的chunk上，不但会引起该chunk所在的shard磁盘I/O过⾼，也会带来短期数据不均匀的场景。

    ![数据均匀分布](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4829666161/p236752.png)

    ![短期数据不均匀分布](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4829666161/p236753.png)

    如上图所示，所有的数据写⼊chunk C所在分⽚，当chunk C写满以后会在本分⽚中split出新的 chunk，后续通过集群负载均衡器Balancer迁移chunk，但这个迁移需要耗费⼤量的时间和I/O，在⼀个⾼并发写⼊的场景下，数据的负载均衡速度可能跟不上数据写⼊速度，从⽽造成分⽚之间数据容量不均的问题。在这种使⽤场景下，不建议使⽤range分⽚策略。

    Sharding Key类型介绍，详情请参见：[https://docs.mongodb.com/manual/core/sharding-shard-key/](https://docs.mongodb.com/manual/core/sharding-shard-key/)、[https://docs.mongodb.com/manual/core/hashed-sharding/](https://docs.mongodb.com/manual/core/hashed-sharding/)和[https://docs.mongodb.com/manual/core/ranged-sharding/](https://docs.mongodb.com/manual/core/ranged-sharding/)。

-   sharding key字段选择不合理

    各个分⽚上的chunk数量基本⼀致，但实际上绝⼤部分数据都只存储在部分chunk上，导致这些热点chunk所在的分⽚上的数据量远远⼤于其他分⽚上的数据量，执行命令`sh.status()`查看MongoDB的运行日志，从日志中可以查看到以下类似告警信息：

    ```
    2019-08-27T13:31:22.076+0800 W SHARDING [conn12681919] possible low cardinality key detected in superHotItemPool.haodanku_all - key is { batch: "201908260000" } 
    2019-08-27T13:31:22.076+0800 W SHARDING [conn12681919] possible low cardinality key detected in superHotItemPool.haodanku_all - key is { batch: "201908260200" } 
    2019-08-27T13:31:22.076+0800 W SHARDING [conn12681919] possible low cardinality key detected in superHotItemPool.haodanku_all - key is { batch: "201908260230" }
    ```

    mongos负载均衡主要考虑的是各个shard的chunk数量保持相当，就认为数据是均衡的，所以就会出现以上的极端场景：虽然各个shard数量相当，但实际数据严重倾斜。因为⼀个chunk内shardKey⼏乎完全相同但⼜触发到64MB的chunk分裂阈值，这时就会分裂出⼀个空的chunk。久⽽久之，虽然chunk的数量变多了并且完成了chunk的迁移，但实际上迁移⾛的chunk都是空的chunk，造成了chunk数量均衡但实际数据不均衡的情况。对于这种情况，需要在架构上重新设计，选择合适的区分度较⾼的列作为sharding key。关于spilt的介绍，详情请参见[https://docs.mongodb.com/manual/core/sharding-data-partitioning/](https://docs.mongodb.com/manual/core/sharding-data-partitioning/)和[https://docs.mongodb.com/manual/tutorial/split-chunks-in-sharded-cluster/](https://docs.mongodb.com/manual/tutorial/split-chunks-in-sharded-cluster/)。

-   部分db未做分片

    MongoDB分⽚集群实例允许部分db做分片，部分db不做分片。那么必然会带来这样的⼀个问题：不做分片的db的数据必然只能存在⼀个分⽚上，如果该db数据量很⼤，可能会造成该分⽚的数据量远⼤于其他分⽚。

    从⼀个源端mongos集群导⼊到⼀个新的mongos集群，但逻辑导⼊过程中忽略了实现在⽬标端mongos集群做好分片设计的步骤。

    针对上述问题，我们建议：

    -   如果是因为⽬标集群初始化导⼊，导⼊之前做好分⽚设计。
    -   如果不做分片的库很多且数据量基本相当，通过MongoDB提供的命令`movePriamy`将指定数据库迁移到指定分⽚。
    -   如果存在某个数据库的数据量极⼤且未做分片，建议对其做分片设计或者将其拆分出来当作单⼀的副本集对待。
    -   如果出现这种情况，但磁盘空间足够大，建议忽略该问题。
-   ⼤规模的movechunk操作可能引起分⽚的磁盘占⽤不均

    movechunk的本质是向⽬标端shard写⼊数据后remove源端数据。默认情况下，remove操作不会释放空间，因为对于wiredTiger引擎，每个表都有独⽴的数据⽂件和索引⽂件，如果该⽂件不删除，总的磁盘空间就不可能回缩。通常最容易引起该问题的操作为：之前的sharding集群中未做shard设计，运⾏⼀段时间后才做了Sharding。

    从原理上说movechunk引起的空间碎⽚和⼤规模删除⼀样，因此针对出现⼤量movechunk或者remove⽂档的情况，可以针对该分⽚进⾏compact操作来回收碎⽚空间，正常情况下compact后数据会进⾏重组以回收⽂件的碎⽚空间。

    movechunk的介绍，详情请参见：[https://docs.mongodb.com/manual/tutorial/migrate-chunks-in-sharded-cluster/](https://docs.mongodb.com/manual/tutorial/migrate-chunks-in-sharded-cluster/)和[https://docs.mongodb.com/manual/tutorial/manage-sharded-cluster-balancer/](https://docs.mongodb.com/manual/tutorial/manage-sharded-cluster-balancer/)。


