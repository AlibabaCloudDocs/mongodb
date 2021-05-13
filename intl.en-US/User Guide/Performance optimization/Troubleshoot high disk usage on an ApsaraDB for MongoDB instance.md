# Troubleshoot high disk usage on an ApsaraDB for MongoDB instance

Disk usage is a key metric to monitor an ApsaraDB for MongoDB instance. If the disk usage on an instance reaches 100%, the instance becomes unavailable. This topic describes how to view the details of disk usage and troubleshoot the high disk usage on an instance.

If the disk usage on an instance exceeds the range of 80% to 85%, you can reduce the storage usage of databases or expand the storage space to prevent the disk usage from reaching 100%.

## View disk usage

-   Replica set instances

    You can use the following methods to view the disk usage on a replica set instance in the ApsaraDB for MongoDB console:

    -   Overview

        On the **Basic Information** page of the replica set instance in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), view the disk usage on the replica set instance.

    -   Detail analysis by using monitoring charts

        On the **Monitoring Info** page of the replica set instance in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), select a node and view the disk usage on the node in monitoring charts.

        **Note:** A replica set instance consists of a primary node that supports read and write operations, one or more high-availability secondary nodes, a hidden node, and one or more optional read-only nodes. Disk usage on a node consists of disk space used by data and logs. Formula: ins\_size = data\_size + log\_size. The following list describes the parameters in this formula:

        -   data\_size indicates the disk space used by data files such as physical data files whose names start with collection, physical index files whose names start with index, and some physical metadata files such as WiredTiger.wt. The data files exclude the local database.
        -   log\_size indicates the disk space used by the local database, runtime logs, and some audit logs.
    -   Detail analysis

        You can use the following methods to view the details of disk usage:

        -   Run the `db.stats()` and `db.$collection_name.stats()` commands provided by MongoDB.

            For more information, visit the following links:

            -   [https://docs.mongodb.com/manual/reference/method/db.stats/](https://docs.mongodb.com/manual/reference/method/db.stats/)
            -   [https://docs.mongodb.com/manual/reference/method/db.collection.stats/](https://docs.mongodb.com/manual/reference/method/db.collection.stats/)
            -   [https://docs.mongodb.com/manual/reference/method/db.collection.storageSize/](https://docs.mongodb.com/manual/reference/method/db.collection.storageSize/)
            -   [https://docs.mongodb.com/manual/reference/method/db.collection.totalIndexSize/](https://docs.mongodb.com/manual/reference/method/db.collection.totalIndexSize/)
            -   [https://docs.mongodb.com/manual/reference/method/db.collection.totalSize/](https://docs.mongodb.com/manual/reference/method/db.collection.totalSize/)
        -   Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Find the instance that you want to view and click the instance ID. In the left-side navigation pane, choose **CloudDBA** \> **Capacity analysis**.

            **Note:** On the page that appears, you can view the following items. For more information, see [t1846264.dita\#task\_2350359](/intl.en-US/User Guide/CloudDBA for performance diagnostics and optimization/Capacity analysis.md).

            -   Overview of the disk usage of databases and tables, average daily increment, and predicted available days of storage
            -   Disk usage of abnormal databases and tables
            -   Details about the disk usage on a specific business table, including the disk space used by index files and data files, compression ratio, and average row size
-   Sharded cluster instances

    You can use the following methods to view the disk usage on a sharded cluster instance in the ApsaraDB for MongoDB console:

    -   Detail analysis by using monitoring charts

        On the **Monitoring Info** page of the sharded cluster instance in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), select a node and view the disk usage on the node in monitoring charts.

    -   Detail analysis by running commands

        Run the `db.stats()` and `db.$collection_name.stats()` commands that are provided by MongoDB to analyze the disk usage on each node of the sharded cluster instance.


## Troubleshoot large data volume caused by the compact command

-   compact command and its effect on an instance

    The execution duration of the compact command is related to the data volume of a collection. If the data volume is large, the compact command runs for a long period of time. Therefore, we recommend that you run the compact command during off-peak hours. The compact operation is easy to perform. Run the `db.runCommand({compact:"collectionName"})` command on the secondary database and perform primary/secondary switchover to minimize the effect on your business.

    **Note:**

    -   Replace the collectionName parameter value with your actual collection name.
    -   In versions later than MongoDB 4.4, the compact command does not block business data reads or writes. For more information about the usage and limits of the compact command, visit [https://docs.mongodb.com/manual/reference/command/compact/](https://docs.mongodb.com/manual/reference/command/compact/), [https://mongoing.com/archives/26907](https://mongoing.com/archives/26907), and [t61599.dita\#concept\_ngj\_sxl\_sfb](/intl.en-US/Best Practices/Performance/Defragment a disk to improve disk usage.md).
-   Invalid compact operation

    After you run the compact command, new space is not immediately created to store existing data. Instead, existing data is continuously moved forward into free space. However, the free space may not be reused to store existing data. The following list describes scenarios and solutions:

    -   The system prompts you that the compact operation is successful after you run the compact command. However, the existing free space cannot be used. In this case, we recommend that you create another replica.
    -   In versions earlier than MongoDB 3.4, the compact operation takes effect only on data files but not on index files after large amounts of data is deleted. In this case, we recommend that you upgrade the version of the database engine to 3.4 or later. To determine whether the compact operation takes effect on index files, perform one of the following operations:
        1.  Run the `db.$table_name.stats().indexSizes` command.
        2.  View the size of physical index files.

## Troubleshoot high space usage caused by large amounts of log data

-   The gap between the spaces used by the primary and secondary nodes is large due to large amounts of journal logs.

    In versions earlier than MongoDB 4.0, if the size of open files on the host reaches the specified upper limit, the cleaner threads on the MongoDB log server are terminated. As a result, journal logs infinitely increase in size. If content that is similar to the following code block appears in the runtime logs of an instance, you can temporarily solve the problem by upgrading the version of MongoDB to 4.0 or later or by restarting the mongod process. For more information, visit [https://jira.mongodb.org/browse/WT-4083](https://jira.mongodb.org/browse/WT-4083).

    ```
    2019-08-25T09:45:16.867+0800 I NETWORK [thread1] Listener: accept() returns -1 Too many open files in system 
    2019-08-25T09:45:17.000+0800 I - [ftdc] Assertion: 13538:couldn't open [/proc/55692/stat] Too many open files in system src/mongo/util/processinfo_linux.cpp 74
    2019-08-25T09:45:17.002+0800 W FTDC [ftdc] Uncaught exception in 'Location13538: couldn't open [/proc/55692/stat] Too many open files in system' in full-time diagnostic data capture subsystem. Shutting down the full-time diagnostic data capture subsystem.
    ```

-   Used log space of secondary nodes may continuously increase in size due to latency on the secondary nodes and incremental backup.

    If latency occurs in synchronization between primary and secondary nodes, the available space of oplogs is not limited by the fixed collection size defined in the configuration file. In theory, the available space can reach 20% of the disk space for which you apply. However, after the latency on the secondary nodes has elapsed, the physical space used by oplogs is not released.

    When you perform physical backups of an instance on a hidden node, a large number of checkpoints generate large volumes of data and occupy large log space.

    To solve the issues in the preceding scenarios, perform the compact operation on oplogs as shown in the following code.

    **Note:** All write operations are blocked during the compact operation.

    ```
    db.grantRolesToUser("root", [{db: "local", role: "dbAdmin"}])
    use local
    db.runCommand({ compact: "oplog.rs", force: true  })
    ```


## Troubleshoot uneven data distribution caused by unreasonable sharding

-   Data is unevenly distributed due to unreasonable selection of sharding key types.

    In a sharded cluster instance, an appropriate sharding key is critical. In most cases, hashed sharding or ranged sharding is used. Hashed sharding is much better than ranged sharding for disk load balancing. Hashed sharding uses built-in hash functions to evenly distribute data among shards based on various key values. Ranged sharding distributes data based on ranges of key values, which results in uneven data distribution among shards. Data is distributed on a populated chunk. This may lead to high I/O workloads and short-term uneven data distribution in the disk where the chunk is located.

    As shown in the preceding figure, all data is written to the shard where Chunk C is located. After the storage space of Chunk C is exhausted, a new chunk is split in this shard. Then, the chunk is migrated by the MongoDB balancer, which consumes a considerable amount of time and I/O resources. In a scenario in which high-concurrency data requires to be written, the speed of data load balancing may not keep up with the speed of data writing. This results in uneven data distribution among shards. In this scenario, we recommend that you do not use ranged sharding.

    For more information about sharding key types, visit [https://docs.mongodb.com/manual/core/sharding-shard-key/](https://docs.mongodb.com/manual/core/sharding-shard-key/), [https://docs.mongodb.com/manual/core/hashed-sharding/](https://docs.mongodb.com/manual/core/hashed-sharding/), and [https://docs.mongodb.com/manual/core/ranged-sharding/](https://docs.mongodb.com/manual/core/ranged-sharding/).

-   Data is unevenly distributed due to unreasonable selection of sharding key fields.

    The number of chunks on each shard is essentially the same. However, most data is stored only in several populated chunks, which results in uneven data distribution. To view the runtime logs of an instance, run the `sh.status()` command. Alert information may be displayed in the output. The following code provides an example of alert information:

    ```
    2019-08-27T13:31:22.076+0800 W SHARDING [conn12681919] possible low cardinality key detected in superHotItemPool.haodanku_all - key is { batch: "201908260000" } 
    2019-08-27T13:31:22.076+0800 W SHARDING [conn12681919] possible low cardinality key detected in superHotItemPool.haodanku_all - key is { batch: "201908260200" } 
    2019-08-27T13:31:22.076+0800 W SHARDING [conn12681919] possible low cardinality key detected in superHotItemPool.haodanku_all - key is { batch: "201908260230" }
    ```

    The MongoDB balancer monitors the number of chunks on each shard regardless of the data volume. In this case, the number of chunks on each shard is balanced, whereas the data may be severely skewed. In a chunk, sharding keys are almost the same. When the chunk size reaches 64 MB, an empty chunk is split. This way, the number of chunks increases and chunk migration is complete. However, migrated chunks are empty chunks. As a result, shards may have an equal number of chunks but have largely different data sizes. In this case, you must redesign sharding keys by using appropriate columns that have a high degree of discrimination. For more information about chunk splitting, visit [https://docs.mongodb.com/manual/core/sharding-data-partitioning/](https://docs.mongodb.com/manual/core/sharding-data-partitioning/) and [https://docs.mongodb.com/manual/tutorial/split-chunks-in-sharded-cluster/](https://docs.mongodb.com/manual/tutorial/split-chunks-in-sharded-cluster/).

-   Jumbo shards arise from unsharded databases.

    An ApsaraDB for MongoDB instance allows only some databases to be sharded. This way, data in an unsharded database is stored in the same shard. If large volumes of data is stored in the database, the data volume in the populated shard is much larger than that in other shards.

    In another case, when data is logically imported from a source ApsaraDB for MongoDB instance to a destination ApsaraDB for MongoDB instance, the destination ApsaraDB for MongoDB instance may not be sharded.

    To resolve the issues in the preceding scenarios, we recommend that you perform the following operations:

    -   If the destination instance is not sharded by default, configure a sharding policy for the destination instance before you import data.
    -   If the number of unsharded databases is large and their data volumes are similar, run the `movePriamy` command provided by MongoDB to migrate specific databases to specific shards.
    -   If a database has a super large amount of data and is not sharded, we recommend that you shard the database or split the database as an individual replica set.
    -   If disk space is sufficient, we recommend that you ignore these issues.
-   Uneven disk usage is caused by multiple movechunk operations.

    The movechunk operation is used to remove the source data after data is written to destination shards. By default, the remove operation does not release space. Each table has data files and index files in an instance that runs the wiredTiger engine. If the files are not deleted, the occupied space is not released. In most cases, this issue occurs because sharding is implemented in an instance after the instance runs for a period of time.

    In theory, the space fragmentation caused by the movechunk operation is similar to the one caused by the operation in which large volumes of data is deleted. Therefore, if a large number of movechunk or remove operations are required on a shard, you can perform the compact operation on the shard to release the space used by fragments.

    For more information about movechunk, visit [https://docs.mongodb.com/manual/tutorial/migrate-chunks-in-sharded-cluster/](https://docs.mongodb.com/manual/tutorial/migrate-chunks-in-sharded-cluster/) and [https://docs.mongodb.com/manual/tutorial/manage-sharded-cluster-balancer/](https://docs.mongodb.com/manual/tutorial/manage-sharded-cluster-balancer/).


