# Migrate data in a MongoDB replica set instance to a sharded cluster instance {#concept_fdj_twz_zfb .concept}

You can use [Data Transmission Service \(DTS\)](https://dts-intl.console.aliyun.com/) to migrate data from a replica set instance to a sharded cluster instance. DTS supports full data migration and incremental data migration. You can use incremental data migration to migrate data seamlessly to ApsaraDB for MongoDB without any service interruptions.

## Prerequisites {#section_hy5_sc1_4gb .section}

-   The database version of the source instance must be version 3.2, 3.4 or 4.0.
-   The storage space of the destination instance must be larger than that of the source instance.

## Precautions {#section_dww_lmr_zfb .section}

-   We recommend that you migrate your data during off-peak hours to avoid business interruptions.
-   The database versions of the destination instance can be 3.2, 3.4, or 4.0.
-   The storage engine of the destination instance can be WiredTiger, RocksDB, and TerarkDB.
-   The data in the admin database cannot be migrated even if it is selected as a migration object.

## Billing information {#section_brm_q21_1gb .section}

|Migration type|Configuration fee|Public network traffic fee|
|:-------------|:----------------|:-------------------------|
|Full data migration|Not billed|Not billed|
|Incremental data migration|Billed. For more information, see [Data Transmission Service pricing](https://www.alibabacloud.com/zh/product/data-transmission-service/pricing).|Not billed|

## Migration type description {#section_zjf_5fs_zfb .section}

-   Full data migration: All data of the database in the source instance is migrated to the database in the destination database.
    -   Migrates databases.
    -   Migrates collections.
    -   Migrates indexes.
-   Incremental data migration: The incrementally updated data of the database in the source instance is synchronized to the database in the destination instance on the basis of full data migration.
    -   Synchronizes the create and delete operations on databases.
    -   Synchronizes the create, delete, and update operations on documents.
    -   Synchronizes the create and delete operations on collections.
    -   Synchronizes the create and delete operations on indexes.

## Migration permission requirements {#section_mfq_xmr_zfb .section}

|Instance type|Full data migration|Incremental data migration|
|:------------|:------------------|:-------------------------|
|Source MongoDB instance|Read permissions| -   Read permissions on the source database
-   Read permissions on the admin database
-   Read permissions on the local database

 |
|Destination MongoDB instance|Read and write permissions|Read and write permissions|

## Premigration preparation {#section_pcx_yhs_zfb .section}

Configure data sharding based on business needs. For more information, see [Configure sharding to maximize the performance of shards](../../../../intl.en-US/Best Practices/Configure sharding to maximize the performance of shards.md#).

**Note:** 

-   You can create a database and a set for data sharding in the destination instance in advance, and configure data sharding based on the database structure of the source instance. You can also configure data sharding after the data migration is complete.
-   Skip this step if you do not need to configure data sharding.

## Migration procedure {#section_lnt_knr_zfb .section}

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the upper-right corner of the Data Migration page, click **Create Migration Task**.
4.  Configure **Source and Destination Databases** of the migration task.

    ![Configure the source and destination databases](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75938/156455146833658_en-US.png)

    |Parameters for source and destination databases|
    |:----------------------------------------------|
    |Task Name|     -   DTS automatically generates a name for each task. Task names are not required to be unique.
    -   You can modify task names as needed. We recommend that you specify meaningful names for the tasks to help identify the tasks.
 |
    |Source Database|     -   Instance Type: Select **ApsaraDB for MongoDB**.
    -   Instance Region: Select the region where the source MongoDB instance is located.
    -   MongoDB Instance ID: Select the ID of the source instance.
    -   Database Name: Enter the name of the authentication database in the source instance. The default value is admin.
    -   Database Account: Enter the database account of the source instance. For more information, see [Migration permission requirements](#).
    -   Database Password: Enter the password of the Database Account.
 |
    |Destination Database|     -   Instance Type: Select **MongoDB Instance**.
    -   Instance Region: Select the region where the destination MongoDB instance is located.
    -   MongoDB Instance ID: Select the ID of the destination instance.
    -   Database Name: Enter the name of the authentication database in the destination instance. The default value is admin.
    -   Database Account: Enter the database account of the destination instance. For more information, see [Migration permission requirements](#).
    -   Database Password: Enter the password of the Database Account.
 |

5.  After configuring the parameters, click **Set Whitelist and Next** in the lower-right corner.

    **Note:** The IP address of the DTS server is automatically added to the whitelist of the ApsaraDB for MongoDB instance.This ensures that the DTS server can connect to the ApsaraDB for MongoDB instance. After the migration is complete, you can delete the whitelist if you no longer need it. For more information, see [Configure a whitelist](intl.en-US/User Guide/Data security/Configure a whitelist.md#).

6.  Set **Available** and **Migration Types**.

    ![Configure migration types and objects](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75938/156455146833662_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|     -   If you need to migrate all of the data, select **Full Data Migration** for Migration Types.

**Note:** To ensure data consistency, do not write new data into the source database during full data migration.

    -   If you need to migrate the data without stopping businesses, select **Full Data Migration** and **Incremental Data Migration** for Migration Types.
 |
    |Migration object|     -   Select the database to be migrated from the **Available** area and click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75938/156455146933712_en-US.png) to add the database to the **Selected** area.

**Note:** The data in the admin database cannot be migrated even if it is selected as a migration object.

    -   The migration object can be a database or a collection/function.
    -   After an object is migrated to the destination MongoDB instance, the object name remains the same as that in the on-premises MongoDB instance by default.

**Note:** If the migrated object has different names in the source instance and the destination instance, you can use the object name mapping function provided by DTS. For more information about the usage, see [Object name mapping](https://www.alibabacloud.com/help/zh/doc-detail/26628.htm).

 |

7.  When you complete the preceding configurations, click **Precheck** in the lower-right corner.

    **Note:** 

    -   A precheck is performed before the migration task starts. The migration starts only after the precheck succeeds.
    -   If the precheck fails, click the ![Notes](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/86903/156455146935996_en-US.png) icon corresponding to the check items to view their details. Perform a precheck again after the problems are rectified.
8.  After the precheck succeeds, click **Next**.
9.  On the **Confirm Settings** page, set **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
10. Click Buy and Start to start the migration.
    -   Full data migration

        Wait until the migration task stops automatically.

    -   Incremental data migration

        The migration task does not stop automatically. To stop the migration task, wait until the task is in the **Incremental Migration without Delay** state, and stop writing to the source database. After a few minutes, the task enters the **Incremental Migration without Delay** state again, and you can stop the task.

        ![Incremental migration without delay](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75938/156455146933674_en-US.png)


Switch your businesses to the ApsaraDB for MongoDB instance during off-peak hours to avoid negatively affecting your businesses.

## More information {#section_kkd_rc1_4gb .section}

 [Connect to an ApsaraDB for MongoDB instance](../../../../intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance.md#)

