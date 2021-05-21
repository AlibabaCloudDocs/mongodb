# 关于MongoDB Sharding，你应该知道的

关于MongoDB Sharding的相关知识。

## 什么情况下使用Sharded cluster？

当您遇到如下两个问题时，您可以使用Sharded cluster来解决您的问题：

-   存储容量受单机限制，即磁盘资源遭遇瓶颈。
-   读写能力受单机限制，可能是CPU、内存或者网卡等资源遭遇瓶颈，导致读写能力无法扩展。

## 如何确定shard、mongos数量？

当您决定使用Sharded cluster时，到底应该部署多少个shard、多少个mongos？shard、mongos的数量归根结底是由应用需求决定：

-   如果您使用sharding只是解决海量数据存储问题，访问并不多。假设单个shard能存储M， 需要的存储总量是N，那么您可以按照如下公式来计算实际需要的shard、mongos数量：
    -   numberOfShards = N/M/0.75 （假设容量水位线为75%）
    -   numberOfMongos = 2+（对访问要求不高，至少部署2个mongos做高可用即可）
-   如果您使用sharding是解决高并发写入（或读取）数据的问题，总的数据量其实很小。您要部署的shard、mongos要满足读写性能需求，容量上则不是考量的重点。假设单个shard最大QPS为M，单个mongos最大QPS为Ms，需要总的QPS为Q。那么您可以按照如下公式来计算实际需要的shard、mongos数量：

    -   numberOfShards = Q/M/0.75 （假设负载水位线为75%）
    -   numberOfMongos = Q/Ms/0.75
    **说明：** mongos、mongod的服务能力，需要用户根据访问特性来实测得出。


如果sharding要同时解决上述2个问题，则按需求更高的指标来预估。以上估算是基于sharded cluster里数据及请求都均匀分布的理想情况。但实际情况下，分布可能并不均衡，为了让系统的负载分布尽量均匀，就需要合理的选择shard key。

## 如何选择shard key？

MongoDB Sharded cluster支持2种分片方式：

-   范围分片，通常能很好的支持基于shard key的范围查询。
-   Hash 分片，通常能将写入均衡分布到各个shard。

上述2种分片策略都无法解决以下3个问题：

-   shard key取值范围太小（low cardinality），比如将数据中心作为shard key，而数据中心通常不会很多，分片的效果肯定不好。
-   shard key某个值的文档特别多，这样导致单个chunk特别大（及 jumbo chunk），会影响chunk迁移及负载均衡。
-   根据非shardkey进行查询、更新操作都会变成scatter-gather查询，影响效率。

好的shard key应该拥有如下特性：

-   key分布足够离散（sufficient cardinality）
-   写请求均匀分布（evenly distributed write）
-   尽量避免scatter-gather查询（targeted read）

例如某物联网应用使用MongoDB Sharded cluster存储海量设备的工作日志。假设设备数量在百万级别，设备每10s向 MongoDB汇报一次日志数据，日志包含deviceId，timestamp信息。应用最常见的查询请求是查询某个设备某个时间内的日志信息。以下四个方案中前三个不建议使用，第四个为最优方案，主要是为了给客户做个对比。

-   方案1： 时间戳作为shard key，范围分片：
    -   Bad。
    -   新的写入都是连续的时间戳，都会请求到同一个shard，写分布不均。
    -   根据deviceId的查询会分散到所有shard上查询，效率低。
-   方案2： 时间戳作为shard key，hash分片：
    -   Bad。
    -   写入能均分到多个shard。
    -   根据deviceId的查询会分散到所有shard上查询，效率低。
-   方案3：deviceId作为shardKey，hash分片（如果ID没有明显的规则，范围分片也一样）：
    -   Bad。
    -   写入能均分到多个shard。
    -   同一个deviceId对应的数据无法进一步细分，只能分散到同一个chunk，会造成jumbo chunk根据deviceId的查询只请求到单个shard。不足的是，请求路由到单个shard后，根据时间戳的范围查询需要全表扫描并排序。
-   方案4：（deviceId，时间戳）组合起来作为shardKey，范围分片（Better）：
    -   Good。
    -   写入能均分到多个shard。
    -   同一个deviceId的数据能根据时间戳进一步分散到多个chunk。
    -   根据deviceId查询时间范围的数据，能直接利用（deviceId，时间戳）复合索引来完成。

## 关于jumbo chunk及chunk size

MongoDB默认的chunk size为64MB，如果chunk超过64MB且不能分裂（比如所有文档的shard key都相同），则会被标记为jumbo chunk ，balancer不会迁移这样的chunk，从而可能导致负载不均衡，应尽量避免。

一旦出现了jumbo chunk，如果对负载均衡要求不高，并不会影响到数据的读写访问。如果一定要处理，可以尝试如下方法：

-   对jumbo chunk进行split，一旦split成功，mongos会自动清除jumbo标记。
-   对于不可再分的chunk，如果该chunk已不是jumbo chunk，可以尝试手动清除chunk的jumbo标记（注意先备份下config数据库，以免误操作导致config库损坏）。
-   调大chunk size，当chunk大小不超过chunk size时，jumbo标记最终会被清理。但是随着数据的写入仍然会再出现 jumbo chunk，根本的解决办法还是合理的规划shard key。

关于chunk size如何设置，绝大部分情况下可以直接使用默认的chunk size ，以下场景可能需要调整chunk size（取值在1-1024之间）：

-   迁移时IO负载太大，可以尝试设置更小的chunk size。
-   测试时，为了方便验证效果，设置较小的chunk size。
-   初始chunk size设置不合理，导致出现大量jumbo chunk影响负载均衡，此时可以尝试调大chunk size。
-   将未分片的集合转换为分片集合，如果集合容量太大，需要（数据量达到T级别才有可能遇到）调大chunk size才能转换成功。具体方法请参见[Sharding Existing Collection Data Size](https://docs.mongodb.com/manual/core/sharded-cluster-requirements/)。

## Tag aware sharding

[Tag aware sharding](https://docs.mongodb.com/manual/core/zone-sharding/)是Sharded cluster很有用的一个特性，允许用户自定义一些chunk的分布规则。Tag aware sharding原理如下：

1.  sh.addShardTag\(\)给shard设置标签A。
2.  sh.addTagRange\(\)给集合的某个chunk范围设置标签A，最终MongoDB会保证设置标签A的chunk范围（或该范围的超集）分布设置了标签A的shard上。

## Tag aware sharding可应用在如下场景

-   将部署在不同机房的shard设置机房标签，将不同chunk范围的数据分布到指定的机房。
-   将服务能力不同的shard设置服务等级标签，将更多的chunk分散到服务能力更强的shard上去。

使用Tag aware sharding需要注意：

chunk分配到对应标签的shard上无法立即完成，而是在不断insert、update后触发split、moveChunk后逐步完成的并且需要保证balancer是开启的。在设置了tag range一段时间后，写入仍然没有分布到tag相同的shard上去。

## 关于负载均衡

MongoDB Sharded cluster的自动负载均衡目前是由mongos的后台线程来做，并且每个集合同一时刻只能有一个迁移任务。负载均衡主要根据集合在各个shard上chunk的数量来决定的，相差超过一定阈值（跟chunk总数量相关）就会触发chunk迁移。

负载均衡默认是开启的，为了避免chunk迁移影响到线上业务，可以通过设置迁移执行窗口，比如只允许凌晨2:00-6:00期间进行迁移。

```
use config
                db.settings.update(
                { _id: "balancer" },
                { $set: { activeWindow : { start : "02:00", stop : "06:00" } } },
                { upsert: true }
                )
            
```

> 注意：在进行sharding备份时（通过mongos或者单独备份config server和所有shard），需要停止负载均衡，以免备份出来的数据出现状态不一致问题。

```
sh.stopBalancer()
            
```

## moveChunk归档设置

使用3.0及以前版本的Sharded cluster可能会遇到一个问题，停止写入数据后，数据目录里的磁盘空间占用还会一直增加。

上述行为是由sharding.archiveMovedChunks配置项决定的，该配置项在3.0及以前的版本默认为true。即在move chunk 时，源shard会将迁移的chunk数据归档一份在数据目录里，当出现问题时，可用于恢复。也就是说，chunk发生迁移时，源节点上的空间并没有释放出来，而目标节点又占用了新的空间。

**说明：** 在3.2版本，该配置项默认值也被设置为false，默认不会对moveChunk的数据在源shard上归档。

## recoverShardingState设置

使用MongoDB Sharded cluster时，还可能遇到一个问题：

启动shard后，shard不能正常服务，Primary上调用ismaster时，结果却为true，也无法正常执行其他命令，其状态类似如下：

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
                "electionId" : ObjectId("57c7e62d218e9216c70aa3cf"),
                "maxBsonObjectSize" : 16777216,
                "maxMessageSizeBytes" : 48000000,
                "maxWriteBatchSize" : 1000,
                "localTime" : ISODate("2016-09-01T12:29:27.113Z"),
                "maxWireVersion" : 4,
                "minWireVersion" : 0,
                "ok" : 1
                }
            
```

查看其错误日志，会发现shard一直无法连接上config server，是由sharding.recoverShardingState选项决定，默认为true。也就是说shard启动时会连接config server进行sharding状态的一些初始化，如果config server连不上，初始化工作就一直无法完成，导致shard 状态不正常。

在您将Sharded cluster所有节点都迁移到新的主机上时可能会遇到了上述问题，因为config server的信息发生变化，而 shard启动时还会连接之前的config server。通过在启动命令行加上`setParameter recoverShardingState=false`来启动shard就能恢复正常。

