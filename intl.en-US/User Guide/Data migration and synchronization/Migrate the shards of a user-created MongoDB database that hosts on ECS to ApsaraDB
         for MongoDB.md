# Migrate the shards of a user-created MongoDB database that hosts on ECS to ApsaraDB for MongoDB

This topic describes how to use Data Transmission Service \(DTS\) to migrate the shards of a user-created MongoDB database that hosts on Elastic Compute Service \(ECS\) to an ApsaraDB for MongoDB instance. DTS allows you to migrate historical and incremental data without business interruptions.

## How it works

DTS migrates a user-created MongoDB database by migrating each shard in the instance. You must create a data migration task for each shard.

**Note:** The distribution of migrated data in the destination instance depends on the shard key that you specify. For more information, see [Configure sharding to maximize the performance of shards](/intl.en-US/Best Practices/Performance/Configure sharding to maximize the performance of shards.md).

![How it works](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1435298951/p50227.png)

## Prerequisites

-   The version of the user-created MongoDB database is 3.0, 3.2, 3.4, 3.6, 4.0, or 4.2.
-   Each shard in the ApsaraDB for MongoDB instance has sufficient storage space.

    **Note:** For example, a user-created MongoDB database has three shards, and one of these shards occupies the most storage space, which is 500 GB. In this case, the storage space of each shard in the ApsaraDB for MongoDB instance must be greater than 500 GB.


## Precautions

-   DTS uses resources of the source and destination instances during full data migration. This may increase the load of the database server. If the data volume is large or the specification is low, the database server may become unavailable. We recommend that you migrate user-created MongoDB databases during off-peak hours.
-   If the source user-created MongoDB database and the destination ApsaraDB for MongoDB instance run different MongoDB versions or storage engines, ensure that your applications can run on both instances. For more information about MongoDB versions and storage engines that are supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## Billing information

|Migration Types|Instance configurations|Internet traffic|
|:--------------|:----------------------|:---------------|
|Full data migration|Free of charge|Free of charge|
|Incremental data migration|Charged, For more information, see [Data Transmission Service \(DTS\) pricing](https://www.alibabacloud.com/zh/product/data-transmission-service/pricing).|Free of charge|

## Migration types

-   Full data migration: All historical data in the source MongoDB database is migrated to the destination MongoDB database.

    **Note:** Data migration is supported at the database, collection, and index levels.

-   Incremental data migration: After full data migration, incremental data is synchronized to the destination MongoDB database.

    **Note:**

    -   The create and delete operations for databases, collections, and indexes can also be synchronized.
    -   The create, delete, and update operations for documents can be synchronized.

## Permissions required for database accounts

|Database|Full data migration|Incremental data migration|
|:-------|:------------------|--------------------------|
|Source user-created MongoDB database on ECS|Read permission on the source database|Read permission on the source database, admin database, and local database|
|Destination ApsaraDB for MongoDB instance|Read/write permissions on the destination database|Read/write permissions on the destination database|

For more information about how to create and authorize a database account, see:

-   [Manage MongoDB users through DMS]() for an ApsaraDB for MongoDB instance.
-   [db.createUser\(\) in MongoDB](https://docs.mongodb.com/manual/reference/method/db.createUser/) for a user-created MongoDB database.

## Preparations before data migration

Disable the balancer for the source database and delete orphaned documents. For more information, see [Migrate user-created MongoDB databases to Alibaba Cloud by using DTS](/intl.en-US/Quick Start for Cluster/Migrate data/Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS.md).

## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the Migration Tasks section, select the region where the ApsaraDB for MongoDB instance resides.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner, click **Create Migration Task**.
5.  Click Create Migration Task. In the **Configure Source and Destination** step, configure the source and destination databases for the migration task.

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |Task Name|-|    -   DTS automatically generates a task name. You do not need to use a unique task name.
    -   We recommend that you use an informative name for easy identification. |
    |Source Database|Instance Type|The type of the instance. In this example, select **User-Created Database in ECS Instance** from the drop-down list.|
    |Instance Region|The region where the ECS instance resides.|
    |ECS Instance ID|The ID of the ECS instance. DTS migrates each shard of the source database in turn. In this example, enter the ID of the ECS instance on which the first shard is deployed.

For the second migration task, enter the ID of the ECS instance on which the second shard is deployed. Repeat this operation until all shards are migrated. |
    |Database Type|The type of the database. In this example, select **MongoDB** from the drop-down list.|
    |Port Number|The service port of the shard. In this example, enter the service port of the first shard.

For the second migration task, enter the service port of the second shard. Repeat this operation until all shards are migrated. |
    |Database Name|The name of the source database to which the database account belongs.|
    |Database Account|The username of the database account used to connect to the source database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_u2r_lh8_kvi).|
    |Database Password|The password of the database account used to connect to the source database. **Note:** After you specify the source database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message appears. If the information is incorrect, the **Failed** message appears. In this case, you must click **Check** next to the **Failed** message to modify the information as prompted. |
    |Destination Database|Instance Type|The type of the instance. In this example, select **MongoDB Instance**.|
    |Instance Region|The region where the ApsaraDB for MongoDB instance resides.|
    |MongoDB Instance ID|The ID of the destination ApsaraDB for MongoDB instance.|
    |Database Name|The name of the destination database to which the database account belongs.|
    |Database Account|The username of the database account used to connect to the destination database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_u2r_lh8_kvi).|
    |Database Password|The password of the database account used to connect to the destination database. **Note:** After you specify the destination database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message appears. If the information is incorrect, the **Failed** message appears. In this case, you must click **Check** next to the **Failed** message to modify the information as prompted. |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    **Note:** The Classless Inter-Domain Routing \(CIDR\) blocks of DTS servers are automatically added to the inbound rule of the ECS instance and the whitelist of the ApsaraDB for MongoDB instance. This ensures that DTS servers can connect to the source and destination instances. After the migration is completed, you can remove these CIDR blocks from the inbound rule and the whitelist as needed. For more information, see [Manage security group rules](https://www.alibabacloud.com/help/zh/doc-detail/25472.htm) and [Configure a whitelist for a replica set instance](/intl.en-US/Quick Start for Replica Set/Configure a whitelist for a replica set instance.md).

7.  Select the migration types and objects to be migrated.

    ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1535298951/p38566.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   To migrate all data, select **Full Data Migration**.

**Note:** To ensure data consistency, do not write new data to the source MongoDB database during full data migration.

    -   To migrate data with minimal downtime, select both **Full Data Migration** and **Incremental Data Migration**. |
    |Migration objects|    -   Select objects from the **Available** section and click the ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to move the objects to the **Selected** section.

**Note:**

        -   Data in the admin and local databases cannot be migrated.
        -   The config database is an internal database. Do not migrate its data unless otherwise specified.
    -   A migration object can be a database, collection, or function.
    -   By default, the names of the objects to be migrated remain unchanged after the migration. You can change the names of the objects in the destination ApsaraDB for MongoDB instance by using the object name mapping feature provided by DTS. For more information about how to use this feature, see [Object name mapping](). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   A precheck is performed before the migration task starts. The migration task starts only after the precheck succeeds.
    -   If the precheck fails, click the ![Tip](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon for each failed check item to view their details. Perform a precheck again after the failures are fixed.
9.  After the precheck succeeds, click **Next**.
10. On the **Confirm Settings** page, set **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
11. Click **Buy and Start** to start the migration task.
12. Repeat Step 4 to Step 11 to create migration tasks for the remaining shards.
13. Stop the data migration task.
    -   Full data migration

        Do not manually stop a task during full data migration. Otherwise, the system may fail to perform a full data migration. Wait until the data migration task automatically stops.

    -   Incremental data migration

        An incremental data migration task does not automatically stop. You must manually stop the migration task.

        **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the destination instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **incremental data migration** may be displayed in the progress bar.
        2.  After the status of **Incremental Data Migration** changes to **The migration task is not delayed**, stop the migration task.

            ![Stop a migration task](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1435298951/p34689.png)

14. Switch your workloads to the ApsaraDB for MongoDB instance.

