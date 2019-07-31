# Migrate data from a standalone MongoDB instance to a replica set or sharded cluster instance {#concept_fdj_twz_zfb .concept}

You can use [Data Transmission Service \(DTS\)](https://dts-intl.console.aliyun.com/) to migrate data from a standalone instance to a replica set or sharded cluster instance.

## Background information {#section_uwn_5jz_ngb .section}

The system architecture of standalone instances are unique. Therefore, standalone instances are suitable for scenarios that do not require storage of enterprise core data, such as development and testing. Replica set instances and sharded cluster instances are more suitable for production scenarios.

This topic describes how to use DTS to migrate a MongoDB database in a standalone instance to a database in a replica set instance or a sharded cluster instance when your business has been adjusted or the existing standalone instance cannot meet your business requirements.

## Precautions {#section_dww_lmr_zfb .section}

-   DTS does not support incremental migration of data in standalone instances.

    **Note:** Stop services related to standalone instances before the migration starts. To ensure data consistency, do not write new data into the database of the standalone instance during migration.

-   The storage space of the destination instance must be larger than that of the source instance.
-   The database of the destination instance supports MongoDB versions 3.2, 3.4, and 4.0.
-   The source database can be migrated to databases with different storage engines. \(ApsaraDB for MongoDB supports three storage engines: WiredTiger, RocksDB, and TerarkDB.\)
-   The data in the admin database cannot be migrated even if it is selected as a migration object.

## Billing information {#section_brm_q21_1gb .section}

|Migration type|Configuration fee|Public network traffic fee|
|:-------------|:----------------|:-------------------------|
|Full data migration|Not billed|Not billed|

## Migration type description {#section_zjf_5fs_zfb .section}

Full data migration: All data of the source database is migrated to the destination database.

-   Migrates databases.
-   Migrates collections.
-   Migrates indexes.

## Migration permission requirements {#section_mfq_xmr_zfb .section}

|Instance type|Required permission|
|:------------|:------------------|
|Source MongoDB instance|Read permissions|
|Destination MongoDB instance|Read and write permissions|

## Premigration preparation for the sharded cluster instance {#section_pcx_yhs_zfb .section}

If you migrate the data of a standalone instance to a sharded cluster instance, we recommend that you shard the data as needed. For more information, see [Configure sharding to maximize the performance of shards](../../../../intl.en-US/Best Practices/Configure sharding to maximize the performance of shards.md#).

**Note:** 

-   You can create a database and a set for data sharding in the destination instance in advance, and configure data sharding based on the database structure of the source instance. You can also configure data sharding after the data migration is complete.
-   Skip this step if you do not need to configure data sharding.

## Migration procedure {#section_lnt_knr_zfb .section}

The following steps provide an example about how to migrate the full data of the mongodbtest database in a standalone instance.

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the upper-right corner of the Data Migration page, click **Create Migration Task**.
4.  Configure **Source and Destination Databases** of the migration task.

    ![Configure source and destination databases](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75938/156455198733658_en-US.png)

    |Parameters for source and destination databases|
    |:----------------------------------------------|
    |Task Name|     -   DTS automatically generates a name for each task. Task names are not required to be unique.
    -   You can modify task names as needed. We recommend that you specify meaningful names for the tasks to help identify the tasks.
 |
    |Source Database|     -   Instance Type: Select **ApsaraDB MongoDB**.
    -   Instance Region: Select the region where the source instance is located.
    -   MongoDB Instance ID: Select the ID of the source instance.
    -   Database Name: Enter the name of the authentication database in the source instance. The default name is admin.
    -   Database Account: Enter the database account of the source instance. For more information, see [Migration permission requirements](#section_mfq_xmr_zfb).
    -   Database Password: Enter the password of the Database Account.
 |
    |Destination Database|     -   Instance Type: Select **MongoDB Instance**.
    -   Instance Region: Select the region where the destination instance is located.
    -   MongoDB Instance ID: Select the ID of the destination instance.
    -   Database Name: Enter the name of the authentication database in the destination instance. The default name is admin.
    -   Database Account: Enter the database account of the destination instance. For more information, see [Migration permission requirements](#section_mfq_xmr_zfb).
    -   Database Password: Enter the password of the Database Account.
 |

5.  After configuring the parameters, click **Set Whitelist and Next** in the lower-right corner.

    **Note:** The IP address of the DTS server is automatically added to the whitelists of the source and destination ApsaraDB for MongoDB instances.This ensures that the DTS server can connect to the ApsaraDB for MongoDB instances. After the migration is complete, you can delete the whitelist if you no longer need it. For more information, see [Configure a whitelist](intl.en-US/User Guide/Data security/Configure a whitelist.md#).

6.  Set **Available** and **Migration Types**.

    ![Configure the migration object and migration type](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83046/156455198735725_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|Migration type: Select **Full Data Migration**. **Note:** To ensure data consistency, do not write new data into the source database during full data migration.

 |
    |Available|     -   Select the database to be migrated from the **Available** area and click the ![Rightwards arrow](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83046/156455198837966_en-US.png) icon to add the database to the **Selected** area.

**Note:** The data in the admin database cannot be migrated even if it is selected as a migration object.

    -   The migration object can be a database or a collection/function.
    -   After an object is migrated to ApsaraDB for MongoDB, the object name in ApsaraDB for MongoDB is the same as that in the source database.

**Note:** If the migrated object has different names in the source instance and the destination instance, you can use the object name mapping function provided by DTS. For more information about the usage, see [Object name mapping](https://help.aliyun.com/document_detail/26628.html).

 |

7.  When you complete the preceding configurations, click **Precheck** in the lower-right corner.

    **Note:** 

    -   A precheck is performed before the migration task starts. The migration starts only after the precheck succeeds.
    -   If the precheck fails, click the ![Notes](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/86903/156455198835996_en-US.png) icon corresponding to the check items to view their details. Perform a precheck again after the problems are rectified.
8.  After the precheck succeeds, click **Next**.
9.  On the **Confirm Settings** page, set **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
10. Click **Buy and Start** to start the migration.

    Wait until the migration task stops automatically.


Switch your businesses to the ApsaraDB for MongoDB instance during off-peak hours to avoid negatively affecting your businesses.

## More information {#section_ogw_hmz_ngb .section}

-   [Connect to an replica set instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to an replica set instance through the mongo shell.md#)
-   [Connect to an ApsaraDB for MongoDB instance](../../../../intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance.md#)

