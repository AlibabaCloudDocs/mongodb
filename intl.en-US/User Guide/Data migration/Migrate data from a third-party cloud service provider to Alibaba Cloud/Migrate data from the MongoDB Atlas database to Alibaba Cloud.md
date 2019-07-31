# Migrate data from the MongoDB Atlas database to Alibaba Cloud {#concept_phx_ws5_jgb .concept}

You can use mongodump and mongorestore, the backup and restoration tools provided MongoDB, to migrate data from a MongoDB Atlas database to ApsaraDB for MongoDB.

## Precautions {#section_j3k_5sk_5fb .section}

-   ApsaraDB for MongoDB supports migration of several database versions. \(ApsaraDB for MongoDB supports MongoDB versions 3.2, 3.4 and 4.0.\)
-   The source database can be migrated to databases with different storage engines. \(ApsaraDB for MongoDB supports three storage engines: WiredTiger, RocksDB and TerarkDB.\)
-   This operation is full data migration. [Incremental data migration](https://help.aliyun.com/knowledge_detail/39252.html) is not supported. To avoid data inconsistency, stop writing data to the database before the migration starts.
-   The version of mongodump and mongorestore is the same as the version of the MongoDB Atlas database.
-   If you have backed up databases with mongodump, move the backup files in the dump folder to other directories. Make sure that the default dump folder is empty before data migration. Otherwise, the backup files in this folder will be overwritten.
-   Run the mongodump and mongorestore commands on servers that have MongoDB services. Do not run these commands in the mongo shell.

## Database account permission requirements {#section_oyv_j2l_5fb .section}

|Migration object|Account permission|
|:---------------|:-----------------|
|MongoDB Atlas instance|Read permissions|
|ApsaraDB for MongoDB instance|Read and write permissions|

## Premigration preparation 1 {#section_y4p_ztk_5fb .section}

1.  Create an ApsaraDB for MongoDB instance. For more information, see [Create a replica set instance](../../../../intl.en-US/Quick Start for Replica Set/Create an instance.md#) or [Create a sharded cluster instance](../../../../intl.en-US/Quick Start for Cluster/Create a sharded cluster instance.md#).

    **Note:** 

    -   The storage space of ApsaraDB for MongoDB instances must be greater than that of MongoDB Atlas.
    -   If you migrate data to a sharded cluster instance of ApsaraDB for MongoDB, we recommend that you shard the data. For more information, see [Configure sharding to maximize the performance of shards](../../../../intl.en-US/Best Practices/Configure sharding to maximize the performance of shards.md#).
2.  Set the password for the ApsaraDB for MongoDB database. For more information, see [Set a password](https://help.aliyun.com/document_detail/54956.html#task-xxj-svb-kfb).

## Premigration preparation 2 {#section_thc_nt5_jgb .section}

Install MongoDB on the local server. Ensure that the version number of the program is the same as that of the MongoDB Atlas database. This server is an intermediary that transfers the data during data migration. In this case, the MongoDB program is installed on the Linux server.

1.  Install the MongoDB program on the local server. For more information, see [Install MongoDB](https://docs.mongodb.com/manual/administration/install-community/).

    **Note:** 

    -   This server is used as the intermediary for data backup and recovery. You will not need it after the migration.
    -   The available storage space of the partition in which the backup directories reside must be greater than that of the MongoDB Atlas database.
2.  Add the public IP address of the local server to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](http://1).

## Migration procedure {#section_nf4_mby_ggb .section}

1.  Log on to the MongoDB Atlas console.
2.  Add the public IP address of the local server that is used for data migration to the whitelist of the MongoDB Atlas instance.

    ![Configuration of the MongoDB Atlas whitelist](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/91579/156455521936508_en-US.png)

3.  On the Clusters page, click Clusters.

    ![Clusters](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/91579/156455521936523_en-US.png)

4.  On the Command Line Tools tab, click **COPY** next to the mongodump command to copy the mongodump command that contains the connection information of the MongoDB Atlas database.

    ![Copy the mongodump command that contains the connection information.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/91579/156455521936524_en-US.png)

5.  Back up the MongoDB Atlas database on the local server.

    1.  On the local server, paste the mongodump command that contains connection information of the MongoDB Atlas database.
    2.  Replace <PASSWORD\> with the password of the root user, and replace <DATABASE\> with the name of the database to be backed up.
    3.  Run this command and wait until the data is backed up.
    Example:

    ![mongodump operation example](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/91579/156455522036534_en-US.png)

6.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com) to obtain the public connection address of the ApsaraDB for MongoDB instance.

    -   To migrate data to a replica set instance of ApsaraDB for MongoDB, obtain the public IP address of the primary node. For more information, see [Obtain the replica set instance connection information](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to an replica set instance through the mongo shell.md#).
    -   To migrate data to a sharded cluster instance of ApsaraDB for MongoDB, obtain the public IP address of any mongos. For more information, see [Connect to an ApsaraDB for MongoDB instance](../../../../intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance.md#).
    **Note:** You must apply for a public IP address. For more information, see [Apply for a public IP address](intl.en-US/User Guide/Network connection management/Apply for a public address.md#).

7.  On the local server, run the following command to import data to the ApsaraDB for MongoDB database:

    ``` {#codeblock_gzz_1vj_ey4}
    mongorestore --host <mongodb_host>:3717 --authenticationDatabase admin -u <username> -d <database> <database_backupfile_directory>
    ```

    **Note:** 

    -   <mongodb\_host\>: the connection address of the primary node in the ApsaraDB for MongoDB replica set instance, or the connection address of a mongos in the ApsaraDB for MongoDB sharded cluster instance.
    -   <username\>: the database username of the ApsaraDB for MongoDB instance.
    -   <database\>: the database to be restored. If multiple databases exist in the backup file, repeat this step to restore all the databases.
    -   <database\_backupfile\_directory\>: the directory of the database backup file.
    Example:

    Restore the mongodbtest database in the database backup file

    ``` {#codeblock_086_sfz_twi}
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -d mongodbtest /dump/mongodbtest
    ```

    Restore the test123 database in the database backup file

    ``` {#codeblock_5d7_aak_1jy}
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -d test123 /dump/test123
    ```

8.  In the `Enter password:` prompt, enter the password corresponding to the ApsaraDB for MongoDB database account.

Wait until data restoration is completed. The data in MongoDB Atlas is migrated to ApsaraDB for MongoDB.

