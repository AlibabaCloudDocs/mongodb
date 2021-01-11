# 使用NimoShake将Amazon DynamoDB迁移至阿里云

NimoShake（又名DynamoShake）是阿里云研发的数据同步工具，您可以借助该工具将Amazon DynamoDB数据库迁移至阿里云。

已经创建阿里云MongoDB实例，详情请参见[创建副本集实例](/cn.zh-CN/快速入门/创建实例/创建副本集实例.md)或[创建分片集群实例](/cn.zh-CN/快速入门/创建实例/创建分片集群实例.md)。

本文档主要介绍NimoShake工具及其使用方法。

NimoShake主要用于从DynamoDB进行迁移，目的端支持MongoDB和兼容DynamoDB协议的MongoDB实例。更多详情请参见[NimoShake介绍](https://github.com/alibaba/NimoShake)。

## 注意事项

在执行全量数据迁移时将占用源库和目标库一定的资源，可能会导致数据库服务器负载上升。如果数据库业务量较大或服务器规格较低，可能会加重数据库压力，甚至导致数据库服务不可用。建议您在执行数据迁移前谨慎评估，在业务低峰期执行数据迁移。

## 名词解释

-   断点续传：断点续传是指将一个任务分成多个部分进行传输，当遇到网络故障或者其他原因造成的传输中断，可以延续之前传输的部分继续传输，而不用从头开始。

    **说明：** 全量同步不支持断点续传功能，增量同步支持断点续传，如果增量同步过程中连接断开了，在一定时间内恢复连接是可以继续进行增量同步的。但在某些情况下，比如断开的时间过久，或者之前位点的丢失，都会导致重新触发全量同步。

-   位点：增量的断点续传是根据位点来实现的，默认的位点是写入到目的端MongoDB中，库名是dynamo-shake-checkpoint。每个表都会记录一个checkpoint的表，同样还会有一个status\_table表记录当前是全量同步还是增量同步。

## NimoShake功能特性

NimoShake目前支持全量和增量分离的同步机制，即先同步全量数据，再同步增量数据。

-   全量同步：包含数据同步和索引同步两个部分，基本架构如下：

    ![全量同步基本架构](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4246819951/p128818.png)

    -   数据同步：NimoShake使用多个并发线程拉取源端数据，如下图所示。

        ![数据同步](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4246819951/p128828.png)

        |线程名称|说明|
        |----|--|
        |Fecher|调用Amazon提供的协议转换驱动批量抓取源表的数据并放入队列中，直至抓取完源表的所有数据。 **说明：** 目前只提供一个Fetcher线程。 |
        |Parser|从队列中读取数据，并解析成BSON结构。Parser解析完成后，将数据按条写入Executor队列。Parser线程可以启动多个，默认为2个，您可以通过`FullDocumentParser`参数调整Parser的个数。|
        |Executor|从队列中拉取数据，并将数据进行聚合后写入目的端MongoDB（聚合上限16MB，总条数1024）。Executor线程可以启动多个，默认为4个，您可以通过`FullDocumentConcurrency`参数调整Executor的个数。|

    -   索引同步：NimoShake会在完成数据同步之后写入索引。索引分为自带索引和用户索引两部分：
        -   自带索引：如您有分区键（Partition key）和排序键（Sort key），NimoShake将会创建一个联合唯一索引写入MongoDB，除此之外，NimoShake还会针对分区键创建一个哈希（Hash）索引同时写入。如果您只有一个分区键，那么最终写入到MongoDB的将会是一个哈希索引和一个唯一索引。
        -   用户索引：如果您有自建的索引，NimoShake将会根据主键（Primary key）创建一个哈希索引写入MongoDB。
-   增量同步：增量同步只同步数据，不同步增量同步过程中产生的索引。其基本架构如下：

    ![增量同步架构图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4246819951/p128843.png)

    |线程名称|说明|
    |----|--|
    |Fetcher|感知流（Stream）中分片（shard）的变化。|
    |Manager|进行消息的通知，或者创建新的Dispatcher处理消息，一个shard对应一个Dispatcher。|
    |Dispatcher|从源端拉取增量数据。如果是断点续传，则会从上一次的Checkpoint位点开始拉取，而不是从头拉取。|
    |Batcher|对Dispatcher线程拉取的增量数据进行数据解析和打包整合。|
    |Executor|将整合后的数据写入到MongoDB，同时更新checkpoint位点。|


## 将Amazon DynamoDB迁移至阿里云

本步骤以Ubuntu系统为例，介绍如何使用NimoShake将Amazon Dynamo数据库迁移到阿里云数据库。

1.  在系统中执行如下命令下载NimoShake包，等待下载完成。

    ```
    wget https://github.com/alibaba/NimoShake/releases/download/release-v1.0.0-20191015/nimo.tar.gz
    ```

    **说明：** 建议下载最新版本的NimoShake包，下载地址请参见[NimoShake](https://github.com/alibaba/NimoShake/releases)。

2.  执行如下命令解压下载的NimoShake包。

    ```
    tar zxvf nimo.tar.gz
    ```

3.  解压完成后，输入`cd nimo`命令进入nimo文件夹。

4.  输入`vi nimo-shake.conf`命令打开NimoShake的配置文件。

5.  配置NimoShake，各配置项说明如下：

    |参数|说明|示例值|
    |--|--|---|
    |id|迁移任务的ID，可自定义，用于输出pid文件等信息，如本次任务的日志名称、断点续传（checkpoint）位点信息存储的数据库名称、同步到目的端的数据库名称。|`id = nimo-shake`|
    |log.file|日志文件路径，不配置将打印到stdout。|`log.file = nimo-shake.log`|
    |log.level|日志的等级，取值：     -   none：不收集日志。
    -   error：包含错误级别信息的日志。
    -   warn：包含警告级别信息的日志。
    -   info：反馈当前系统状态的日志。
    -   debug：包含调试信息的日志。
默认值：info。

|`log.level = info`|
    |log.buffer|是否启用日志缓冲区。取值：     -   true：启用。启用后能保证性能，但退出时可能会丢失最后几条日志。
    -   false：不启用。不启用将会降低性能但保证退出时每条日志都被打印。
默认值：true。

|`log.buffer = true`|
    |system\_profile|PPROF端口，作调试用，打印堆栈协程信息。|`system_profile = 9330`|
    |http\_profile|HTTP端口，开放该端口可通过外网查看NimoShake的当前状态。|`http_profile = 9340`|
    |sync\_mode|同步的类型，取值如下：     -   all：执行全量数据同步和增量数据同步。
    -   full：仅执行全量同步。
    -   incr：仅执行增量同步。
默认值：all。

**说明：** 程序默认执行全量数据同步和增量数据同步。如果您只希望执行全量数据同步或增量数据同步，请将参数改为full或者incr。

|`sync_mode = all`|
    |source.access\_key\_id|DynamoDB端的AccessKey ID。|`source.access_key_id = xxxxxxxxxxx`|
    |source.secret\_access\_key|DynamoDB端的AccessKey。|`source.secret_access_key = xxxxxxxxxx`|
    |source.session\_token|DynamoDB端的临时密钥，如没有可以不配置。|`source.session_token = xxxxxxxxxx`|
    |source.region|DynamoDB所属的地域，如没有可以不配置。|`source.region = us-east-2`|
    |source.session.max\_retries|会话失败后的最大重试次数。|`source.session.max_retries = 3`|
    |source.session.timeout|会话超时时间，0为不启用。单位：毫秒。|`source.session.timeout = 3000`|
    |filter.collection.white|数据同步的白名单，设置允许通过的表名。如`filter.collection.white = c1;c2`表示允许C1和C2表通过，剩下的表全部过滤。 **说明：** 不能同时指定filter.collection.white和filter.collection.black参数，否则表示全部表通过。

|`filter.collection.white = c1;c2`|
    |filter.collection.black|数据同步的黑名单，设置需要过滤的表名。如`filter.collection.black = c1;c2`表示过滤掉C1和C2表，剩下的表全部通过。 **说明：** 不能同时指定filter.collection.white和filter.collection.black参数，否则表示全部表通过。

|`filter.collection.black = c1;c2`|
    |qps.full|全量同步阶段，限制`Scan`命令对表执行的频率，表示每秒钟最多调用多少次`Scan`。默认值：1000。|`qps.full = 1000`|
    |qps.full.batch\_num|全量同步阶段，每秒拉取多少条数据。默认值：128。|`qps.full.batch_num = 128`|
    |qps.incr|增量同步阶段，限制`GetRecords`命令对表执行的频率，表示每秒钟最多调用多少次`GetRecords`。默认值：1000。|`qps.incr = 1000`|
    |qps.incr.batch\_num|增量同步阶段，每秒拉取多少条数据。默认值：128。|`qps.incr.batch_num = 128`|
    |target.type|目的端数据库类型，取值：    -   mongodb：目的端为MongoDB数据库。
    -   aliyun\_dynamo\_proxy：目的端为兼容DynamoDB协议的MongoDB数据库。
**说明：** 目前aliyun\_dynamo\_proxy选项仅支持中国站。

|`target.type = mongodb`|
    |target.mongodb.type|目的端MongoDB数据库的类型，取值：     -   replica：副本集
    -   sharding：分片集群
|`target.mongodb.type = sharding`|
    |target.address|目的端数据库的连接地址，支持MongoDB的连接串地址和DynamoDB兼容连接地址。目前DynamoDB协议实例仅支持中国站。    -   获取MongoDB的地址信息，请参见[副本集实例连接说明]()或[分片集群实例连接说明]()。
    -   获取DynamoDB兼容连接地址信息，请参见[获取DynamoDB协议兼容版实例的连接地址](/cn.zh-CN/DynamoDB协议兼容版/获取DynamoDB协议兼容版实例的连接地址.md)。
**说明：** 目前DynamoDB兼容连接地址仅支持中国站。

|`target.address = mongodb://username:password@s-*****-pub.mongodb.rds.aliyuncs.com:3717`|
    |target.db.exist|目的端重名表的处理方式，取值：     -   rename：对目的端已存在的重名表进行重命名，添加时间戳后缀，比如c1变为c1.2019-07-01Z12:10:11。

警告：

此操作会修改目的端的表名称，可能会对业务产生影响，请务必提前做好迁移的准备工作。

    -   drop：删除目的端的重名表。
如不配置则不作处理，此时如果目的端中有重名表会报错退出，迁移终止。

|`target.mongodb.exist = drop`|
    |full.concurrency|全量同步阶段的表级别并发度，表示一次最多同步多少个表。默认值：4。|`full.concurrency = 4`|
    |full.document.concurrency|全量同步阶段参数。表内document的并发度，表示使用多少个线程并发将一个表内的内容写入目的端。默认值：4。|`full.document.concurrency = 4`|
    |full.document.parser|全量同步阶段参数。表内解析线程个数，表示使用多少个线程并发将Dynamo协议转换到目的端对应协议。默认值：2。|`full.document.parser = 2`|
    |full.enable\_index.user|全量同步阶段参数。是否同步用户自建的索引。取值：     -   true：是
    -   false：否
|`full.enable_index.user = true`|
    |full.executor.insert\_on\_dup\_update|全量同步阶段参数。在目的端碰到相同key的情况下，是否将`INSERT`操作改为`UPDATE`。取值：    -   true：是
    -   false：否
|`full.executor.insert_on_dup_update = true`|
    |increase.executor.insert\_on\_dup\_update|增量同步阶段参数。在目的端碰到相同key的情况下，是否将`INSERT`操作改为`UPDATE`。取值：    -   true：是
    -   false：否
|`increase.executor.insert_on_dup_update = true`|
    |increase.executor.upsert|增量同步阶段参数。如果目的端不存在key的情况下，是否将`UPDATE`操作改为`UPSERT`。取值：    -   true：是
    -   false：否
**说明：** `UPSERT`操作会判断目标key是否存在，如果存在则执行`UPDATE`操作，如果不存在则执行`INSERT`操作。

|`increase.executor.upsert = true`|
    |convert.type|增量同步阶段参数。是否对Dynamo协议进行转换。取值：     -   raw：不对Dynamo协议进行转换，直接写入。
    -   change：对Dynamo协议进行转换。如：将`{"hello":"1"}`转换为`{"hello": 1}`。
|`convert.type = change`|
    |increase.concurrency|增量同步阶段参数。一次最多并发抓取多少个分片（shard）。默认值：16。|`increase.concurrency = 16`|
    |checkpoint.type|断点续传（Checkpoint）位点信息的存储类型。取值：    -   mongodb：断点续传（Checkpoint）位点信息存储于MongoDB数据库中，仅在`target.type`参数为`mongodb`时可用。
    -   file：断点续传（Checkpoint）位点信息存储于本地计算机中。
|`checkpoint.type = mongodb`|
    |checkpoint.address|存储断点续传（Checkpoint）位点信息的地址。    -   `checkpoint.type`参数为`mongodb`：输入MongoDB数据库的连接地址。如不配置则默认存储到目的端的MongoDB库中。查看MongoDB的地址信息，请参见[副本集实例连接说明]()或[分片集群实例连接说明]()。
    -   `checkpoint.type`参数为`file`：输入以nimo-shake运行文件所在路径为基准的相对路径，如：checkpoint。如不配置则默认存储到checkpoint文件夹。
|`checkpoint.address = mongodb://username:password@s-*****-pub.mongodb.rds.aliyuncs.com:3717`|
    |checkpoint.db|存储断点续传（Checkpoint）位点信息的MongoDB数据库名，如不配置则数据库名的格式默认为`<任务ID>-checkpoint`，示例：nimoshake-checkpoint。|`checkpoint.db = nimoshake-checkpoint`|

6.  执行如下命令使用配置好的nimo-shake.conf文件启动迁移。

    ```
    ./nimo-shake.linux -conf=nimo-shake.conf
    ```

    **说明：** 全量同步完成后，屏幕上会打印出`full sync done!`。如果中途出错导致同步终止，程序会自动关闭并在屏幕上打印对应的错误信息，便于您定位错误原因。


