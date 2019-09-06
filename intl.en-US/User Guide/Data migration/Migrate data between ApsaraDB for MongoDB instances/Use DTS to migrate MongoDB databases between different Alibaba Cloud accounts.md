# Use DTS to migrate MongoDB databases between different Alibaba Cloud accounts {#concept_rzc_lrl_qgb .concept}

This topic describes how to use Data Transmission Service \(DTS\) to migrate MongoDB databases between different Alibaba Cloud accounts. DTS supports full data migration and incremental data migration. You can use incremental data migration to migrate data seamlessly to ApsaraDB for MongoDB without any service interruptions.

## Background information {#section_vsj_hsl_qgb .section}

This topic describes how to use DTS to migrate data from one Alibaba Cloud account to another. You can perform full data migration or incremental data migration by setting the source instance type to **User-Created Database with Public IP Address**.

## Prerequisites {#section_tql_qpw_pgb .section}

-   The source instance must be a standalone instance or replica set instance. If the source instance type is sharded cluster, see [Use mongodump and mongorestore to migrate databases](../../../../intl.en-US/Quick Start for Cluster/Migrate data/Use the built-in commands of MongoDB to migrate data.md#).

    **Note:** DTS does not support [incremental data migration](#section_zjf_5fs_zfb) of standalone instances.

-   The storage space of the destination instance must be larger than the occupied storage space in use of the source instance.

## Precautions {#section_a3z_x11_kfb .section}

We recommend that you migrate your data during off-peak hours to avoid business interruptions.

The data in the admin database cannot be migrated even if it is selected as a migration object.

## Billing information {#section_m3c_t5f_cgb .section}

|Migration type|Configuration fee|Public network traffic fee|
|:-------------|:----------------|:-------------------------|
|Full data migration|Not billed|Not billed|
|Incremental data migration|Billed. For more information, see [Data Transmission Service pricing](https://www.alibabacloud.com/zh/product/data-transmission-service/pricing).|Not billed|

## Migration type description {#section_zjf_5fs_zfb .section}

-   Full data migration: All data from the source instance database is migrated to the destination instance database.
    -   Migrates databases.
    -   Migrates collections.
    -   Migrates indexes.
-   Incremental data migration: The incrementally updated data of the source database is synchronized to the database in the destination instance on the basis of full data migration.
    -   Synchronizes the create and delete operations on databases.
    -   Synchronizes the create, delete, and update operations on documents.
    -   Synchronizes the create and delete operations on collections.
    -   Synchronizes the create and delete operations on indexes.

## Migration permission requirements {#section_kvw_kb1_kfb .section}

If you use DTS to migrate MongoDB databases, you need different permissions when performing different types of migration. The details are as follows:

|Migration object|Full data migration|Incremental data migration|
|:---------------|:------------------|--------------------------|
|Source MongoDB instance|Read permissions| -   Read permissions on the source database
-   Read permissions on the admin database
-   Read permissions on the local database

 |
|Destination MongoDB instance|Read and write permissions|Read and write permissions|

## Premigration preparation for the source instance {#section_ffj_jhm_qgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) with the Alibaba Cloud account to which the source instance belongs.
2.  Apply for a public IP address to connect to the source instance through the Internet. For more information, see [Apply for a public address](intl.en-US/User Guide/Network connection management/Apply for a public address.md#).
3.  Obtain required information from [DTS CIDR blocks](https://www.alibabacloud.com/help/doc-detail/84900.htm)and add the CIDR block of the destination instance to the whitelist of the source instance. For more information, see [Configure a whitelist](intl.en-US/User Guide/Data security/Configure a whitelist.md#).

    For example, the source instance is located in Hangzhou and the destination instance is located in Shenzhen, add the DTS CIDR block of Shenzhen to the whitelist.


## Premigration preparation for the destination instance {#section_pcx_yhs_zfb .section}

If you migrate data to a sharded cluster instance, we recommend that you shard the data as needed. For more information, see [Configure sharding to maximize the performance of shards](../../../../intl.en-US/Best Practices/Configure sharding to maximize the performance of shards.md#).

**Note:** 

-   You can create a database and a set for data sharding in the destination instance in advance, and configure data sharding based on the database structure of the source instance. You can also configure data sharding after the data migration is complete.
-   Skip this step if you do not need to configure data sharding.

## Migration procedure {#section_njl_2c1_kfb .section}

1.  Log on to the [DTS console](http://dts.aliyun.com) with the Alibaba Cloud account to which the destination instance belongs.
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the upper-right corner of the Data Migration page, click **Create Migration Task**.
4.  Configure **Source and Destination Databases** of the migration task.

    ![Configure the source and destination databases of different accounts](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123029/156775255438564_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Task Name|     -   DTS automatically generates a name for each task. Task names are not required to be unique.
    -   You can modify task names as needed. We recommend that you specify meaningful names for the tasks to help identify the tasks.
 |
    |Source Database|     -   Instance Type: Select **User-created Database with Public IP Address**.
    -   Database Type: Select **MongoDB**.
    -   Hostname or IP Address: Enter the domain of the public IP address of the source instance. For example, dds-1udxxxxxxx-pub.mongodb.rds.aliyuncs.com.
    -   Port Number: Enter the service port 3717 of the source instance.
    -   Database Name: Enter the name of the authentication database in the source instance.
    -   Database Account: Enter the account of the database in the source instance. For more information, see [Migration permission requirements](#section_kvw_kb1_kfb).
    -   Database Password: Enter the password of the Database Account.
 |
    |Destination Database|     -   Instance Type: Select **MongoDB Instance**.
    -   Instance Region: Select the region where the destination instance is located.
    -   MongoDB Instance ID: Select the ID of the destination instance.
    -   Database Name: Enter the name of the authentication database in the destination instance. The default name is admin.
    -   Database Account: Enter the database account of the destination instance. For the permission requirement, see [Migration permission requirements](#section_kvw_kb1_kfb).
    -   Database Password: Enter the password of the Database Account.
 |

5.  After configuring the parameters, click **Set Whitelist and Next** in the lower-right corner.

    **Note:** The IP address of the DTS server is automatically added to the whitelist of the destination instance.This ensures that the DTS server can connect to the destination instance. After the migration is complete, you can delete the whitelist if you no longer need it. For more information, see [Configure a whitelist](intl.en-US/Quick Start for Replica Set/Configure a whitelist.md#).

6.  Configure the migration objects and migration types.

    ![Configure the migration types and objects](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123029/156775255438566_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|     -   If you need to migrate all of the data, select **Full Data Migration** for Migration Types.

**Note:** To ensure data consistency, do not write new data into the source instance during full data migration.

    -   If you need to migrate the data without stopping businesses, select **Full Data Migration** and **Incremental Data Migration** for Migration Types.
 |
    |Migration Objects|     -   Select the database to be migrated from the **Available** area and click the ![Rightwards arrow](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83046/156775255437966_en-US.png) icon to add the database to the **Selected** area.

**Note:** The data in the admin database cannot be migrated even if it is selected as a migration object.

    -   The migration object can be a database or a collection/function.
    -   After an object is migrated to ApsaraDB for MongoDB, the object name in ApsaraDB for MongoDB is the same as that in the source database.

**Note:** If the migrated object has different names in the source instance and the destination instance, you can use the object name mapping function provided by DTS. For more information, see [Object name mapping](https://www.alibabacloud.com/help/zh/doc-detail/26628.htm).

 |

7.  When you complete the preceding configurations, click **Precheck** in the lower-right corner.

    **Note:** 

    -   A precheck is performed before the migration task starts. The migration starts only after the precheck succeeds.
    -   If the precheck fails, click the ![Tip](https://dts.console.aliyun.com/styles/images/info.png) icon corresponding to the check items to view their details. Perform a precheck again after the problems are rectified.
8.  After the precheck succeeds, click **Next**.
9.  On the Confirm Settings page, set **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
10. Click **Buy and Start** to start the migration.
    -   Full data migration

        Wait until the migration task stops automatically.

    -   Incremental data migration

        The migration task does not stop automatically. To stop the migration task, wait until the task is in the **Incremental Migration without Delay** state, and stop writing to the source database. After a few minutes, the task enters the **Incremental Migration without Delay** state again, and you can stop the task.

        ![Incremental migration without delay](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123029/156775255438567_en-US.png)


Switch your businesses to the ApsaraDB for MongoDB instance during off-peak hours to avoid negatively affecting your businesses.

## More information {#section_v5g_lrw_pgb .section}

 [Set common alert rules for monitoring ApsaraDB for MongoDB](../../../../intl.en-US/Best Practices/Set common alert rules for monitoring ApsaraDB for MongoDB.md#)

