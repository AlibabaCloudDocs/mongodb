# MongoDB 4.4功能概览

阿里云作为MongoDB官方的独家战略合作伙伴，全网首次引入MongoDB 4.4版本并已于2020年11月发布。而MongoDB官方4.4版本已经在2020年7月30日正式发布。和往年的大版本不同，本次的4.4版本是以往版本的全面加强版，主要针对用户呼声最高的一些痛点重点进行了改进。

## Hidden Indexes

众所周知数据库维护太多的索引会导致写性能下降，但是往往业务上的复杂性导致了运维人员不敢轻易去删除一个潜在的低效率索引，担心误删除会带来业务性能的抖动，而重建索引的代价也非常大。

为了解决上述问题，[阿里云数据库MongoDB版](https://www.aliyun.com/product/mongodb?spm=5176.12418109.h2v3icoap.116.436729b3RpUJq5)和MongoDB官方达成战略合作后共同开发了Hidden Indexes功能。该功能支持通过`collMod`命令隐藏现有的索引，保证该索引在后续的查询中不会被使用。在观察一段时间后，确定业务没有异常即可以放心删除该索引。

参考代码：

```
db.runCommand( {
   collMod: 'testcoll',
   index: {
      keyPattern: 'key_1',
      hidden: false
   }
} )
```

需要注意的是，索引被隐藏之后仅对MongoDB的执行计划器不可见，这并不会改变索引本身的一些特殊行为，如唯一键约束、TTL淘汰等。

**说明：** 索引在隐藏期间也不会停止更新，所以当需要该索引时，可以通过取消隐藏使其立刻可用。

## Refinable Shard Keys

在MongoDB分片集群中，一个好的[Shard key](https://docs.mongodb.com/manual/core/sharding-shard-key/#choosing-a-shard-key)至关重要，因为它决定了分片集群在指定的Workload（工作量）下是否有良好的扩展性。但是在实际使用MongoDB的过程中，即使我们事先仔细斟酌了要选择的Shard Key，也会因为Workload的变化而导致出现Jumbo Chunk（超过预设大小的Chunk），或者业务流量都打向单一分片的情况。

在4.0及之前的版本中，集合选定的Shard Key及其对应的Value都是不能更改的，到了4.2版本，虽然可以修改Shard Key的Value，但是数据的跨分片迁移以及基于分布式事务的实现机制导致性能开销很大，而且并不能完全解决Jumbo Chunk或访问热点的问题。例如，现在有一个订单表，Shard Key为`{customer_id:1}`，在业务初期每个客户不会有很多的订单，这样的Shard Key完全可以满足需求，但是随着业务的发展，某个大客户累积的订单越来越多，进而对这个客户订单的访问成为某个单一分片的热点，由于订单和`customer_id`天然的关联关系，修改`customer_id`并不能改善访问不均的情况。

针对上述类似场景，在4.4版本中，您可以通过[refineCollectionShardKey](https://docs.mongodb.com/master/reference/command/refineCollectionShardKey/#dbcmd.refineCollectionShardKey)命令给现有的Shard Key增加一个或多个Suffix Field来改善现有的文档在Chunk上的分布问题。例如在上面描述的订单业务场景中，通过`refineCollectionShardKey`命令把Shard key更改为`{customer_id:1, order_id:1}`，即可避免单一分片上的访问热点问题。

并且，`refineCollectionShardKey`命令的性能开销非常低，仅更改Config Server节点上的元数据，不需要任何形式的数据迁移，数据的打散仍然在后续正常的Chunk自动分裂和迁移的流程中逐步进行。此外，Shard Key需要有对应的Index来支撑，因此`refineCollectionShardKey`命令要求提前创建新Shard Key所对应的Index。

由于并不是所有的文档都存在新增的Suffix Field，因此在4.4版本中隐式支持了Missing Shard Key功能，即新插入的文档可以不包含指定的Shard Key Field。但是由于很容易产生Jumbo Chunk，因此并不建议使用。

## Compound Hashed Shard Keys

在4.4之前的版本中，您只能指定单字段的哈希片键，原因是当时版本的MongoDB不支持复合哈希索引，这样就很容易导致集合数据在分片上分布不均匀。

在最新的4.4版本中加入了复合哈希索引，即您可以在复合索引中指定单个哈希字段，位置不限，可以作为前缀，也可以作为后缀，进而也就提供了对复合哈希片键的支持。

参考代码：

```
sh.shardCollection(
  "examples.compoundHashedCollection",
  { "region_id" : 1, "city_id": 1, field1" : "hashed" }
)
sh.shardCollection(
  "examples.compoundHashedCollection",
  { "_id" : "hashed", "fieldA" : 1}
)
```

复合哈希索引有很多优点，例如如下两个场景：

-   应法律法规的要求，需要使用MongoDB的[zone sharding](https://docs.mongodb.com/manual/tutorial/manage-shard-zone/)功能，把数据尽量均匀打散在某个地域的分片上。
-   集合指定的片键的值是递增的，例如上文例子中的`{customer_id:1, order_id:1}`这个片键，如果`customer_id`是递增的，并且业务也总是访问最新顾客的数据，导致大部分的流量总是访问单一分片。

在没有复合哈希片键支持的情况下，只能提前对需要的字段进行哈希值的计算，并将结果存储到文档中的某个特殊字段中，然后再通过范围分片的方式指定其作为片键来解决上述问题。

而在4.4版本中只需直接把目标字段指定为哈希即可轻松解决上述问题。例如，针对上述第二个场景，仅需将片键设置为`{customer_id:'hashed', order_id:1}`即可在极大程度上简化业务逻辑的复杂性。

## Hedged Reads

页面的响应速度和经济损失直接挂钩。Google有一个[研究报告](https://unbounce.com/landing-pages/7-page-speed-stats-for-marketers/)表明，如果网页的加载时间超过3秒，用户的跳出率会增加50%。针对这个问题，MongoDB在4.4版本中提供了Hedged Reads功能，即在分片集群场景下，mongos节点会把一个读请求同时发送给某个分片的两个副本集成员，然后选择最快的返回结果回复客户端，来减少业务上的P95（指过去十秒内95%的请求延迟均在规定范围内）和P99延迟（指过去十秒内99%的请求延迟均在规定范围内）。

Hedged Reads功能作为[Read Preference](https://docs.mongodb.com/manual/core/read-preference/)参数的一部分来提供， 因此可以在Operation粒度上进行配置，当Read Preference指定为`nearest`时，系统默认启用Hedged Reads功能，当指定为primary时，不支持Hedged Reads功能，当指定为其他时，需要显式地指定`hedgeOptions`才可以启用Hedged Reads。如下所示：

```
db.collection.find({ }).readPref(
   "secondary",                      // mode
   [ { "datacenter": "B" },  { } ],  // tag set
   { enabled: true }                 // hedge options
)
```

此外，Hedged Reads也需要mongos开启支持，配置[readHedgingMode](https://docs.mongodb.com/manual/reference/parameters/#param.readHedgingMode)参数为`on`，使mongos开启该功能支持。

参考代码：

```
db.adminCommand( { setParameter: 1, readHedgingMode: "on" } )
```

## 降低复制延迟

本次4.4的更新带来了主备复制延迟的降低。对于MongoDB来说，主备复制的延迟会对读写有非常大的影响。在某些特定的场景下，备库需要及时地复制并应用主库的增量更新，才可以继续进行读写操作。因此，更低的复制延迟会带来更好的一致性体验。

## Streaming Replication

在4.4之前的版本中，备库需要通过不断地轮询upstream来获取增量更新操作。每次轮询时，备库主动给主库发送一个`getMore`命令读取Oplog集合，如果有数据，会返回一个最大16MB的Batch，如果没有数据，备库也会通过[awaitData](https://docs.mongodb.com/manual/reference/method/cursor.addOption/)选项来控制备库无谓的`getMore`开销，同时能够在有新的增量更新时，第一时间获取到对应的Oplog。拉取操作是通过单个OplogFetcher线程来完成，每个Batch的获取都需要经历一个完整的RTT（Round-Trip Time，往返时间），在副本集网络状况不好的情况下，复制的性能就严重受限于网络延迟。

而在4.4版本中，增量的Oplog是不断地主动流向备库的，而不是被动地依靠备库轮询。相比于备库轮询的方式，至少在Oplog的获取上节省了一半的RTT。在以下两个场景中，Streaming Replication功能会大大提升性能：

-   当用户的写操作指定了[writeConcern](https://docs.mongodb.com/manual/reference/write-concern/)参数为`"majority"`时，写操作需要等待足够多次数的“备库返回复制成功”。而在新的复制机制下，高延迟的网络环境也可以平均提升50%的`majority`写性能。
-   当用户使用了因果一致性（Causal Consistency）的场景下，为了保证可以在备库读到自己的写操作（Read Your Write），同样强依赖备库对主库Oplog的及时复制。

## Simultaneous Indexing

4.4 之前的版本中，索引的创建需要在主库中完成之后，才会到备库上执行。备库上的创建动作在不同的版本中，因为创建机制和创建方式的不同，对备库Oplog的影响也大有不同。

但即使在4.2版本中统一了前后台索引创建机制，使用了相当细粒度的加锁机制（只在索引创建的开始和结束阶段对集合加独占锁），也会因为索引创建本身的CPU、IO性能开销导致复制延迟，或是因为一些特殊操作，例如使用`collMod`命令修改集合元信息，而导致Oplog的应用阻塞，甚至会因为主库历史Oplog被覆盖而进入[Recovering](https://docs.mongodb.com/v4.2/core/index-creation/#index-builds-in-replicated-environments)状态。

在4.4版本中，主库和备库上的索引创建操作是同时进行的，这样可以大幅减少上述情况所带来的主备延迟，即使在索引创建过程中，也可以保证备库访问到最新的数据。

此外，新的索引创建机制规定，只有在大多数具备投票权限节点返回成功后，索引才会真正生效。所以，也可以减轻在读写分离场景下因为索引不同而导致的性能差异。

## Mirrored Reads

在阿里云数据库MongoDB版以往提供服务的过程中，有一个现象，即大多数用户虽然购买的是三节点副本集实例，但是实际在使用过程中读写都是在Primary节点进行，其中一个可见的Secondary节点并未承载任何读流量，导致在偶尔的宕机切换之后，用户能明显感受到业务的访问延迟，经过一段时间后才会恢复到之前的水平，原因就在于新选举出的主节点之前从未提供过读服务，并不了解业务的访问特征，没有针对性地对数据做缓存，所以在突然提供服务后，读操作会出现大量的缓存未命中（Cache Miss），需要从磁盘重新加载数据，造成访问延迟上升。在大内存实例的情况下，这个问题尤为明显。

在4.4版本中，MongoDB针对上述问题实现了[Mirrored Reads](https://docs.mongodb.com/master/release-notes/4.4/#mirrored-reads)功能，即主节点会按一定的比例把读流量复制到备库上执行，来帮助备库预热缓存。这是一个非阻塞执行（Fire and Forgot）的行为，不会对主库的性能产生任何实质性的影响，但是备库负载会有一定程度的上升。

流量复制的比例是可动态配置的，通过[mirrorReads](https://docs.mongodb.com/master/reference/parameters/#param.mirrorReads)参数设置，默认复制`1%`的流量。

参考代码：

```
db.adminCommand( { setParameter: 1, mirrorReads: { samplingRate: 0.10 } } )
```

此外，还可以通过`db.serverStatus( { mirroredReads: 1 } )`来查看Mirrored Reads相关的统计信息，如下所示：

```
SECONDARY> db.serverStatus( { mirroredReads: 1 } ).mirroredReads
{ "seen" : NumberLong(2), "sent" : NumberLong(0) }
```

## Resumable Initial Sync

在4.4之前的版本中，如果备库在做全量同步时出现网络抖动而导致连接闪断，那么备库需要从头开始全量同步，导致之前的工作全部白费，这个情况在数据量比较大时会对业务造成巨大的影响。

在4.4版本中，MongoDB提供了从中断位置继续执行同步的能力。如果在闪断后一直无法连接成功，系统会重新选择一个同步源进行新的全量同步。该过程的默认超时时间为24小时，您可以通过`replication.initialSyncTransientErrorRetryPeriodSeconds`在进程启动时更改。

需要注意的是，对于全量同步过程中遇到的非网络异常导致的中断，仍然需要重新发起全量同步。

## Time-Based Oplog Retention

MongoDB中的Oplog集合记录了所有数据的变更操作，除了用于复制，还可用于增量备份、数据迁移、数据订阅等场景，是MongoDB数据生态的重要基础设施。

Oplog是通过[Capped Collection](https://docs.mongodb.com/manual/core/capped-collections/)来实现的，虽然从3.6版本开始，MongoDB支持通过`replSetResizeOplog`命令动态修改Oplog集合的大小，但是往往不能准确反映下游对Oplog增量数据的需求，您可以考虑如下场景：

-   计划在凌晨2~4点对某个Secondary节点进行停机维护，需要避免上游Oplog被清理而触发全量同步。
-   下游的数据订阅组件可能会因为一些异常情况而停止服务，但是最慢会在3个小时之内恢复服务并继续进行增量拉取，也需要避免上游的增量缺失。

由此可见，在大部分应用场景下，需要保留最近一个时间段内的Oplog，而这个时间段内产生多少Oplog往往是很难确定的。

在4.4版本中，MongoDB支持通过[storage.oplogMinRetentionHours](https://docs.mongodb.com/master/reference/configuration-options/#storage.oplogMinRetentionHours)参数定义需要保留的Oplog时长，也可以通过`replSetResizeOplog`命令在线修改这个值，参考代码如下：

```
// First, show current configured value
db.getSiblingDB("admin").serverStatus().oplogTruncation.oplogMinRetentionHours
// Modify
db.adminCommand({
  "replSetResizeOplog" : 1,
  "minRetentionHours" : 2
})
```

## Union

在多表联合查询能力上，4.4之前的版本只提供了一个[$lookup stage](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/)用于实现类似于SQL中的`left outer join`功能，而4.4版本中新增了[$unionWith stage](https://docs.mongodb.com/master/reference/operator/aggregation/unionWith/)用于实现类似于SQL的`union all`功能，用于将两个集合中的数据聚合到一个结果集中，然后做指定的查询和过滤。区别于`$lookup stage`的是，`$unionWith stage`支持分片集合。在Aggregate Pipeline中使用多个`$unionWith stage`，可以对多个集合数据做聚合，使用方式如下：

```
{ $unionWith: { coll: "<collection>", pipeline: [ <stage1>, ... ] } }
```

您也可以在pipeline参数中指定不同的stage，用于在对集合数据做聚合前进行一定的过滤，使用起来非常灵活。例如，某个业务上对订单数据按表拆分存储到不同的集合中，第二季度有如下数据：

```
db.orders_april.insertMany([
  { _id:1, item: "A", quantity: 100 },
  { _id:2, item: "B", quantity: 30 },
]);
db.orders_may.insertMany([
  { _id:1, item: "C", quantity: 20 },
  { _id:2, item: "A", quantity: 50 },
]);
db.orders_june.insertMany([
  { _id:1, item: "C", quantity: 100 },
  { _id:2, item: "D", quantity: 10 },
]);
```

假设需要列出第二季度中不同产品的销量，在4.4版本之前，可能需要业务自己把数据都读出来，然后在应用层面做聚合才能解决这个问题，或者依赖某种数据仓库产品来做分析，而在4.4版本中只需要如下一条Aggregate语句即可解决问题：

```
db.orders_april.aggregate( [
   { $unionWith: "orders_may" },
   { $unionWith: "orders_june" },
   { $group: { _id: "$item", total: { $sum: "$quantity" } } },
   { $sort: { total: -1 }}
] )
```

## Custom Aggregation Expressions

4.4之前的版本中，您可以通过`find`命令中的[$where operator](https://docs.mongodb.com/master/reference/operator/query/where/#op._S_where)或者MapReduce功能来实现在Server端执行自定义的JavaScript脚本，进而提供更为复杂的查询能力，但是这两个功能并没有做到和Aggregation Pipeline在使用上的统一。

在4.4版本中，MongoDB提供了[$accumulator](https://docs.mongodb.com/master/reference/operator/aggregation/accumulator/#grp._S_accumulator)和[$function](https://docs.mongodb.com/master/reference/operator/aggregation/function/#exp._S_function)这两个新的Aggregation Pipeline Operator用来取代`$where operator`和MapReduce。借助于Server Side JavaScript来实现自定义的Aggregation Expression，这样做到复杂查询的功能接口都集中到Aggregation Pipeline中，完善接口统一性和用户体验的同时，也可以把Aggregation Pipeline本身的执行模型利用上，实现一举多得的效果。

`$accumulator`和MapReduce功能有些相似，会先通过`init`函数定义一个初始的状态，然后根据指定的`accumate`函数更新每一个输入文档的状态，并且根据需要决定是否执行`merge`函数。

例如，假设在分片集合上使用了`$accumulator operator`，则需要将在不同分片上执行完成的结果做`merge`，并且如果指定了`finalize`函数，那么在所有输入文档处理完成后，还会根据该函数将状态转换为最终的输出。

`$function`和`$where operator`在功能上基本一致，但其强大之处在于可以和其他Aggregation Pipeline Operator配合使用，此外也可以在`find`命令中借助`$expr operator`来使用`$function operator`，等价于之前的`$where operator`，MongoDB官方在文档中也建议优先使用`$function operator`。

## 其他易用性增强

除了上述`$accumulator`和`$function operator`，4.4版本中还新增了其他多个Aggregation Pipeline Operator，例如字符串处理、获取数组收尾元素、还有用来获取文档或二进制串大小的操作符，具体请参见下表：

|操作符|说明|
|---|--|
|$accumulator|返回用户定义的[accumulator operator](https://docs.mongodb.com/master/reference/operator/aggregation/#agg-operators-group-accumulators)结果。|
|$binarySize|返回指定字符串或二进制数据的大小（以字节为单位）。|
|$bsonSize|返回编码为BSON时指定文档（即bsontype对象）的字节大小。|
|$first|返回数组中的第一个元素。|
|$function|用来自定义aggregation表达式。|
|$last|返回数组中的最后一个元素。|
|$isNumber|如果指定的表达式类型为整数、十进制、双精度或长整型，则返回布尔值`true`。如果表达式类型为BSON类型、null或缺失字段，则返回布尔值`false`。|
|$replaceOne|替换第一个通过指定的字符串匹配到的实例。|
|$replaceAll|替换所有通过指定的字符串匹配到的实例。|

Connection Monitoring and Pooling

4.4版本的Driver中增加了对客户端连接池的行为监控和自定义配置，通过标准的API来订阅和连接池相关的事件，包括连接的关闭和开启、连接池的清理。也可以通过API来配置连接池的一些行为，例如拥有的最大或最小连接数、每个连接的最大空闲时间、线程等待可用连接时的超时时间等。具体可以参见[MongoDB官方设计文档](https://github.com/mongodb/specifications/blob/master/source/connection-monitoring-and-pooling/connection-monitoring-and-pooling.rst)。

Global Read and Write Concerns

在4.4之前的版本中，如果执行的操作没有显式地指定`readConcern`或者`writeConcern`，则会有默认行为。例如：`readConcern`默认为`local`，`writeConcern`默认为`{w: 1}`。但这个默认行为不可以变更，如果用户想让所有`insert`操作的`writeConcern`默认为 `{w: majority}`，那么只能在所有访问MongoDB的代码中显式指定该值。

而在4.4版本中，可以通过[setDefaultRWConcern](https://docs.mongodb.com/master/reference/command/setDefaultRWConcern/#dbcmd.setDefaultRWConcern)命令来配置全局默认的`readConcern`和`writeConcern`。参考代码：

```
db.adminCommand({
  "setDefaultRWConcern" : 1,
  "defaultWriteConcern" : {
    "w" : "majority"
  },
  "defaultReadConcern" : { "level" : "majority" }
})
```

您也可以通过[getDefaultRWConcern](https://docs.mongodb.com/master/reference/command/getDefaultRWConcern/#dbcmd.getDefaultRWConcern)命令获取当前默认的`readConcern`和`writeConcern`。

此外，在4.4版本中记录慢日志或诊断日志的时候，会记录当前操作的`readConcern`或者`writeConcern`设置的来源，两者共通的来源有如下三种：

|来源|说明|
|--|--|
|clientSupplied|由应用自己指定。|
|customDefault|由用户通过`setDefaultRWConcern`命令指定。|
|implicitDefault|完全没做任何配置，Server默认行为。|

`writeConcern`还有如下一种来源：

|来源|说明|
|--|--|
|getLastErrorDefaults|继承自副本集的`settings.getLastErrorDefaults`配置。|

New MongoDB Shell \(beta\)

对于MongoDB的运维人员来说，使用最多的工具可能就是mongo shell，4.4版本提供了新版本的mongo shell，增加了诸如代码高亮、命令自动补全、更具可读性的错误信息等非常人性化的功能。目前提供的是beta版本，很多命令还未提供支持，仅供体验。

![新版MongoShell](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8116272061/p172857.png)

## 结语

本次发布的4.4版本主要是一个维护性的版本，除了上述解读，还有很多其他小的优化，例如[$indexStats](https://docs.mongodb.com/master/release-notes/4.4/#indexstats)优化、TCP Fast Open支持优化建连、索引删除优化等等。还有一些相对大的增强，例如新的结构化日志[LogV2](https://github.com/mongodb/mongo/blob/master/src/mongo/logv2/README.md)、新的安全机制支持等。详情请参见官方的[Release Notes](https://docs.mongodb.com/master/release-notes/4.4/)。

