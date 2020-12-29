# Migrate data from a replica set MongoDB instance to a sharded cluster instance

This topic describes how to migrate data from a replica set MongoDB instance to a sharded cluster instance by using Data Transmission Service \(DTS\). DTS supports full data migration and incremental data migration. When you migrate data between ApsaraDB for MongoDB instances, you can select both of the supported migration types to ensure service continuity.

Each shard in the destination sharded cluster instance has sufficient storage space.

## Precautions

-   During full data migration, DTS uses read and write resources of the source and destination databases. This may increase the load of the database server. If you migrate a large volume of data or the server specifications cannot meet your requirements, database services may become unavailable. Before you migrate data, evaluate the impact of data migration on the performance of the source and destination databases. We recommend that you migrate data during off-peak hours.
-   If the source and destination ApsaraDB for MongoDB instances have different versions or storage engines, make sure that the versions or storage engines are compatible. For more information, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## Billing

|Migration type|Instance configuration|Internet traffic|
|--------------|----------------------|----------------|
|Full data migration|Free of charge.|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, see [DTS pricing](~~117780~~).|
|Incremental data migration|Charged. For more information, see [DTS pricing](~~117780~~).|

## Migration types

|Migration type|Description|
|--------------|-----------|
|Full data migration|DTS migrates all historical data of the required objects from the source MongoDB database to the destination MongoDB database. **Note:** The following types of objects are supported: database, collection, and index. |
|Incremental data migration|After full data migration is complete, DTS synchronizes incremental data from the source MongoDB database to the destination MongoDB database. **Note:**

-   The create and delete operations that are performed on databases, collections, and indexes can be synchronized.
-   The create, delete, and update operations that are performed on documents can be synchronized. |

## Permissions required for database accounts

|Instance|Full data migration|Incremental data migration|
|:-------|:------------------|--------------------------|
|ApsaraDB for MongoDB replica set instance|The read permission on the source database|The read permission on the source database, admin database, and local database|
|ApsaraDB for MongoDB sharded cluster instance|The read/write permissions on the destination database|The read/write permissions on the destination database|

**Note:** For more information about how to create and authorize a database account, see [Use DMS to manage MongoDB users](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).

## Before you begin

Create databases and collections to be sharded in the destination ApsaraDB for MongoDB instance, and configure data sharding based on your business requirements. For more information, see [Configure sharding to maximize the performance of shards](/intl.en-US/Best Practices/Performance/Configure sharding to maximize the performance of shards.md).

**Note:** After you configure sharding for a cluster, data will not be migrated to the same shard. This maximizes the performance of the sharded cluster.

## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).

2.  In the left-side navigation pane, click **Data Migration**.

3.  At the top of the Migration Tasks page, select the region where the destination ApsaraDB for MongoDB instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner of the page, click **Create Migration Task**.

5.  Configure the source and destination databases for the data migration task.

    ![Configure the source and destination databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5435298951/p33658.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|DTS automatically generates a task name. We recommend that you specify an informative name for easy identification. You do not need to use a unique task name.|
    |Source Database|Instance Type|Select **ApsaraDB for MongoDB**.|
    |Instance Region|Select the region where the source ApsaraDB for MongoDB instance resides.|
    |MongoDB Instance ID|Select the ID of the source ApsaraDB for MongoDB instance.|
    |Database Name|Enter the name of the authentication database. The database account is created in this database. **Note:** If the database account is root, enter admin. |
    |Database Account|Enter the database account of the source ApsaraDB for MongoDB instance. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_ma1_5cy_uqu).|
    |Database Password|Enter the password of the source database account. **Note:** After you specify the source database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the source database parameters based on the check results. |
    |Destination Database|Instance Type|Select **MongoDB Instance**.|
    |Instance Region|Select the region where the destination ApsaraDB for MongoDB instance resides.|
    |MongoDB Instance ID|Select the ID of the destination ApsaraDB for MongoDB instance.|
    |Database Name|Enter the name of the authentication database. The database account is created in this database. **Note:** If the database account is root, enter admin. |
    |Database Account|Enter the database account of the destination ApsaraDB for MongoDB instance. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_ma1_5cy_uqu).|
    |Database Password|Enter the password of the destination database account. **Note:** After you specify the destination database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the destination database parameters based on the check results. |

6.  In the lower-right corner, click **Set Whitelist and Next**.

    **Note:** DTS adds the CIDR blocks of DTS servers to the whitelists of the source and destination ApsaraDB for MongoDB instances. This ensures that DTS servers can connect to the source and destination ApsaraDB for MongoDB instances. After data migration is complete, you can remove the CIDR blocks of DTS servers from the whitelists. For more information, see [Configure a whitelist for a sharded cluster instance]().

7.  Select the migration types and objects to be migrated.

    ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8435298951/p33662.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   To perform only full data migration, select only **Full Data Migration**.
    -   To ensure service continuity during data migration, select both **Full Data Migration** and **Incremental Data Migration**.
 **Note:** If **Incremental Data Migration** is not selected, do not write data to the source ApsaraDB for MongoDB database during full data migration. This ensures data consistency between the source and destination databases. |
    |Objects|    -   Select objects from the **Available** section and click the ![Right arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to move the objects to the **Selected** section.

**Note:** You cannot migrate data from the admin or local database.

    -   You can select databases, collections, or functions as the objects to be migrated.
    -   After an object is migrated to the destination database, the name of the object remains unchanged. You can change the names of the objects that are migrated to the destination database by using the object name mapping feature. For more information about how to use this feature, see [Object name mapping](/intl.en-US/Data Migration/Migration task management/Object name mapping.md). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   Before you can start the data migration task, a precheck is performed. You can start the data migration task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and run the precheck again.
9.  After the task passes the precheck, click **Next**.

10. In the **Confirm Settings** dialog box, specify the **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.

11. Click **Buy and Start** to start the migration task.

    -   Full data migration

        We recommend that you do not manually stop a migration task. Otherwise, data migrated to the destination database will be incomplete. Wait until the migration task automatically stops.

    -   Incremental data migration

        An incremental data migration task does not automatically stop. You must manually stop the migration task.

        **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the destination ApsaraDB for MongoDB instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **incremental data migration** may be displayed in the progress bar.
        2.  After the status of **incremental data migration** changes to **The migration task is not delayed**, manually stop the migration task.

            ![Incremental data migration without delay](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p33674.png)

12. Switch your workloads to the destination ApsaraDB for MongoDB instance.


