---
keyword: [MongoDB windows service, server migrates data to MongoDB, MongoDB Linux, MongoDB data migration, MongoDB data import, MongoDB data export, Migrate MongoDB standalone data to clusters, MongoDB replica set migration sharding set]
---

# Migrate an ECS-hosted self-managed MongoDB database that uses the standalone or replica set architecture to ApsaraDB for MongoDB

This topic describes how to use Data Transmission Service \(DTS\) to migrate a self-managed MongoDB database that hosts on Elastic Compute Service \(ECS\) and uses the standalone or replica set architecture to ApsaraDB for MongoDB. DTS allows you to migrate historical and incremental data without business interruptions.

## Prerequisites

-   The version of the self-managed MongoDB database is 3.0, 3.2, 3.4, 3.6, 4.0, or 4.2.
-   The storage space of the ApsaraDB for MongoDB instance is larger than the size of the self-managed MongoDB database.

## Usage notes

-   We recommend that you migrate your data during off-peak hours to avoid business interruptions.
-   The config database is an internal database. Do not migrate its data unless otherwise specified.
-   If the self-managed MongoDB database and the destination ApsaraDB for MongoDB instance run different MongoDB versions or storage engines, make sure that your applications can run on both databases. For more information about the MongoDB versions and storage engines that ApsaraDB for MongoDB supports, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## Billing information

|Migration Types|Instance configurations|Internet traffic|
|:--------------|:----------------------|:---------------|
|Full data migration|Free of charge|Free of charge|
|Incremental data migration|Charged, For more information, see [Data Transmission Service \(DTS\) pricing](https://www.alibabacloud.com/zh/product/data-transmission-service/pricing).|Free of charge|

## Migration type description

-   Full data migration: All data of the migration objects is migrated from the source instance to the destination instance..

    **Note:** Data migration is supported at the database, collection, and index levels.

-   Incremental data migration: Updated data of the migration objects is synchronized from the source instance to the destination instance..

    **Note:**

    -   The create and delete operations for databases, collections, and indexes can be synchronized.
    -   The create, delete, and update operations on documents can be synchronized.

## Permissions required for database accounts

|Database|Full data migration|Incremental data migration|
|:-------|:------------------|--------------------------|
|Self-managed MongoDB database on ECS|Read permissions on the source database|Read permissions on the source database, admin database, and local database|
|Destination ApsaraDB for MongoDB instance|Read/write permissions on the destination databases|Read/write permissions on the destination databases|

For more information about how to create and authorize a database account, see the following topics:

-   [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md) for an ApsaraDB for MongoDB instance.
-   [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/) for a self-managed MongoDB database.

## Preparations before data migration

Skip this step if the self-managed MongoDB database on ECS uses the replica set architecture.

If the self-managed MongoDB database on ECS uses the standalone architecture, enable oplog for the database before you migrate incremental data. For more information, see [Preparations for incremental data migration](/intl.en-US/Quick Start/Migrate data/Migrate self-managed standalone MongoDB databases to Alibaba Cloud by using DTS.md).

## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the Migration Tasks section, select the region where the ApsaraDB for MongoDB instance is deployed.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner, click **Create Migration Task**.
5.  Configure the source and destination databases.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9335298951/p52890.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |Task Name|N/A|    -   DTS automatically generates a task name. You do not need to use a unique task name.
    -   We recommend that you use an informative name for easy identification. |
    |Source Database|Instance Type|Select **User-Created Database in ECS Instance**.|
    |Instance Region|The region where the ECS instance is deployed.|
    |ECS Instance ID|The ID of the ECS instance on which the self-managed MongoDB database is deployed.|
    |Database Type|The type of the database. In this example, select **MongoDB** from the drop-down list.|
    |Port Number|The service port of the self-managed MongoDB database.|
    |Database Name|The name of the destination database to which the database account belongs.|
    |Database Account|The username of the database account used to connect to the source database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_u2r_lh8_kvi).|
    |Database Password|The password of the database account used to connect to the source database. **Note:** After you specify the source database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message appears. If the information is incorrect, the **Failed** message appears. In this case, you must click **Check** next to the **Failed** message to modify the information. |
    |Destination Database|Instance Type|The type of the instance. In this example, select **MongoDB Instance**.|
    |Instance Region|The region where the ApsaraDB for MongoDB instance is deployed.|
    |The ID of the ApsaraDB for MongoDB instance.|The ID of the destination ApsaraDB for MongoDB instance.|
    |Database Name|The name of the destination database to which the database account belongs.|
    |Database Account|The username of the database account used to connect to the destination database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_u2r_lh8_kvi).|
    |Database Password|The password of the database account used to connect to the destination database. **Note:** After you specify the destination database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message appears. If the information is incorrect, the **Failed** message appears. In this case, you must click **Check** next to the **Failed** message to modify the information. |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    **Note:** The CIDR blocks of DTS servers are automatically added to the inbound rule of the ECS instance and the whitelist of the ApsaraDB for MongoDB instance. This ensures that DTS servers can connect to the source and destination instances. After data migration is complete, you can remove the CIDR blocks of DTS servers from the whitelists. For more information, see [Manage security group rules](https://www.alibabacloud.com/help/zh/doc-detail/25472.htm) and [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md).

7.  Select the migration types and the objects to be migrated.

    ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1535298951/p38566.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   To migrate all data, select **Full Data Migration**.

**Note:** To ensure data consistency, do not write new data to the source MongoDB database during full data migration.

    -   To migrate data with minimal downtime, select both **Full Data Migration** and **Incremental Data Migration**.

**Note:** Before you migrate incremental data from a standalone self-managed MongoDB database, you must enable oplog for the database. For more information, see [Preparations before data migration](#section_w9n_i40_l6d). |
    |Migration objects|    -   Select objects from the **Available** section and click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to move the objects to the **Selected** section.

**Note:**

        -   Data in the admin and local databases cannot be migrated.
        -   The config database is an internal database. Do not migrate its data unless otherwise specified.
    -   A migration object can be a database, collection, or function.
    -   By default, the names of the objects to be migrated remain unchanged after the migration. You can change the names of the objects in the destination ApsaraDB for MongoDB instance by using the object name mapping feature provided by DTS. For more information about how to use this feature, see [Object name mapping](/intl.en-US/Data Migration/Migration task management/Object name mapping.md). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   A precheck is performed before the migration task starts. The migration task starts only after the precheck succeeds.
    -   If the precheck fails, click the ![Tip](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon for each failed check item to view their details. Perform a precheck again after the failures are fixed.
9.  After the precheck succeeds, click **Next**.
10. Click **Buy and Start** to start the migration task.
    -   Full data migration

        Do not manually end a migration task. If you do so, the system may fail to migrate all data of the database. Wait until the migration task is complete.

    -   Incremental data migration

        An incremental data migration task does not automatically end. You need to manually end the task.

        **Note:** Select an appropriate point in time to manually end a migration task. For example, you can end the migration task during off-peak hours or before you switch over your business to the destination ApsaraDB for MongoDB instance.

        1.  When the task progress bar displays **Incremental Data Migration** and **The migration task is not delayed**, stop writing data to the source database for a few minutes. Wait until the progress bar displays the delay time of the incremental data migration next to **Incremental Data Migration**.
        2.  After the status of **Incremental Data Migration** changes to **The migration task is not delayed**, manually end the migration task.

            ![Incremental data migration without delay](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p33674.png)

11. Switch over your business to the destination ApsaraDB for MongoDB instance.

