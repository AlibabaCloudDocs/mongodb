# Migrate an Amazon DynamoDB database to ApsaraDB for MongoDB by using NimoShake

NimoShake, also known as DynamoShake, is a data synchronization tool developed by Alibaba Cloud. You can use this tool to migrate an Amazon DynamoDB database to ApsaraDB for MongoDB.

An ApsaraDB for MongoDB instance is created. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md) or [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md).

This topic describes how to use NimoShake.

NimoShake is used to migrate data from an Amazon DynamoDB database. The destination must be an ApsaraDB for MongoDB instance.For more information, see [NimoShake overview](https://github.com/alibaba/NimoShake).

## Precautions

Resources of the source and destination databases are occupied during full data migration. This may increase the load of the database servers. If you attempt to migrate a large volume of data or if the server specifications are insufficient, the databases may be overloaded or become unavailable. Before you migrate data, evaluate the performance of the source and destination databases. We recommend that you migrate data during off-peak hours.

## Terms

-   Resumable upload: In a resumable upload task, data is split into multiple chunks. When transmission is interrupted due to network failures or other causes, the task can be resumed from where it was left off rather than restarting from the beginning.

    **Note:** Resumable upload is supported in incremental migration, but not in full migration. If an incremental migration task is interrupted due to disconnection and the connection is recovered within a short time range, the task can be resumed. In some cases such as a long-period disconnection or the loss of a previous checkpoint, a full migration may be triggered.

-   Checkpoint: Resumable upload is based on checkpoints. Default checkpoints are written to the ApsaraDB for MongoDB database named dynamo-shake-checkpoint. Each collection records a checkpoint list and the status\_table collection records whether the current task is a full or incremental migration.

## NimoShake features

NimoShake performs full migration the first time and then incremental migration.

-   Full migration: contains data migration and index migration. The following figure shows the basic architecture of full migration.

    ![Full migration architecture](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9535298951/p128818.png)

    -   Data migration: NimoShake uses multiple concurrent threads to pull source data, as shown in the following figure.

        ![Data migration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9535298951/p128828.png)

        |Thread|Description|
        |------|-----------|
        |Fecher|Calls the protocol conversion driver provided by Amazon to capture data in the source collection in batches and then place the batches into queues until all source data is captured. **Note:** Only one fetcher thread is provided. |
        |Parser|Reads data from queues and parses data into the BSON structure. After data is parsed, the parser thread writes data to queues of the executor thread as entries. Multiple parser threads can be started and the default value is 2. You can specify the number of parser threads through the `FullDocumentParser` parameter.|
        |Executor|Pulls data from queues and then aggregates and writes data to the ApsaraDB for MongoDB database. Up to 16 MB data in 1,024 entries can be aggregated. Multiple executor threads can be started and the default value is 4. You can specify the number of executor threads through the `FullDocumentConcurrency` parameter.|

    -   Index migration: NimoShake writes indexes after data migration is complete. Indexes include self-contained indexes and user-created indexes.
        -   Self-contained indexes: If you have both a partition key and a sort key, NimoShake creates a unique composite index and writes the index to the ApsaraDB for MongoDB database. NimoShake also creates a hash index for the partition key and writes the index to the ApsaraDB for MongoDB database. If you have only a partition key, NimoShake writes a hash index and a unique index to the ApsaraDB for MongoDB database.
        -   User-created indexes: If you have a user-created index, NimoShake creates a hash index based on the primary key and writes the index to the ApsaraDB for MongoDB database.
-   Incremental migration: NimoShake migrates data but not the generated indexes. The following figure shows the basic architecture of incremental migration.

    ![Incremental migration architecture](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9535298951/p128843.png)

    |Thread|Description|
    |------|-----------|
    |Fetcher|Senses the changes of shards in a stream.|
    |Manager|Sends messages or creates a dispatcher to process messages. One shard corresponds to one dispatcher.|
    |Dispatcher|Pulls incremental data from the source. In resumable upload, data is pulled from the last checkpoint instead of the very beginning.|
    |Batcher|Parses and encapsulates the incremental data pulled from the dispatcher thread.|
    |Executor|Writes the encapsulated data to the ApsaraDB for MongoDB database and updates the checkpoint.|


## Migrate an Amazon DynamoDB database to ApsaraDB for MongoDB

This section uses Ubuntu to describe how to use NimoShake to migrate an Amazon DynamoDB database to ApsaraDB for MongoDB.

1.  Run the following command to download the NimoShake package and wait until the package is downloaded:

    ```
    wget https://github.com/alibaba/NimoShake/releases/download/release-v1.0.0-20191015/nimo.tar.gz
    ```

    **Note:** We recommend that you download the latest NimoShake package. For more information about the download address, visit [NimoShake](https://github.com/alibaba/NimoShake/releases).

2.  Run the following command to decompress the NimoShake package:

    ```
    tar zxvf nimo.tar.gz
    ```

3.  After decompression, run the `cd nimo` command to access the nimo folder.

4.  Run the `vi nimo-shake.conf` command to open the NimoShake configuration file.

5.  Configure the following parameters for NimoShake.

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |id|The ID of the migration task, which is custom. The ID is used to display pid files and other information, such as the log name of the migration task, the name of the database that stores checkpoint information, and the name of the destination database.|`id = nimo-shake`|
    |log.file|The path of the log file. If you do not configure this parameter, logs are displayed in stdout.|`log.file = nimo-shake.log`|
    |log.level|The severity of logs. Valid values:     -   none: No logs are collected.
    -   error: logs that contain error information.
    -   warn: logs that contain warning information.
    -   info: logs that contain system status information.
    -   debug: logs that contain debugging information.
Default value: info.

|`log.level = info`|
    |log.buffer|Specifies whether to enable log buffering. Valid values:     -   true. Log buffering ensures high performance. However, several latest log entries may be lost when you disable log buffering.
    -   false. If log buffering is disabled, performance is low, but all log entries are displayed.
Default value: true.

|`log.buffer = true`|
    |system\_profile|The pprof port. It is used for debugging and displaying stackful coroutine information.|`system_profile = 9330`|
    |http\_profile|The HTTP port. After this port is enabled, you can view the current status of NimoShake over the Internet.|`http_profile = 9340`|
    |sync\_mode|The type of data migration. Valid values:     -   all: both full and incremental migration.
    -   full: only full migration.
    -   incr: only incremental migration.
Default value: all.

**Note:** Both full and incremental migration is performed by default. If you only want to perform either full migration or incremental migration, change the value to full or incr.

|`sync_mode = all`|
    |source.access\_key\_id|The AccessKey ID used to access Amazon DynamoDB.|`source.access_key_id = xxxxxxxxxxx`|
    |source.secret\_access\_key|The AccessKey secret used to access Amazon DynamoDB.|`source.secret_access_key = xxxxxxxxxx`|
    |source.session\_token|The temporary key used to access Amazon DynamoDB. If no temporary key is available, you can skip this parameter.|`source.session_token = xxxxxxxxxx`|
    |source.region|The region where the Amazon DynamoDB database is located. If no region is available, you can skip this parameter.|`source.region = us-east-2`|
    |source.session.max\_retries|The maximum number of retries after a session failure.|`source.session.max_retries = 3`|
    |source.session.timeout|The session timeout. 0 indicates that the session timeout is disabled. Unit: milliseconds.|`source.session.timeout = 3000`|
    |filter.collection.white|The names of collections to be migrated. For example, `filter.collection.white = c1;c2` indicates that the c1 and c2 collections will be migrated and the rest collections will be filtered out. **Note:** You cannot specify both the filter.collection.white and filter.collection.black parameters. Otherwise, all collections will be migrated.

|`filter.collection.white = c1;c2`|
    |filter.collection.black|The names of collections to be filtered out. For example, `filter.collection.black = c1;c2` indicates that the c1 and c2 collections will be filtered out and the rest collections will be migrated. **Note:** You cannot specify both the filter.collection.white and filter.collection.black parameters. Otherwise, all collections will be migrated.

|`filter.collection.black = c1;c2`|
    |qps.full|The maximum number of the `scan` commands to be called per second in full migration. It is used to limit the frequency of the `scan` command. Default value: 1000.|`qps.full = 1000`|
    |qps.full.batch\_num|The number of data entries pulled per second in full migration. Default value: 128.|`qps.full.batch_num = 128`|
    |qps.incr|The maximum number of the `GetRecords` commands to be called per second in incremental migration. It is used to limit the frequency of the `GetRecords` command. Default value: 1000.|`qps.incr = 1000`|
    |qps.incr.batch\_num|The number of data entries pulled per second in incremental migration. Default value: 128.|`qps.incr.batch_num = 128`|
    |target.type|The category of the destination database. Valid values:    -   mongodb: an ApsaraDB for MongoDB instance.
    -   aliyun\_dynamo\_proxy: an ApsaraDB for MongoDB instance that is compatible with the DynamoDB protocol.
**Note:** The aliyun\_dynamo\_proxy option is only available at the China site \(aliyun.com\).

|`target.type = mongodb`|
    |target.mongodb.type|The category of the destination ApsaraDB for MongoDB instance. Valid values:     -   replica: the replica set instance.
    -   sharding: the sharded cluster instance.
|`target.mongodb.type = sharding`|
    |target.address|The connection string of the destination ApsaraDB for MongoDB instance. The destination must be an ApsaraDB for MongoDB instance or an ApsaraDB for MongoDB instance that is compatible with the DynamoDB protocol.For more information about ApsaraDB for MongoDB connection string URIs, see [Overview of replica set instance connections]() or [Overview of sharded cluster instance connections]().

**Note:** ApsaraDB for MongoDB instances that are compatible with the DynamoDB protocol are only available at the China site \(aliyun.com\).

|`target.address = mongodb://username:password@s-*****-pub.mongodb.rds.aliyuncs.com:3717`|
    |target.db.exist|Specifies how to handle a second collection with the same name on the destination. Valid values:     -   rename: NimoShake will rename a second collection with the same name and add a timestamp suffix to the name. For example, NimoShake changes c1 to c1.2019-07-01Z12:10:11.

Warning:

This operation modifies the names of destination collections and may affect the business. You must make preparations before data migration.

    -   drop: NimoShake will delete a second collection with the same name.
If this parameter is not specified and the destination already contains a collection with the same name, the migration task is terminated and an error message is returned.

|`target.mongodb.exist = drop`|
    |full.concurrency|The maximum number of collections that can be migrated concurrently in full migration. Default value: 4.|`full.concurrency = 4`|
    |full.document.concurrency|A parameter for full migration. It specifies the maximum number of threads used concurrently to write documents in a collection to the destination. Default value: 4.|`full.document.concurrency = 4`|
    |full.document.parser|A parameter for full migration. It specifies the maximum number of parser threads used concurrently to convert the Dynamo protocol to the corresponding protocol on the destination. Default value: 2.|`full.document.parser = 2`|
    |full.enable\_index.user|A parameter for full migration. It specifies whether to migrate user-created indexes. Valid values:     -   true
    -   false
|`full.enable_index.user = true`|
    |full.executor.insert\_on\_dup\_update|A parameter for full migration. Specifies whether to change the `INSERT` statement to the `UPDATE` statement if the same keys occur at the destination. Valid values:    -   true
    -   false
|`full.executor.insert_on_dup_update = true`|
    |increase.executor.insert\_on\_dup\_update|A parameter for incremental migration. Specifies whether to change the `INSERT` statement to the `UPDATE` statement if the same keys occur at the destination. Valid values:    -   true
    -   false
|`increase.executor.insert_on_dup_update = true`|
    |increase.executor.upsert|A parameter for incremental migration. Specifies whether to change the `UPDATE` statement to the `UPSERT` statement if no key is provided at the destination. Valid values:    -   true
    -   false
**Note:** The `UPSERT` statement checks whether the target key exists. If yes, the `UPDATE` statement is executed. If not, the `INSERT` statement is executed.

|`increase.executor.upsert = true`|
    |convert.type|A parameter for incremental migration. It specifies whether to convert the Dynamo protocol. Valid values:     -   raw: writes data directly without conversion of the Dynamo protocol.
    -   change: converts the Dynamo protocol. For example, NimoShake converts `{"hello":"1"}` to `{"hello": 1}`.
|`convert.type = change`|
    |increase.concurrency|A parameter for incremental migration. It specifies the maximum number of shards that can be captured concurrently. Default value: 16.|`increase.concurrency = 16`|
    |checkpoint.type|The type of the storage that stores checkpoint information. Valid values:    -   mongodb: Checkpoint information is store in the ApsaraDB for MongoDB database. Only when the `target.type` parameter is set to `mongodb`, the checkpoint.address and checkpoint.db parameters are valid.
    -   file: Checkpoint information is store in the local computer.
|`checkpoint.type = mongodb`|
    |checkpoint.address|The address used to store checkpoint information.    -   If the `checkpoint.type` parameter is set to `mongodb`, enter the connection string URI of the ApsaraDB for MongoDB database. If you do not specify this parameter, checkpoint information is stored in the destination ApsaraDB for MongoDB database. For more information about ApsaraDB for MongoDB connection string URIs, see [Overview of replica set instance connections]() or [Overview of sharded cluster instance connections]().
    -   If the `checkpoint.type` parameter is set to `file`, enter a relative path based on the path of the NimoShake file. Example: checkpoint. If you do not specify this parameter, checkpoint information is stored in checkpoint folder.
|`checkpoint.address = mongodb://username:password@s-*****-pub.mongodb.rds.aliyuncs.com:3717`|
    |checkpoint.db|The name of the ApsaraDB for MongoDB database that stores checkpoint information. If you do not specify this parameter, the database name is in the default format of `<Task ID>-checkpoint`. Example: nimoshake-checkpoint.|`checkpoint.db = nimoshake-checkpoint`|

6.  Run the following command to start data migration by using the configured nimo-shake.conf file:

    ```
    ./nimo-shake.linux -conf=nimo-shake.conf
    ```

    **Note:** After the full migration is complete, `full sync done!` is displayed on the screen. If the migration is terminated due to an error, NimoShake automatically stops and the corresponding error message is displayed on the screen for you to troubleshoot the error.


