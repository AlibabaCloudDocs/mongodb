---
keyword: [实例之间实现准实时表级单向同步, 数据库同步, 阿里云数据库同步]
---

# 使用MongoShake实现MongoDB副本集间的单向同步

通过阿里云自研的MongoShake工具，您可以实现MongoDB数据库间的数据同步，该功能可用于数据分析、灾备和多活等业务场景。本文以云数据库MongoDB实例间的数据实时同步为例介绍配置流程。

**说明：** 如果您需要实现副本集实例间的双向数据同步，您可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请。

## MongoShake介绍

MongoShake是阿里云以Golang语言编写的通用平台型服务工具，它通过读取MongoDB的Oplog操作日志来复制MongoDB的数据以实现特定需求。

MongoShake还提供了日志数据的订阅和消费功能，可通过SDK、Kafka、MetaQ等方式的灵活对接，适用于日志订阅、数据中心同步、Cache异步淘汰等场景。

**说明：** 如需了解更多MongoShake相关信息，请参见[MongoDB-shake Github主页](https://github.com/alibaba/MongoShake)。

## 支持的数据源

|源数据库|目标数据库|
|:---|:----|
|ECS上的自建MongoDB数据库|ECS上的自建MongoDB数据库|
|本地自建的MongoDB数据库|本地自建的MongoDB数据库|
|阿里云MongoDB实例|阿里云MongoDB实例|
|第三方云MongoDB数据库|第三方云MongoDB数据库|

## 注意事项

-   在全量数据同步完成之前，请勿对源库进行DDL操作，否则可能导致数据不一致。
-   不支持同步admin和local数据库。

## 数据库用户的权限要求

|同步的数据源|所需权限|
|:-----|:---|
|源MongoDB实例|readAnyDatabase权限、local库的read权限和mongoshake库的readWrite权限。**说明：** mongoshake库会在增量同步开始时由MongoShake程序自动在源实例中创建。 |
|目标MongoDB实例|readWriteAnyDatabase权限或目标库的readWrite权限。|

**说明：** 关于MongoDB数据库用户的创建及授权操作请参见[使用DMS管理MongoDB数据库用户](/cn.zh-CN/用户指南/账号管理/MongoDB数据库账号权限管理.md)或[db.createUser命令介绍](https://docs.mongodb.com/manual/reference/method/db.createUser/index.html)。

## 准备工作

1.  创建作为同步目标端的MongoDB副本集实例，详情请参见[创建副本集实例](/cn.zh-CN/快速入门/创建实例/创建副本集实例.md)。

    **说明：** 选择与源端的MongoDB实例相同的专有网络，便于ECS通过专有网络进行连接。

2.  创建用于运行MongoShake的ECS实例，详情请参见[创建ECS实例](https://help.aliyun.com/document_detail/25424.html)。

    **说明：** ECS的操作系统选择为Linux，并选择与MongoDB实例相同的专有网络。

3.  将ECS的IP地址加入至源端和目标端MongoDB实例的白名单中，并确保ECS可以连接源端和目标端MongoDB实例。

    **说明：** 建议通过专有网络进行互连，以获取最低的网络延迟。


## 操作步骤

1.  登录[ECS实例](https://help.aliyun.com/document_detail/25434.html)。
2.  执行如下命令格式下载MongoShake程序。

    ```
    wget 最新版MongoShake包下载地址
    ```

    **说明：** 最新版本的MongoShake包下载地址请参见[releases页面](https://github.com/alibaba/MongoShake/releases)。

3.  执行如下命令格式解压MongoShake程序。

    ```
    tar xvf mongoshake包文件名
    ```

4.  通过`vim`命令，修改MongoShake的配置文件collector.conf，涉及的主要参数的说明如下表所示。

    |参数|说明|示例值|
    |:-|:-|:--|
    |mongo\_urls|源端MongoDB实例的ConnectionStringURI格式连接地址。 **说明：**

    -   建议通过专有网络地址进行互连，以获取最低的网络延迟。
    -   关于ConnectionStringURI格式详情请参见[副本集实例连接说明]()。
|`mongo_urls = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`**说明：** 密码中不得包含艾特（@）字符，否则会导致连接失败。 |
    |tunnel.address|目标端MongoDB实例的ConnectionStringURI格式连接地址。|`tunnel.address = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`**说明：** 密码中不得包含艾特（@）字符，否则会导致连接失败。 |
    |sync\_mode|数据同步的方式，取值：     -   all：执行全量数据同步和增量数据同步。
    -   full：仅执行全量数据同步。
    -   incr：仅执行增量数据同步。
**说明：** 默认值为incr。

|`sync_mode = all`|

    **说明：** 关于collector.conf全量参数说明，请参见[附件](#section_uhl_7wp_94n)中的collector.conf全量参数说明。

5.  执行下述命令启动同步任务，并打印日志信息。

    ```
    ./collector.linux -conf=collector.conf -verbose
    ```

6.  观察打印的日志信息，当出现如下日志时，即代表全量数据同步已完成，并进入增量数据同步模式。

    ```
    [09:38:57 CST 2019/06/20] [INFO] (mongoshake/collector.(*ReplicationCoordinator).Run:80) finish full sync, start incr sync with timestamp: fullBeginTs[1560994443], fullFinishTs[1560994737]
    ```


## 监控MongoShake状态

增量数据同步开始后，您可以再开启一个命令行窗口，通过如下命令来监控MongoShake。

```
./mongoshake-stat --port=9100
```

**说明：** `mongoshake-stat`是一个Python脚本，执行之前请先安装Python 2.7版本，详情请参见[Python官网](https://www.python.org/downloads/)。

监控输出示例。

![监控输出](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6246819951/p49777.png)

|参数|说明|
|--|--|
|logs\_get/sec|每秒获取的oplog数量。|
|logs\_repl/sec|每秒执行重放操作的oplog数量。|
|logs\_success/sec|每秒成功执行重放操作的oplog数量。|
|lsn.time|最后发送oplog的时间。|
|lsn\_ack.time|目标端确认写入的时间。|
|lsn\_ckpt.time|CheckPoint持久化的时间。|
|now.time|当前时间。|
|replset|源数据库的副本集名称。|

## 附件

|参数目录|参数|说明|示例值|
|----|:-|:-|:--|
|无|conf.version|当前配置文件的版本号，请不要修改该值。|`conf.version = 4`|
|全局配置选项|id|同步任务的ID，可自定义。主要用于本次任务的日志名称、断点续传（checkpoint）位点信息存储的数据库名称、同步到目的端的数据库名称等。|`id = mongoshake`|
|master\_quorum|高可用选项。当主备MongoShake同时从一个源端同步数据时，主MongoShake中需要设置该参数为`ture`。 取值：

-   ture：开启
-   false：关闭

**说明：** 默认值为false。

|`master_quorum = false`|
|full\_sync.http\_port|HTTP端口，开放该端口可通过外网查看MongoShake的当前全量同步状态。**说明：** 默认值为9101。

|`full_sync.http_port = 9101`|
|incr\_sync.http\_port|HTTP端口，开放该端口可通过外网查看MongoShake的当前增量同步状态。**说明：** 默认值为9100。

|`incr_sync.http_port = 9100`|
|system\_profile\_port|Profiling端口，用于查看内部堆栈信息。|`system_profile_port = 9200`|
|log.level|日志的等级，取值： -   error：包含错误级别信息的日志。
-   warning：包含警告级别信息的日志。
-   info：反馈当前系统状态的日志。
-   debug：包含调试信息的日志。

默认值：info。

|`log.level = info`|
|log.dir|日志文件和pid文件的目录，不设置则默认使用当前路径的logs目录。**说明：** 本参数的路径必须设置为绝对路径。

|`log.dir = ./logs/`|
|log.file|日志文件的名称，可自定义。 **说明：** 默认值为collector.log。

|`log.file = collector.log`|
|log.flush|日志在屏幕上的刷新频率。取值： -   ture：打印每一条日志（对性能有影响）。
-   false：不一定能打印日志，但是保证性能。

**说明：** 默认值为false。

|`log.flush = false`|
|sync\_mode|数据同步的方式，取值： -   all：执行全量数据同步和增量数据同步。
-   full：仅执行全量数据同步。
-   incr：仅执行增量数据同步。

**说明：** 默认值为incr。

|`sync_mode = all`|
|mongo\_urls|源端MongoDB实例的ConnectionStringURI格式连接地址。 **说明：**

-   建议通过专有网络地址进行互连，以获取最低的网络延迟。
-   关于ConnectionStringURI格式详情请参见[副本集实例连接说明]()或[分片集群实例连接说明]()。

|`mongo_urls = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`|
|mongo\_cs\_url|如果源端的MongoDB类型为分片集群实例，需要输入ConfigServer（CS）节点的连接地址。如何申请ConfigServer节点的连接地址请参见[申请Shard或ConfigServer节点连接地址](/cn.zh-CN/用户指南/管理网络连接/Shard或Configserver连接地址/申请Shard或ConfigServer节点连接地址.md)。|`mongo_cs_url = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx-csxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx-csxxx.mongodb.rds.aliyuncs.com:3717/admin`|
|mongo\_s\_url|如果源端的MongoDB类型为分片集群实例，需要输入至少一个Mongos节点的连接地址，多个Mongos地址之间以英文逗号（,）分隔。如何申请Mongos节点的连接地址请参见[申请Shard或ConfigServer节点连接地址](/cn.zh-CN/用户指南/管理网络连接/Shard或Configserver连接地址/申请Shard或ConfigServer节点连接地址.md)。|`mongos_s_url = mongodb://root:Ftxxxxxx@s-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,s-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717/admin`|
|tunnel|同步的通道类型。取值： -   direct：直接同步到目标MongoDB实例。
-   rpc：通过NET/RPC方式同步。
-   tcp：通过TCP方式同步。
-   file：通过文件传输方式同步。
-   kafka：通过Kafka方式同步。
-   mock：仅用于测试，不写入通道。

**说明：** 默认值为direct。

|`tunnel = direct`|
|tunnel.address|目标端的链接地址，支持如下地址： -   当turnel参数为`direct`时，请输入目标端MongoDB实例的ConnectionStringURI格式连接地址。
-   当turnel参数为`rpc`时，请输入目标端实例rpc的接收地址。
-   当turnel参数为`tcp`时，请输入目标端实例的tcp接收地址。
-   当turnel参数为`file`时，请输入目标端实例数据的文件路径。
-   当turnel参数为`kafka`时，请输入kafka的地址，例如`topic@brokers1,brokers2`
-   当turnel参数为`mock`时，此参数不填。

|`tunnel.address = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`|
|tunnel.message|通道数据的类型，仅限tunnel参数为`kafka`或`file`时有效。取值： -   raw：默认的类型，采用聚合的模式进行写入和读取。
-   json：以`JSON`格式写入kafka，便于用户直接读取。
-   bson：以`BSON`二进制的格式写入kafka。

**说明：** 默认值为raw。

|`tunnel.message = raw`|
|mongo\_connect\_mode|MongoDB实例的连接模式，仅限tunnel参数为`direct`时有效。取值： -   primary：从primary节点中拉取数据。
-   secondaryPreferred：从secondary节点中拉取数据。
-   standalone：从指定的单个节点中拉取数据。

**说明：** 默认值为secondaryPreferred。

|`mongo_connect_mode = secondaryPreferred`|
|filter.namespace.black|指定数据同步的黑名单，这些指定的命名空间不会被同步至目标数据库，多个命名空间用英文分号（;）分隔。 **说明：** 命名空间是指MongoDB中集合或索引的规范名称，是由数据库名称和集合或索引名称的组合，例如`mongodbtest.customer`。

|`filter.namespace.black = mongodbtest.customer;testdata.test123`|
|filter.namespace.white|指定数据同步的白名单，只有这些指定的命名空间会被同步至目标数据库，多个命名空间用英文分号（;）分隔。|`filter.namespace.white = mongodbtest.customer;test123`|
|filter.pass.special.db|启用特殊库的同步。正常同步过程中，admin、local、mongoshake、config、system.views等库会被系统过滤掉，您可以在有特殊需求时启用上述库的同步。多个库名用英文分号（;）分隔。|`filter.pass.special.db = admin;mongoshake`|
|filter.ddl\_enable|是否开启DDL同步。取值： -   true：开启
-   false：关闭

**说明：** 源端为MongoDB分片集群实例时不支持开启。

|`filter.ddl_enable = false`|
|checkpoint.storage.url|配置Checkpoint存储地址，用于支持断点续传。如不配置，程序将根据实例类型写入如下对应的数据库： -   MongoDB副本集实例：写入mongoshake库中。
-   MongoDB分片集群实例：写入ConfigServer节点的admin库中。

|`checkpoint.storage.url = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`|
|checkpoint.storage.db|Checkpoint存储的数据库名。 **说明：** 默认为mongoshake。

|`checkpoint.storage.db = mongoshake`|
|checkpoint.storage.collection|Checkpoint存储的集合名。在开启主备MongoShake同时从一个源端同步数据时，可以修改该表名以防止表名重复引起冲突。 **说明：** 默认为ckpt\_default。

|`checkpoint.storage.collection = ckpt_default`|
|checkpoint.start\_position|断点续传的开始位置，如果checkpoint位点已经存在则本参数无效。取值的格式：`*YYYY*-*MM*-*DD*T*HH*:*MM*:*SS*Z`。**说明：** 默认值为1970-01-01T00:00:00Z。

|`checkpoint.start_position = 1970-01-01T00:00:00Z`|
|transform.namespace|将源库的库名或集合名重新命名并同步到目的库。如：将源库中的`A库.B集合`重新命名成`C库.D集合`并同步到目的库。|`transform.namespace = fromA.fromB:toC.toD`|
|全量数据同步选项|full\_sync.reader.collection\_parallel|设置MongoShake单次最多并发拉取多少个集合。|`full_sync.reader.collection_parallel = 6`|
|full\_sync.reader.write\_document\_parallel|设置MongoShake对单个集合写入的并发线程数。|`full_sync.reader.write_document_parallel = 8`|
|full\_sync.reader.document\_batch\_size|设置MongoShake对目的端单次写入文档的聚合（batch）大小。如：128表示单次聚合128个文档后再写入。|`full_sync.reader.document_batch_size = 128`|
|full\_sync.collection\_exist\_drop|设置目的库存在同名集合时的处理方式。取值： -   true：先删除目标重名集合再同步。

**警告：** 此操作会删除目的端的集合，请务必提前做好备份。

-   false：如检测到目的库中有重名集合则直接报错退出。

|`full_sync.collection_exist_drop = true`|
|full\_sync.create\_index|完成同步后是否创建索引。取值： -   foreground：创建前台索引
-   background：创建后台索引
-   none：不创建索引

|`full_sync.create_index = none`|
|full\_sync.executor.insert\_on\_dup\_update|目的库中有`_id`重复字段时是否将`INSERT`语句更改为`UPDATE`语句。取值： -   true：更改
-   false：不更改

|`full_sync.executor.insert_on_dup_update = false`|
|full\_sync.executor.filter.orphan\_document|源端为分片集群实例时，是否过滤孤儿文档（Orphaned document）。取值： -   true：过滤
-   false：不过滤

|`full_sync.executor.filter.orphan_document = false`|
|full\_sync.executor.majority\_enable|是否启用目的端的多数写（Majority write）功能。取值： -   true：启用
-   false：不启用

|`full_sync.executor.majority_enable = false`|
|增量数据同步选项|incr\_sync.mongo\_fetch\_method|配置增量数据拉取方法。取值： -   oplog：从源库中拉取oplog。
-   change\_stream：从源库中拉取change事件（仅支持MongoDB 4.0及以上版本）。

默认值：oplog

|`incr_sync.mongo_fetch_method = oplog`|
|incr\_sync.oplog.gids|用于云上集群搭建双向复制。如有需求请提交[工单](https://workorder.console.aliyun.com/#/ticket/list)申请GIDS。|`incr_sync.oplog.gids = xxxxxxxxxxxx`|
|incr\_sync.shard\_key|MongoShake内部处理并发的方式。请勿修改该参数。|`incr_sync.shard_key = collection`|
|incr\_sync.worker|传输oplog的并发线程数。如果主机性能足够，可以提高线程数。 **说明：** 如果是分片集群实例，线程数必须等同于分片（shard）数量。

|`incr_sync.worker = 8`|
|incr\_sync.worker.oplog\_compressor|启用压缩数据功能以减少网络带宽消耗。取值： -   none：不压缩
-   gzip：以gzip格式压缩
-   zlib：以zlib格式压缩
-   deflate：以deflate格式压缩

**说明：** 本参数仅限于tunnel参数非`direct`模式下使用。当tunnel为`direct`时，请将本参数设置为`none`。

|`incr_sync.worker.oplog_compressor = none`|
|incr\_sync.target\_delay|设置源端与目的端的延迟同步。通常源端中的变更会实时同步到目的端，为了防止误操作，您可以通过设置本参数达到延迟同步的目的。如：`incr_sync.target_delay = 1800`为设置30分钟的延迟。单位：秒。 **说明：** 0表示不启用延迟同步。

|`incr_sync.target_delay = 1800`|
|incr\_sync.worker.batch\_queue\_size|MongoShake内部队列的配置参数。如无特殊情况请勿修改。|`incr_sync.worker.batch_queue_size = 64`|
|incr\_sync.adaptive.batching\_max\_size|`incr_sync.adaptive.batching_max_size = 1024`|
|incr\_sync.fetcher.buffer\_capacity|`incr_sync.fetcher.buffer_capacity = 256`|
|MongoDB同步选项（仅适用于`direct`模式）|incr\_sync.executor.upsert|当`_id`（重复字段）或唯一索引不存在时，是否将`UPDATE`语句更改为`INSERT`语句。取值： -   true：更改
-   false：不更改

|`incr_sync.executor.upsert = false`|
|incr\_sync.executor.insert\_on\_dup\_update|当`_id`（重复字段）或唯一索引不存在时，是否将`INSERT`语句更改为`UPDATE`语句。取值： -   true：更改
-   false：不更改

|`incr_sync.executor.insert_on_dup_update = false`|
|incr\_sync.conflict\_write\_to|同步时如果存在写冲突，是否记录冲突文档。取值： -   none：不记录
-   db：将冲突日志写入mongoshake\_conflict
-   sdk：将冲突日志写入sdk

|`incr_sync.conflict_write_to = none`|
|incr\_sync.executor.majority\_enable|是否在目的端启用多数写（Majority write）。取值： -   true：启用
-   false：不启用

**说明：** 如果启用则会对性能造成一定影响。

|`incr_sync.executor.majority_enable = false`|

