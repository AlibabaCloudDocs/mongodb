# Migrate user-created standalone MongoDB databases to ApsaraDB for MongoDB through DTS {#concept_rcw_511_kfb .concept}

This topic describes how to use Data Transmission Service \(DTS\) to migrate data from user-created MongoDB databases to ApsaraDB for MongoDB. DTS supports full data migration and incremental data migration. You can use incremental data migration to migrate data seamlessly to ApsaraDB for MongoDB without any service interruptions.

## Prerequisites {#section_tql_qpw_pgb .section}

-   The service port of the user-created MongoDB instance is open to the public network.
-   The database version of the source database must be 3.0, 3.2, 3.4 or 3.6. MongoDB 4.0 is not supported. For more information about data migration in MongoDB 4.0, see [Migrate user-created databases to Alibaba Cloud through tools provided by MongoDB](intl.en-US/Quick Start for Standalone/Data migration/Migrate user-created databases to Alibaba Cloud through tools provided by MongoDB.md#).
-   The storage space of the ApsaraDB for MongoDB instance must be larger than the storage space of the user-created MongoDB instance.

## Notes {#section_a3z_x11_kfb .section}

-   Data in the admin database cannot be migrated even if it is selected.
-   The config database is an internal database. We recommend that you do not migrate data from the config database unless otherwise specified.
-   For user-created standalone MongoDB instances, you must first enable oplog to use DTS incremental data migration. For more details, see [Preparations before incremental data migration](#section_vqd_r51_dhb).
-   We recommend that you migrate your data during off-peak hours to avoid business interruptions.

## Billing information {#section_m3c_t5f_cgb .section}

|Migration type|Configuration fee|Public network traffic fee|
|:-------------|:----------------|:-------------------------|
|Full data migration|Not billed|Not billed|
|Incremental data migration|Billed. For more information, see [Data Transmission Service pricing](https://www.alibabacloud.com/product/data-transmission-service/pricing).|Not billed|

## Migration type description {#section_zjf_5fs_zfb .section}

-   Full data migration: All data from the user-created MongoDB database is migrated to the destination instance.
    -   Migrates databases.
    -   Migrates collections.
    -   Migrates indexes.
-   Incremental data migration: The incrementally updated data of the user-created database is synchronized to the database in the destination instance on the basis of full data migration.
    -   Synchronizes the create and delete operations on databases.
    -   Synchronizes the create, delete, and update operations on documents.
    -   Synchronizes the create and delete operations on collections.
    -   Synchronizes the create and delete operations on indexes.

## Migration permission requirements {#section_kvw_kb1_kfb .section}

If you use DTS to migrate MongoDB databases, you need different permissions when performing different types of migration. The details are as follows:

|Source database|Full data migration|Incremental data migration|
|:--------------|:------------------|--------------------------|
|User-created MongoDB database|Read permissions| -   Read permissions on the source database
-   Read permissions on the admin database
-   Read permissions on the local database

 |
|ApsaraDB for MongoDB|Read and write permissions|Read and write permissions|

**Note:** For more information about how to create and authorize a MongoDB account, see [db.createUser](https://docs.mongodb.com/manual/reference/method/db.createUser/) in the official MongoDB documentation.

## Preparations before incremental data migration {#section_vqd_r51_dhb .section}

To use DTS for incremental data migration, you must first enable oplog for the source database. The following section describes how to enable oplog for user-created MongoDB databases. Skip this step if you only perform full data migration.

**Note:** This operation requires the MongoDB service to be restarted, which will affect database access. We recommend that you perform this operation during off-peak hours.

1.  You can use the mongo shell to log on to the user-created MongoDB server. You must run the following commands to stop the MongoDB service of the user-created database.

    ``` {#codeblock_gjn_87j_h9x}
    use admin
    db.shutdownServer()
    ```

2.  Run the following command to start the MongoDB service from the back end as a replica set:

    ``` {#codeblock_fxa_h5r_lh9}
    mongod --port 27017 --dbpath /var/lib/mongodb --logpath /var/log/mongodb/mongod.log --replSet rs0 --bind_ip 0.0.0.0 --auth --fork
    ```

    **Note:** 

    -   This command uses the existing database path in the user-created MongoDB instance `/var/lib/mongodb` and the log file `/var/log/mongodb/mongod.log`. You can specify the directory path based on the actual directory path on the user-created server.
    -   This command uses 0.0.0.0 as the binding address of the MongoDB service, which allows access from all IP addresses.
    -   This command enables authentication. Users can only access the database after passing authentication.
    -   You can run the kill command to end the process.
3.  Use the mongo shell to log on to the user-created MongoDB server and run the following commands to initialize the replica set:

    ``` {#codeblock_yva_pwb_oxp}
    use admin
    rs.initiate()
    ```

4.  Wait for a few minutes. The status of the current node will change to primary.

You have enabled oplog for the user-created MongoDB database deployed in a standalone architecture. You can run the `rs.printReplicationInfo()` command to view the status of oplog.

## The procedure of migrating data from MongoDB databases to ApsaraDB for MongoDB instances {#section_njl_2c1_kfb .section}

1.  Log on to the [DTS console](http://dts.aliyun.com).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the upper-right corner of the Data Migrati page, click **Create Migration Task**.
4.  Configure **Source and Destination Databases** of the migration task.

    ![Configure the source and destination databases for MongoDB migration](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6682/156222877334129_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Task Name|     -   DTS automatically generates a name for each task. Task names are not required to be unique.
    -   You can modify task names as needed. We recommend that you specify meaningful names for the tasks to help identify the tasks.
 |
    |Source Database|     -   Instance Type: Select **User-Created Database with Public IP Address**.
    -   Database Type: Select **MongoDB**.
    -   Host Name or IP Address: Enter the address of the user-created MongoDB instance. This address must be a public IP address.
    -   Port: Enter the service port of the user-created MongoDB instance.
    -   Database Name: Enter the name of the authentication database of the user-created MongoDB database.
    -   Database Account: Enter the account used to connect to the user-create database. For more information, see [Migration permission requirements](#section_kvw_kb1_kfb).
    -   Database Password: Enter the password of the database account used to connect to the user-created MongoDB instance.
 |
    |Destination Database|     -   Instance Type: Select **MongoDB Instance**.
    -   Instance Region: Select the region where the destination MongoDB instance is located.
    -   MongoDB instance ID: Select the instance ID of the destination MongoDB instance.
    -   Database Name: Enter the name of the authentication database in the destination instance. The default name is admin.
    -   Database Account: Enter the account used to connect to the database of the destination MongoDB instance. For more information, see [Migration permission requirements](#section_kvw_kb1_kfb).
    -   Database Password: Enter the password of the database account used to connect to the destination MongoDB instance.
 |

5.  After configuring the parameters, click, click **Set Whitelist and Next** in the lower-right corner.

    **Note:** 

    -   The IP address of the DTS server is automatically added to the whitelist of the destination ApsaraDB for MongoDB instance. This ensures that the DTS server can connect to the ApsaraDB for MongoDB instance. After the migration is complete, you can delete the whitelist if you no longer need it. For more information, see [Configure a whitelist](intl.en-US/Quick Start for Standalone/Configure a whitelist.md#).
    -   If a whitelist is configured for the user-created MongoDB database, you must perform the following operations: In the **Source Database** section, click **Obtain DTS IP** to obtain the IP address of the DTS server. Then, add the obtained IP address to the whitelist of the user-created MongoDB database.
6.  Select the migration object and migration type.

    ![Configure the migration object and migration type](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6682/156222877438327_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|     -   If you need to migrate all of the data, select **Full Data Migration** for Migration Types.

**Note:** To ensure data consistency, do not write new data into the source MongoDB database during full data migration.

    -   If you need to migrate the data without stopping businesses, select **Full Data Migration** and **Incremental Data Migration** for Migration Types.

**Note:** For user-created standalone MongoDB instances, you must first enable oplog to use DTS incremental data migration. For more details, see [Preparations before incremental data migration](#section_vqd_r51_dhb).

 |
    |Migration objects.|     -   Select the database to be migrated from the **Available** section and click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/140110/156222877450872_en-US.png)to add the database to the **Selected** box.

**Note:** 

        -   Data in the admin database cannot be migrated even if it is selected.
        -   The config database is an internal database. Do not migrate data from the config database unless otherwise specified.
    -   The migration object can be a database or a collection/function.
    -   After an object is migrated to an ApsaraDB for MongoDB instance, the object name in ApsaraDB for MongoDB is the same as that in the user-created database.

**Note:** If the migrated object has different names in the user-created source database and the destination instance, you can use the object name mapping function provided by DTS. For more information, see [Object name mapping](https://www.alibabacloud.com/help/doc-detail/26628.htm).

 |

7.  When you complete the preceding configurations, click **Precheck** in the lower-right corner.

    **Note:** 

    -   A precheck is performed before the migration task starts. The migration starts only after the precheck succeeds.
    -   If the precheck fails, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/140110/156222877450068_en-US.png) icon corresponding to the check items to view their details. Perform a precheck again after the problems are rectified.
8.  After the precheck succeeds, click **Next**.
9.  On the Confirm Settings page, set **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
10. Click **Buy and Start** to start the migration.
    -   Full data migration

        Wait until the migration task stops automatically.

    -   Incremental data migration

        The migration task does not stop automatically. To stop the migration task, wait until the task is in the **The migration task is not delayed** state, and stop writing to the source database. After a few minutes, the task enters the **The migration task is not delayed** state again, and you can stop the task.

        ![Incremental migration without delay](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75938/156222877433674_en-US.png)


Check whether the data is correct. If yes, you can switch your business from the user-created database to the ApsaraDB for MongoDB instance.

## More information {#section_v5g_lrw_pgb .section}

[Connect to a standalone ApsaraDB for MongoDB instance through the mongo shell](intl.en-US/Quick Start for Standalone/Connect to an instance/Connect to ApsaraDB for MongoDB through the mongo shell.md#)

