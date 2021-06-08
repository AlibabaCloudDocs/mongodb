# MongoDB 分片集群介绍

MongoDB分片集群技术用于解决海量数据的存储问题，本文介绍MongoDB分片集群相关的常用知识。

## 什么情况下使用分片集群？

当您遇到如下问题时，可以使用分片集群解决：

-   存储容量受单机限制，即磁盘资源遭遇瓶颈。
-   读写能力受单机限制，可能是CPU、内存或者网卡等资源遭遇瓶颈，导致读写能力无法扩展。

## 如何确定shard、mongos数量？

您可以根据以下方法确定shard和mongos的使用数量：

-   分片集群仅用于解决海量数据的存储问题，且访问量不多。例如一个shard能存储M， 需要的存储总量是N，那么您的业务需要的shard和mongos数量按照以下公式计算：
    -   numberOfShards = N/M/0.75 （假设容量水位线为75%）
    -   numberOfMongos = 2+（对访问要求不高，至少部署2个mongos做高可用）
-   分片集群用于解决高并发写入（或读取）数据的问题，但总的数据量很小。即shard和mongos需要满足读写性能需求，例如一个shard的最大QPS为M，一个mongos的最大QPS为Ms，业务需要的总QPS为Q，那么您的业务需要的shard和mongos数量按照以下公式计算：

    -   numberOfShards = Q/M/0.75 （假设负载水位线为75%）
    -   numberOfMongos = Q/Ms/0.75
    **说明：** mongos、mongod的服务能力，需要用户根据访问特性来实测得出。


**说明：**

-   如果分片集群同时解决上述两个问题，则按照需求更高的指标进行预估。
-   上述计算方法是基于分片集群中数据和请求都均为分布的理想情况下进行预估，实际情况下，分布可能并不均匀，为了让系统的负载尽量均匀，您需要选择合理的Shard Key。

## 如何选择Shard Key？

-   MongoDB分片集群支持的分片策略
    -   范围分片，支持基于Shard Key的范围查询。
    -   哈希分片，能够将写入均衡分布到各个shard。
    -   Tag aware sharding，您可以自定义一些chunk的分布规则。

        **说明：**

        -   原理
            1.  `sh.addShardTag()`给shard设置标签A。
            2.  `sh.addTagRange()`给集合的某个chunk范围设置标签A，最终MongoDB会保证设置标签A的chunk范围（或该范围的超集）分布设置了标签A的shard上。
        -   应用场景
            -   将部署在不同机房的shard设置机房标签，将不同chunk范围的数据分布到指定的机房。
            -   将服务能力不同的shard设置服务等级标签，将更多的chunk分散到服务能力更强的shard上去。
        -   注意事项

            chunk分配到对应标签的shard上无法立即完成，而是在不断insert、update后触发split、moveChunk后逐步完成的并且需要保证balancer是开启的。在设置了tag range一段时间后，写入仍然没有分布到tag相同的shard上去。

        更多信息请参见[Tag aware sharding](https://docs.mongodb.com/manual/core/zone-sharding/)。

-   范围分片和哈希分片无法解决的问题
    -   Shard Key的取值范围太小，例如将数据中心作为Shard Key，由于数据中心通常不多，则分片效果不好。
    -   Shard Key中某个值的文档特别多，会导致单个chunk特别大（即 jumbo chunk），会影响chunk迁移及负载均衡。
    -   根据非Shard Key进行查询、更新操作都会变成scatter-gather查询，影响效率。
-   好的Shard Key拥有的特性
    -   key分布足够离散（sufficient cardinality）
    -   写请求均匀分布（evenly distributed write）
    -   尽量避免scatter-gather查询（targeted read）

示例：

场景：某物联网应用使用MongoDB分片集群存储海量设备的工作日志。如果设备数量在百万级别，设备每10秒向MongoDB汇报一次日志数据，日志包含设备ID（deviceId）和时间戳（timestamp）信息。应用最常见的查询请求是查询某个设备某个时间内的日志信息。

查询请求：查询某个设备某个时间内的日志信息。

-   （推荐）方案一：组合设备ID和时间戳作为Shard Key，进行范围分片。
    -   写入能均分到多个shard。
    -   同一个设备ID的数据能根据时间戳进一步分散到多个chunk。
    -   根据设备ID查询时间范围的数据，能直接利用（deviceId，时间戳）复合索引来完成。
-   方案二： 时间戳作为Shard Key，进行范围分片。
    -   新的写入为连续的时间戳，都会请求到同一个分片，写分布不均。
    -   根据设备ID的查询会分散到所有shard上查询，效率低。
-   方案三： 时间戳作为Shard Key，进行哈希分片。
    -   写入能均分到多个shard上。
    -   根据设备ID的查询会分散到所有shard上查询，效率低。
-   方案四：设备ID作为Shard Key，进行哈希分片。

    **说明：** 如果设备ID没有明显的规则，可以进行范围分片。

    -   写入能均分到多个shard上。
    -   同一个设备ID对应的数据无法进一步细分，只能分散到同一个chunk，会造成jumbo chunk，根据设备ID的查询只请求到单个shard，请求路由到单个shard后，根据时间戳的范围查询需要全表扫描并排序。

## 关于jumbo chunk及chunk size

MongoDB默认的chunk size为64 MB，如果chunk超过64 MB且不能分裂（假如所有文档的Shard Key都相同），则会被标记为jumbo chunk，balancer不会迁移这样的chunk，从而可能导致负载不均衡，应尽量避免。

当出现jumbo chunk时，如果对负载均衡要求不高，并不会影响到数据的读写访问。如果您需要处理，可以使用如下方法：

-   对jumbo chunk进行split，split成功后mongos会自动清除jumbo标记。
-   对于不可再分的chunk，如果该chunk已不是jumbo chunk，可以尝试手动清除chunk的jumbo标记。

    **说明：** 清除前，您需要先备份config数据库，避免误操作导致config库损坏。

-   调大chunk size，当chunk大小不超过chunk size时，jumbo标记最终会被清理。但是随着数据的写入仍然会再出现jumbo chunk，根本的解决办法还是合理的规划Shard Key。

需要调整chunk size（取值范围为1~1024 MB）的场景：

-   迁移时I/O负载太大，可以尝试设置更小的chunk size。
-   测试时，为了方便验证效果，设置较小的chunk size。
-   初始chunk size设置不合理，导致出现大量jumbo chunk影响负载均衡，此时可以尝试调大chunk size。
-   将未分片的集合转换为分片集合，如果集合容量太大，需要（数据量达到T级别才有可能遇到）调大chunk size才能转换成功。具体方法请参见[Sharding Existing Collection Data Size](https://docs.mongodb.com/manual/core/sharded-cluster-requirements/)。

## 关于负载均衡

MongoDB分片集群的自动负载均衡目前是由mongos的后台线程来做，并且每个集合同一时刻只能有一个迁移任务。负载均衡主要根据集合在各个shard上chunk的数量来决定的，相差超过一定阈值（和chunk总数量相关）就会触发chunk迁移。

负载均衡默认是开启的，为了避免chunk迁移影响到线上业务，可以通过设置迁移执行窗口，例如只允许凌晨02:00~06:00期间进行迁移。

```
use config
                db.settings.update(
                { _id: "balancer" },
                { $set: { activeWindow : { start : "02:00", stop : "06:00" } } },
                { upsert: true }
                )
            
```

**说明：** 在进行分片集群备份时（通过mongos或单独备份ConfigServer和所有shard），需要执行以下命令停止负载均衡，避免备份的数据出现状态不一致问题。

```
sh.stopBalancer()            
```

## moveChunk归档设置

MongoDB 3.0及以前版本的分片集群可能存在停止写入数据后，数据目录里的磁盘空间占用还会一直增加的问题。

上述问题是由`sharding.archiveMovedChunks`配置项决定的，该配置项在MongoDB 3.0及以前的版本默认为`true`。即在moveChunk时，源shard会将迁移的chunk数据进行归档设置，当出现问题时，用于恢复。也就是说，chunk发生迁移时，源节点上的空间并没有释放出来，而目标节点又占用了新的空间。

**说明：** 在MongoDB 3.2版本，该配置项默认值为`false`，默认不会对moveChunk的数据在源shard上归档。

## recoverShardingState设置

使用MongoDB分片集群时，可能遇到如下问题：

启动shard后，shard不能正常服务，且在主节点上调用ismaster时，结果为true，也无法正常执行其他命令，其状态类似如下：

```
mongo-9003:PRIMARY> db.isMaster()
                {
                "hosts" : [
                "host1:9003",
                "host2:9003",
                "host3:9003"
                ],
                "setName" : "mongo-9003",
                "setVersion" : 9,
                "ismaster" : false,  // primary 的 ismaster 为 false？？？
                "secondary" : true,
                "primary" : "host1:9003",
                "me" : "host1:9003",
                "electionId" : ObjectId("57c7e62d218e9216c70a****"),
                "maxBsonObjectSize" : 16777216,
                "maxMessageSizeBytes" : 48000000,
                "maxWriteBatchSize" : 1000,
                "localTime" : ISODate("2016-09-01T12:29:27.113Z"),
                "maxWireVersion" : 4,
                "minWireVersion" : 0,
                "ok" : 1
                }
            
```

查看其错误日志，会发现shard一直无法连接ConfigServer，是由`sharding.recoverShardingState`选项决定，默认为true。即shard启动时会连接ConfigServer进行sharding状态的一些初始化，如果ConfigServer连不上，初始化工作就一直无法完成，导致shard的状态异常。

在您将分片集群所有节点都迁移到新的主机上时可能会遇到上述问题，因为ConfigServer的信息发生变化，而shard启动时还会连接之前的ConfigServer。通过在启动命令行加上`setParameter recoverShardingState=false`来启动shard就能恢复正常。

