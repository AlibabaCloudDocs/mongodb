---
keyword: [quasi-real-time one-way synchronization of table data between instances, database synchronization, Alibaba Cloud database synchronization]
---

# Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica set instances

You can use the MongoShake tool developed by Alibaba Cloud to synchronize data between MongoDB databases. This tool can be used in scenarios such as data analysis, disaster recovery, and active-active replication. This topic uses the real-time data synchronization between ApsaraDB for MongoDB replica set instances as an example to describe how to configure MongoShake.

**Note:** If you want to implement two-way data synchronization between replica set instances, you can [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex).

## MongoShake overview

MongoShake is a general-purpose Platform as a Service \(PaaS\) tool developed by Alibaba Cloud with the Go language. MongoShake reads the oplogs of a MongoDB database and replicates data based on the oplogs to meet specific requirements.

MongoShake also allows you to subscribe to and consume MongoDB logs. You can connect to MongoShake by using multiple methods such as SDKs, Kafka, and MetaQ. MongoShake is suitable for scenarios such as log subscription, data synchronization across data centers, and asynchronous cache eviction.

**Note:** For more information about MongoShake, see [MongoShake homepage on GitHub](https://github.com/alibaba/MongoShake).

## Supported databases

|Source database|Destination database|
|:--------------|:-------------------|
|Self-managed MongoDB database hosted on Elastic Compute Service \(ECS\)|Self-managed MongoDB database hosted on ECS|
|Self-managed MongoDB database hosted on a local server|Self-managed MongoDB database hosted on a local server|
|ApsaraDB for MongoDB instance|ApsaraDB for MongoDB instance|
|MongoDB database on a third-party cloud|MongoDB database on a third-party cloud|

## Precautions

-   Do not perform data definition language \(DDL\) operations in the source database before full data synchronization is complete. Otherwise, data inconsistency may occur.
-   You cannot use MongoShake to synchronize data in the admin and local databases.

## Required permissions on databases

|Database|Required permission|
|:-------|:------------------|
|Source ApsaraDB for MongoDB instance|readAnyDatabase permissions, read permissions on the local database, and read/write permissions on the mongoshake database**Note:** The mongoshake database is created by MongoShake at the source when the incremental migration task starts. |
|Destination ApsaraDB for MongoDB instance|readWriteAnyDatabase or read/write permissions on the destination database|

**Note:** For more information about how to create and authorize MongoDB users, see [Use DMS to manage MongoDB users](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md) or [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/index.html).

## Preparations

1.  Create an ApsaraDB for MongoDB replica set instance as the synchronization destination. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md).

    **Note:** Create the destination ApsaraDB for MongoDB instance in the same virtual private cloud \(VPC\) as the source ApsaraDB for MongoDB instance. In this way, you can connect the Elastic Compute Service \(ECS\) instance where MongoShake runs to the source and destination ApsaraDB for MongoDB instances over the VPC.

2.  Create an ECS instance to run MongoShake. For more information, see [Create an ECS instance](https://www.alibabacloud.com/help/zh/doc-detail/25424.htm).

    **Note:** Set the operating system of the ECS instance to Linux and select the same VPC as that used by the source and destination ApsaraDB for MongoDB instances.

3.  Add the IP address of the ECS instance to the whitelists of the source and destination ApsaraDB for MongoDB instances. Make sure that the ECS instance can connect to the source and destination ApsaraDB for MongoDB instances.

    **Note:** We recommend that you connect to the source and destination ApsaraDB for MongoDB instances over a VPC to minimize network latency.


## Procedure

1.  Log on to the [ECS instance](https://www.alibabacloud.com/help/zh/doc-detail/25434.htm).
2.  Run the following command to download the MongoShake package:

    ```
    wget Download URL of the latest MongoShake package
    ```

    **Note:** We recommend that you download the latest MongoShake package. For more information, see [Releases](https://github.com/alibaba/MongoShake/releases).

3.  Run the following command to decompress the MongoShake package:

    ```
    tar xvf <Name of the MongoShake package>
    ```

4.  Use Vim to modify the collector.conf file of MongoShake. The following table describes the parameters that you must modify for synchronizing data between ApsaraDB for MongoDB instances.``

    |Section|Parameter|Description|Example|
    |-------|:--------|:----------|:------|
    |N/A|conf.version|The version number of the configuration file. Do not change the value.|`conf.version = 4`|
    |Global configuration options|id|The ID of the synchronization task. You can specify the ID as needed. The global configuration includes the log file name, the name of the database that stores the checkpoint information, and the name of the destination database.|`id = mongoshake`|
    |master\_quorum|Specifies whether the MongoShake node is the active node in high availability scenarios. If you use the active MongoShake node and standby MongoShake node to synchronize data from the same database, you must set this parameter to `true` for the active MongoShake node. Valid values:

    -   true
    -   false
**Note:** The default value is false.

|`master_quorum = false`|
    |full\_sync.http\_port|The HTTP port used to view the status of full data synchronization in MongoShake over the Internet.**Note:** The default value is 9101.

|`full_sync.http_port = 9101`|
    |incr\_sync.http\_port|The HTTP port used to view the status of incremental data synchronization in MongoShake over the Internet.**Note:** The default value is 9100.

|`incr_sync.http_port = 9100`|
    |system\_profile\_port|The profiling port used to view internal stack information.|`system_profile_port = 9200`|
    |log.level|The level of the logs to be generated. Valid values:     -   error: generates logs that contain error messages.
    -   warning: generates logs that contain warnings.
    -   info: generates logs that indicate system status.
    -   debug: logs that contain debugging information.
The default value is info.

|`log.level = info`|
    |log.dir|The directory where the log file and PID file are stored. If you do not specify a value, the log file and PID file are stored to the logs directory in the working directory.**Note:** The path here must be an absolute path.

|`log.dir = ./logs/`|
    |log.file|The name of the log file. You can specify the name as needed. **Note:** The default value is collector.log.

|`log.file = collector.log`|
    |log.flush|Specifies whether to display every log entry on the screen. Valid values:     -   true: displays every log entry on the screen. This ensures that no log entry is missing on the screen but deteriorates the performance.
    -   false: does not display every log entry on the screen. This ensures the performance but certain log entries may be missing on the screen.
**Note:** The default value is false.

|`log.flush = false`|
    |sync\_mode|The data synchronization method. Valid values:     -   all: performs both full data synchronization and incremental data synchronization.
    -   full: performs only full data synchronization.
    -   incr: performs only incremental data synchronization.
**Note:** The default value is full.

|`sync_mode = all`|
    |mongo\_urls|The connection string URI of the source instance. **Note:**

    -   We recommend that you use a VPC endpoint to minimize network latency.
    -   For more information about the format of a connection string URI, see [Overview of replica set instance connections]() or [Overview of sharded cluster instance connections]().
|`mongo_urls = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`|
    |mongo\_cs\_url|The endpoint of the ConfigServer node. Set this parameter if the source ApsaraDB for MongoDB instance is a sharded cluster instance. For more information about how to apply for an endpoint for the ConfigServer node, see [Apply for a connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Apply for a connection string of a shard or Configserver node.md).|`mongo_cs_url = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx-csxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx-csxxx.mongodb.rds.aliyuncs.com:3717/admin`|
    |mongo\_s\_url|The endpoint of the Mongos node. Set this parameter if the source ApsaraDB for MongoDB instance is a sharded cluster instance. You must specify the endpoint of at least one Mongos node. Separate the endpoints of multiple Mongos nodes with commas \(,\). For more information about how to apply for an endpoint for a Mongos node, see [Apply for a connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Apply for a connection string of a shard or Configserver node.md).|`mongos_s_url = mongodb://root:Ftxxxxxx@s-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,s-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717/admin`|
    |tunnel|The type of the tunnel used for synchronization. Valid values:     -   direct: directly synchronizes data to the destination ApsaraDB for MongoDB instance.
    -   rpc: synchronizes data by using NET/RPC.
    -   tcp: synchronizes data by using TCP.
    -   file: synchronizes data by transferring files.
    -   kafka: synchronizes data by using Kafka.
    -   mock: only used for testing without writing data to the tunnel.
**Note:** Th default value is direct.

|`tunnel = direct`|
    |tunnel.address|The address used to connect to the destination ApsaraDB for MongoDB instance through the tunnel.     -   If the tunnel parameter is set to `direct`, set the value to the connection string URI of the destination ApsaraDB for MongoDB instance.
    -   If the tunnel parameter is set to `rpc`, set the value to the receiver socket address used in the RPC connection to the destination ApsaraDB for MongoDB instance.
    -   If the tunnel parameter is set to `tcp`, set the value to the receiver socket address used in the TCP connection to the destination ApsaraDB for MongoDB instance.
    -   If the tunnel parameter is set to `file`, set the value to the file path in the destination ApsaraDB for MongoDB instance.
    -   If the tunnel parameter is set to `kafka`, set the value to the broker server addresses of Kafka. Example: `topic@brokers1,brokers2`.
    -   If the tunnel parameter is set to `mock`, you do not need to set this parameter.
|`tunnel.address = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`|
    |tunnel.message|The type the data to be written to the tunnel. This parameter only takes effect when the tunnel parameter is set to `kafka` or `file`. Valid values:     -   raw: writes data in the original format. The data is aggregated in batches to be written or read at a time.
    -   json: writes data to Kafka in the `JSON` format so that the data can be read directly.
    -   bson: writes data to Kafka in the Binary JSON \(`BSON`\) format.
**Note:** The default value is raw.

|`tunnel.message = raw`|
    |mongo\_connect\_mode|The type of the node from which MongoShake pulls data. This parameter only takes effect when the tunnel parameter is set to `direct`. Valid values:     -   primary: pulls data from the primary node.
    -   secondaryPreferred: pulls data from a secondary node.
    -   standalone: pulls data from the single node that is specified.
**Note:** The default value is secondaryPreferred.

|`mongo_connect_mode = secondaryPreferred`|
    |filter.namespace.black|The namespace blacklist for data synchronization. The specified namespaces are not synchronized to the destination database. Separate multiple namespaces with semicolons \(;\). **Note:** A namespace is the standard name of a collection or index in ApsaraDB for MongoDB. It is the combination of a database name and a collection or index name. Example: `mongodbtest.customer`.

|`filter.namespace.black = mongodbtest.customer;testdata.test123`|
    |filter.namespace.white|The whitelist for data synchronization. Only the specified namespaces are synchronized to the destination database. Separate multiple namespaces with semicolons \(;\).|`filter.namespace.white = mongodbtest.customer;test123`|
    |filter.pass.special.db|The special database from which you want to synchronize data to the destination database. You can specify multiple special databases. By default, the data in special databases, such as admin, local, mongoshake, config, and system.views, is not synchronized. You can set this parameter to synchronize data from special databases as needed. Separate multiple database names with semicolons \(;\).|`filter.pass.special.db = admin;mongoshake`|
    |filter.ddl\_enable|Specifies whether to synchronize DDL operations. Valid values:     -   true
    -   false
**Note:** Do not set this parameter to true if the source ApsaraDB for MongoDB instance is a sharded cluster instance.

|`filter.ddl_enable = false`|
    |checkpoint.storage.url|The storage location of checkpoints, which are used for resumable upload. If you do not set this parameter, MongoShake writes checkpoints to the following databases based on the type of the source ApsaraDB for MongoDB instance:     -   Replica set instance: MongoShake writes checkpoints to the mongoshake database.
    -   Sharded cluster instance: MongoShake writes checkpoints to the admin database on the ConfigServer node.
|`checkpoint.storage.url = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`|
    |checkpoint.storage.db|The name of the database that stores checkpoints. **Note:** The default value is mongoshake.

|`checkpoint.storage.db = mongoshake`|
    |checkpoint.storage.collection|The name of the collection that stores checkpoints. If you use the active MongoShake node and standby MongoShake node to synchronize data from the same database, you can change this collection name to avoid the conflict caused by duplicate collection names. **Note:** The default value is ckpt\_default.

|`checkpoint.storage.collection = ckpt_default`|
    |checkpoint.start\_position|The start position for resumable upload. If a checkpoint exists, this parameter is invalid. Set the value in the following format: `*YYYY*-*MM*-*DD*T*HH*:*MM*:*SS*Z`.**Note:** The default value is 1970-01-01T00:00:00Z.

|`checkpoint.start_position = 1970-01-01T00:00:00Z`|
    |transform.namespace|The rule for renaming the source database or collection in the destination database. For example, you change the database name and collection name from `Database A.Collection B` to `Database C.Collection D` in the destination database.|`transform.namespace = fromA.fromB:toC.toD`|
    |Full data synchronization options|full\_sync.reader.collection\_parallel|The maximum number of collections that can be concurrently pulled by MongoShake at a time.|`full_sync.reader.collection_parallel = 6`|
    |full\_sync.reader.write\_document\_parallel|The number of concurrent threads used by MongoShake to write a collection.|`full_sync.reader.write_document_parallel = 8`|
    |full\_sync.reader.document\_batch\_size|The number of documents to be written to the destination ApsaraDB for MongoDB instance at a time. For example, a value of 128 indicates that 128 documents are written to the destination ApsaraDB for MongoDB instance at a time.|`full_sync.reader.document_batch_size = 128`|
    |full\_sync.collection\_exist\_drop|Specifies whether to delete the collections in the destination database that have the same names as the source collections before synchronization. Valid values:     -   true: deletes the collections in the destination database that have the same names as the source collections before synchronization.

**Warning:** This option will delete collections in the destination database. Therefore, back up data in the destination database in advance.

    -   false: returns an error message and exits if a collection in the destination database has the same name as a source collection.
|`full_sync.collection_exist_drop = true`|
    |full\_sync.create\_index|Specifies whether to create indexes after the synchronization is complete. Valid values:     -   foreground: creates indexes in the foreground.
    -   background: creates indexes in the background.
    -   none: does not create indexes.
|`full_sync.create_index = none`|
    |full\_sync.executor.insert\_on\_dup\_update|Specifies whether to change an `INSERT` statement to an `UPDATE` statement if a document in the destination database has the same `_id` value as the source document. Valid values:     -   true
    -   false
|`full_sync.executor.insert_on_dup_update = false`|
    |full\_sync.executor.filter.orphan\_document|Specifies whether to filter out orphaned documents if the source ApsaraDB for MongoDB instance is a sharded cluster instance. Valid values:     -   true
    -   false
|`full_sync.executor.filter.orphan_document = false`|
    |full\_sync.executor.majority\_enable|Specifies whether to enable the majority write feature in the destination ApsaraDB for MongoDB instance. Valid values:     -   true
    -   false
|`full_sync.executor.majority_enable = false`|
    |Incremental data synchronization options|incr\_sync.mongo\_fetch\_method|The method used to pull incremental data. Valid values:     -   oplog: pulls oplogs from the source database.
    -   change\_stream: pulls change events from the source database. Only MongoDB 4.0 or later supports this method.
The default value is oplog.

|`incr_sync.mongo_fetch_method = oplog`|
    |incr\_sync.oplog.gids|The global ID used to implement two-way replication for ApsaraDB for MongoDB clusters. You can apply for global IDs by [submitting a ticket](https://workorder.console.aliyun.com/#/ticket/list).|`incr_sync.oplog.gids = xxxxxxxxxxxx`|
    |incr\_sync.shard\_key|The method used to distribute concurrent requests to internal worker threads. Do not modify this parameter.|`incr_sync.shard_key = collection`|
    |incr\_sync.worker|The number of concurrent threads that transmit oplogs. If the performance of your ECS instance is sufficient, you can increase the number of concurrent threads. **Note:** If the source ApsaraDB for MongoDB instance is a sharded cluster instance, the number of concurrent threads must be equal to the number of shard nodes.

|`incr_sync.worker = 8`|
    |incr\_sync.worker.oplog\_compressor|Specifies whether to decompress data to reduce network bandwidth usage. Valid values:     -   none: does not compress data.
    -   gzip: compresses data in the gzip format.
    -   zlib: compresses data in the zlib format.
    -   deflate: compresses data in the deflate format.
**Note:** This parameter only takes effect when the tunnel parameter is not set to `direct`. If the tunnel parameter is set to `direct`, set the value to `none`.

|`incr_sync.worker.oplog_compressor = none`|
    |incr\_sync.target\_delay|The time delayed for synchronizing data between the source and destination ApsaraDB for MongoDB instances. By default, changes in the source database are synchronized to the destination database in real time. To avoid misoperations, you can set this parameter to delay the synchronization. For example, if you set `incr_sync.target_delay = 1800`, the synchronization is delayed for 30 minutes. Unit: seconds. **Note:** A value of 0 indicates that data is synchronized in real time.

|`incr_sync.target_delay = 1800`|
    |incr\_sync.worker.batch\_queue\_size|The parameters for configuring internal queues in MongoShake. Do not modify these parameters unless otherwise required.|`incr_sync.worker.batch_queue_size = 64`|
    |incr\_sync.adaptive.batching\_max\_size|`incr_sync.adaptive.batching_max_size = 1024`|
    |incr\_sync.fetcher.buffer\_capacity|`incr_sync.fetcher.buffer_capacity = 256`|
    |Direct tunnel options \(This section only takes effect when the tunnel parameter is set to `direct`.\)|incr\_sync.executor.upsert|Specifies whether to change an `UPDATE` statement to an `INSERT` statement if no document in the destination database has the same `_id` value or unique index as the source document. Valid values:     -   true
    -   false
|`incr_sync.executor.upsert = false`|
    |incr\_sync.executor.insert\_on\_dup\_update|Specifies whether to change an `INSERT` statement to an `UPDATE` statement if a document in the destination database has the same `_id` value or unique index as the source document. Valid values:     -   true
    -   false
|`incr_sync.executor.insert_on_dup_update = false`|
    |incr\_sync.conflict\_write\_to|Specifies whether to record conflicting documents if data write conflicts occur during the synchronization. Valid values:     -   none: does not record conflict documents.
    -   db: writes conflict logs to the mongoshake\_conflict database.
    -   sdk: writes conflict logs to SDK.
|`incr_sync.conflict_write_to = none`|
    |incr\_sync.executor.majority\_enable|Specifies whether to enable the majority write feature in the destination ApsaraDB for MongoDB instance. Valid values:     -   true
    -   false
**Note:** The majority write feature deteriorates the performance.

|`incr_sync.executor.majority_enable = false`|

5.  Run the following command to start the data synchronization task and generate the log information:

    ```
    ./collector.linux -conf=collector.conf -verbose
    ```

6.  Check the log information. If the following log is displayed, it indicates that the full data synchronization is complete and the incremental data synchronization starts.

    ```
    [09:38:57 CST 2019/06/20] [INFO] (mongoshake/collector.( *ReplicationCoordinator).Run:80) finish full sync, start incr sync with timestamp: fullBeginTs[1560994443], fullFinishTs[1560994737]
    ```


## Monitor the MongoShake status

When the incremental data synchronization starts, you can open a command line window to monitor MongoShake.

```
./mongoshake-stat --port=9100
```

The following figure shows sample monitoring information about MongoShake.

![Monitoring output](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1635298951/p49777.png)

|Parameter|Description|
|---------|-----------|
|logs\_get/sec|The number of oplogs obtained per second.|
|logs\_repl/sec|The number of oplogs for replay operations performed per second.|
|logs\_success/sec|The number of oplogs for successful replay operations per second.|
|lsn.time|The time when the last oplog was sent.|
|lsn\_ack.time|The time when the destination database acknowledges the write operation.|
|lsn\_ckpt.time|The time when the last checkpoint was generated.|
|now.time|The current time.|
|replset|The name of the replica set instance where the source database resides.|

