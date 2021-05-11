# Migrate data from a replica set instance to a sharded cluster instance

This topic describes how to migrate data from a replica set instance to a sharded cluster instance by using Data Transmission Service \(DTS\). DTS supports full data migration and incremental data migration. When you migrate data between ApsaraDB for MongoDB instances, you can select both of the supported migration types to ensure service continuity.

Make sure that the shard nodes in the destination sharded cluster instance have sufficient storage space.

## Precautions

-   DTS uses resources of the source and destination instances during full data migration. This may increase the load of the database server. If you migrate a large volume of data or the server specifications cannot meet your requirements, database services may become unavailable. Before you migrate data, evaluate the impact of data migration on the performance of the source and destination instances. We recommend that you migrate data during off-peak hours.
-   If the source and destination instances run different MongoDB versions or storage engines, make sure that your applications can run on the source and destination instances. For more information about MongoDB versions and storage engines that are supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## Pricing

|Migration type|Instance fee|Internet traffic fee|
|--------------|------------|--------------------|
|Full data migration|Free of charge|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, see [DTS pricing](~~117780~~).|
|Incremental data migration|Charged. For more information, see [DTS pricing](~~117780~~).|

## Migration types

|Migration type|Description|
|--------------|-----------|
|Full data migration|All data of the migration objects is migrated from the source instance to the destination instance. **Note:** The following types of objects are supported: database, collection, and index. |
|Incremental data migration|Updated data of the migration objects is synchronized from the source instance to the destination instance. **Note:**

-   The create and delete operations that are performed on databases, collections, and indexes can be synchronized.
-   The create, delete, and update operations that are performed on documents can be synchronized. |

## Permissions required for database accounts

|Instance|Full data migration|Incremental data migration|
|:-------|:------------------|--------------------------|
|ApsaraDB for MongoDB replica set instance|Read permissions on the source database|Read permissions on the source database, admin database, and local database|
|ApsaraDB for MongoDB sharded cluster instance|Read and write permissions on the destination database|Read and write permissions on the destination database|

**Note:** For more information about how to create and authorize a database account, see [Use DMS to manage MongoDB users](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).

## Preparations

Create databases and collections to be sharded in the destination ApsaraDB for MongoDB instance, and configure data sharding based on your business requirements. For more information, see [Configure sharding to maximize the performance of shards](/intl.en-US/Best Practices/Performance/Configure sharding to maximize the performance of shards.md).

**Note:** After you configure sharding for a cluster, data will not be migrated to the same shard. This maximizes the performance of the sharded cluster.

## Procedure

1.  Log on to the [Data Transmission Service console](https://dts-intl.console.aliyun.com/).

2.  In the left-side navigation pane, click **Data Migration**.

3.  At the top of the Migration Tasks page, select the region where the destination ApsaraDB for MongoDB instance is deployed.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner of the page, click **Create Migration Task**.

5.  In the Configure Source and Destination step, configure the source and destination database for the migration task.

    ![Configure the source and destination databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5435298951/p33658.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|The name of the migration task. DTS automatically generates a task name. We recommend that you set a descriptive name that makes it easy to identify. Task names do not have to be unique.|
    |Source Database|Instance Type|The category of the source instance. In this example, select **ApsaraDB for MongoDB**.|
    |Instance Region|Select the region where the source ApsaraDB for MongoDB instance is deployed.|
    |MongoDB Instance ID|The ID of the source ApsaraDB for MongoDB instance.|
    |Database Name|The name of the database corresponding to the username if authentication is enabled. **Note:** If the database account is root, enter admin. |
    |Database Account|The account that is used to log on to the source database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_ma1_5cy_uqu).|
    |Database Password|The password of the source database account. **Note:** After you specify the source database parameters, click **Test Connectivity** next to **Database Password** to verify whether the information is valid. If the information is valid, the **Passed** message appears. If the information is invalid, the **Failed** message appears, and you must click **Check** next to the **Failed** message to modify the information. |
    |Destination Database|Instance Type|The category of the destination instance. In this example, select **MongoDB Instance**.|
    |Instance Region|The region where the destination instance is deployed. In this example, select the region where the destination ApsaraDB for MongoDB instance is deployed.|
    |MongoDB Instance ID|The ID of the destination instance. In this example, select the ID of the destination ApsaraDB for MongoDB instance.|
    |Database Name|The name of the database corresponding to the username if authentication is enabled. **Note:** If the database account is root, enter admin. |
    |Database Account|The account that is used to log on to the destination database. In this example, enter the database account of the destination ApsaraDB for MongoDB. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_ma1_5cy_uqu).|
    |Database Password|The password of the destination database account. **Note:** After you specify the destination database parameters, click **Test Connectivity** next to **Database Password** to verify whether the information is valid. If the information is valid, the **Passed** message appears. If the information is invalid, the **Failed** message appears, and you must click **Check** next to the **Failed** message to modify the information. |

6.  In the lower-right corner, click **Set Whitelist and Next**.

    **Note:** DTS adds the CIDR blocks of DTS servers to the whitelists of the source and destination ApsaraDB for MongoDB instances. This ensures that DTS servers can connect to the source and destination ApsaraDB for MongoDB instances. After data migration is complete, you can remove the CIDR blocks of DTS servers from the whitelists. For more information, see [Configure a whitelist for a sharded cluster instance]().

7.  Configure migration types and objects to be migrated.

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   To perform only full data migration, select **Full Data Migration**.
    -   To ensure service continuity during data migration, select **Full Data Migration** and **Incremental Data Migration**.
**Note:** If **Incremental Data Migration** is not selected, do not write data to the source ApsaraDB for MongoDB instance during full data migration. This ensures data consistency between the source and destination instances. |
    |Objects|    -   In the **Available** section, select the objects to be migrated. Then, click the ![Right arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to add them to the **Selected** section.

**Note:** Data in the admin and local databases cannot be migrated.

    -   A migration object can be a database, collection, or function.
    -   By default, the name of an object remains unchanged after migration. If you want a different object name after migration, use the object name mapping feature provided by DTS. For more information, see [Object name mapping](/intl.en-US/Data Migration/Migration task management/Object name mapping.md). |
    |Specify whether to rename object names|You can use the object name mapping feature to change the names of the objects that are synchronized to the destination instance. For more information, see [Object name mapping](/intl.en-US/Data Migration/Migration task management/Object name mapping.md).|
    |Specify the retry time for failed connection to the source or destination database|By default, if DTS fails to connect to the source or destination database, DTS retries within the next 12 hours. You can specify the retry time based on your needs. If DTS reconnects to the source and destination databases within the specified time, DTS resumes the data migration task. Otherwise, the data migration task fails. **Note:** When DTS retries a connection, you are charged for the DTS instance. We recommend that you specify the retry time based on your business needs. You can also release the DTS instance at your earliest opportunity after the source and destination instances are released. |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   Before you can start the data migration task, a precheck is performed. DTS can migrate data only if the precheck is past.
    -   If the precheck fails, click the ![Prompt](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3457359951/p47468.png) icon next to each failed item to view details. Fix the issues as prompted and run the precheck again.
9.  After the task passes the precheck, click **Next**.

10. In the **Confirm Settings** dialog box, specify the **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.

11. Click **Buy and Start** to start the migration task.

    -   Full data migration

        Do not manually stop a task during full data migration. Otherwise, the system may fail to perform a full data migration. Wait until the full data migration task automatically stops.

    -   Incremental data migration

        An incremental data migration task does not automatically end. You must manually end the task.

        **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the destination ApsaraDB for MongoDB instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **incremental data migration** may be displayed in the progress bar.
        2.  After the status of **incremental data migration** changes to **The migration task is not delayed**, manually stop the migration task.

            ![Incremental data migration without delay](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p33674.png)

12. Switch your workloads to the destination ApsaraDB for MongoDB instance.


