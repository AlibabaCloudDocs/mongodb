# Migrate data between ApsaraDB for MongoDB instances created by different Alibaba Cloud accounts

This topic describes how to migrate data between ApsaraDB for MongoDB instances created by different Alibaba Cloud accounts by using Data Transmission Service \(DTS\). DTS supports both full data migration and incremental data migration. You can use these two methods together to migrate data between ApsaraDB for MongoDB instances without interruptions to your business.

## Prerequisites

-   The source instance is either a standalone instance or a replica set instance. If the source instance is a sharded cluster instance, we recommend that you use the built-in tools of MongoDB to migrate data. For more information, see [Migrate a self-managed MongoDB database to ApsaraDB for MongoDB by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate a self-managed MongoDB database to ApsaraDB for MongoDB by using tools provided
         by MongoDB.md).

    **Note:** You cannot use DTS to incrementally migrate the data of a standalone instance. For more information, see [Migration types](#section_0gp_q2m_yw6).

-   The destination instance is created in the region. For more information, see [Create a standalone instance](/intl.en-US/Quick Start/Create an instance/Create a standalone instance.md), [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md), or [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md).

    **Note:** The storage capacity of the destination instance must be greater than the occupied storage space of the source instance.


## Precautions

-   DTS uses resources of the source and destination instances during full data migration. This may increase the load of the database server. If the data volume is large or the specification is low, the database server may become unavailable. We recommend that you migrate data during off-peak hours.
-   To ensure data consistency, we recommend that you do not write data to the source instance while full data migration of a standalone instance is in progress.
-   If the source and destination instances run different database versions or storage engines, make sure that the instances do not have compatibility issues between them before you start the migration. For more information about the database versions and storage engines supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).
-   To ensure better performance and stability of the instance, the system will upgrade the minor version to the latest version by default. If the minor version of your instance expires or is not included in the maintenance list and the instance is [upgraded](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md), [migrated](/intl.en-US/User Guide/Data migration and synchronization/Overview.md), [changed](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md), [Created from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Created by point-in-time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), or performed [Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md).

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

|Data source|Full data migration|Incremental data migration|
|:----------|:------------------|--------------------------|
|Source ApsaraDB for MongoDB instance|Read permissions on the source database|Read permissions on the source database, admin database, and local database|
|Destination ApsaraDB for MongoDB instance|Read and write permissions on the destination database|Read and write permissions on the destination database|

**Note:** For more information about how to create and authorize a database account, see [Manage MongoDB databases by using DMS](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).

## Preparations

1.  Log on to the ApsaraDB for MongoDB console by using the Alibaba Cloud account to which the source instance belongs. For more information, see [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  Apply for a public endpoint for the source instance. For more information, see [Apply for a public endpoint for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Public IP Connection/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md).
3.  Add the Classless Inter-Domain Routing \(CIDR\) blocks of DTS servers to a whitelist of the source instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

    **Note:** You can determine the CIDR blocks you need to add based on the region where the destination instance is deployed. For more information, see [Add the CIDR blocks of DTS servers to the security settings of on-premises databases]().

    For example, if the source instance is in China \(Hangzhou\) and the destination instance is in China \(Shenzhen\), add the CIDR blocks of the DTS servers in China \(Shenzhen\) to a whitelist of the source instance.


## Procedure

1.  Log on to the [Data Transmission Service console](https://dts-intl.console.aliyun.com/) with the Alibaba Cloud account to which the destination ApsaraDB for MongoDB instance belongs.

2.  In the left-side navigation pane, click **Data Migration**.

3.  At the top of the Migration Tasks page, select the region where the destination ApsaraDB for MongoDB instance is deployed.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner of the page, click **Create Migration Task**.

5.  Create a data migration task.

    1.  Configure the source and destination databases for the data migration task.

        ![Configure the source and destination ApsaraDB for MongoDB databases created by different Alibaba Cloud accounts](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1535298951/p38564.png)

        |Section|Parameter|Description|
        |:------|:--------|:----------|
        |N/A|Task Name|The name of the migration task. DTS automatically generates a task name. We recommend that you set a descriptive name that makes it easy to identify. Task names do not have to be unique.|
        |Source Database|Instance Type|Select **User-Created Database with Public IP Address**.|
        |Instance Region|The region where the source instance is deployed.|
        |Database Type|The database engine of the source instance. In this example, select **MongoDB**.|
        |Hostname or IP Address|Enter the domain name obtained from the public endpoint of the source instance. For example, enter dds-1udxxxxxxx-pub.mongodb.rds.aliyuncs.com.|
        |Port Number|Enter **3717**, which is the service port of the source instance.|
        |Database Name|The name of the database corresponding to the username if authentication is enabled. **Note:** If the database account is root, enter admin. |
        |Database Account|The account that is used to log on to the source database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_9t3_tu1_gm7).|
        |Database Password|The password of the source database account. **Note:** After you specify the source database parameters, click **Test Connectivity** next to **Database Password** to verify whether the information is valid. If the information is valid, the **Passed** message appears. If the **Failed** message appears, click **Check** in the **Failed** message to modify the information. |
        |Encryption|Indicates whether an encrypted connection is used for the source instance. Select **Non-encrypted** or **SSL-encrypted**. If you select **SSL-encrypted**, you must enable SSL encryption for the source instance before you configure the data synchronization task. **Note:**

        -   You can select **SSL-encrypted** only for source MongoDB Atlas databases.
        -   If you select **SSL-encrypted**, more CPU resources will be consumed. |
        |Destination Database|Instance Type|The category of the destination instance. In this example, select **MongoDB Instance**.|
        |Instance Region|Select the region where the destination ApsaraDB for MongoDB instance is deployed.|
        |MongoDB Instance ID|The ID of the destination instance. In this example, select the ID of the destination ApsaraDB for MongoDB instance.|
        |Database Name|The name of the database corresponding to the username if authentication is enabled. **Note:** If the database account is root, enter admin. |
        |Database Account|The account that is used to log on to the destination database. In this example, enter the destination ApsaraDB for MongoDB database account. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_9t3_tu1_gm7).|
        |Database Password|The password of the destination database account. **Note:** After you specify the destination database parameters, click **Test Connectivity** next to **Database Password** to verify whether the information is valid. If the information is valid, the **Passed** message appears. If the information is invalid, the **Failed** message appears, and you must click **Check** next to the **Failed** message to modify the information. |

    2.  In the lower-right corner, click **Set Whitelist and Next**. In the dialog box that appears, click **Next**.

        **Note:** After the migration is complete, you can remove the IP addresses from the whitelist if they are no longer needed. For more information, see [Configure a whitelist](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md).

    3.  Select the migration types and the objects to be migrated.

        ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1535298951/p38566.png)

        |Parameter|Description|
        |---------|-----------|
        |Migration Types|We recommend that you select both **Full Data Migration** and **Incremental Data Migration** to ensure the consistency of migrated data. If you select only **Full Data Migration**, the data updated during the migration process may not be migrated from the source instance to the destination instance.

If you select only **Incremental Data Migration**,

        -   Only incremental data generated in the source instance is migrated.
        -   In incremental migration mode, triggers cannot be synchronized. For more information, see [Configure a data synchronization task for a source database that contains a trigger](/intl.en-US/Best Practices/Configure a data synchronization task for a source database that contains a trigger.md). |
        |Objects|        -   In the **Available** section, select the objects you want to migrate and then click the ![Right arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p37966.png) icon to move them to the **Selected** section.

**Note:** Data in the admin and local databases cannot be migrated.

        -   A migration object can be a database, collection, or function.
        -   By default, the name of an object remains unchanged after migration. If you want a different object name after migration, use the object name mapping feature provided by DTS. For more information, see [Object name mapping](https://www.alibabacloud.com/help/zh/doc-detail/26628.htm). |
        |Specify whether to rename object names|You can use the object name mapping feature to change the names of the objects that are synchronized to the destination instance. For more information, see [Object name mapping](/intl.en-US/Data Migration/Migration task management/Object name mapping.md).|
        |Specify the retry time for failed connection to the source or destination database|By default, if DTS fails to connect to the source or destination database, DTS retries within the next 12 hours. You can specify the retry time based on your needs. If DTS reconnects to the source and destination databases within the specified time, DTS resumes the data migration task. Otherwise, the data migration task fails. **Note:** When DTS retries a connection, you are charged for the DTS instance. We recommend that you specify the retry time based on your business needs. You can also release the DTS instance at your earliest opportunity after the source and destination instances are released. |

    4.  After the preceding configurations are complete, you can select one of the following operations based on your requirements:

        -   If you do not need to perform the data migration task immediately, click **Save** in the lower-right corner of the page.

            To start a data migration task later, find the migration task in the data migration task list, click **Start Task**, and then click **OK** in the message that appears.

        -   To perform the data migration task immediately, click **Precheck** in the lower-right corner of the page.
        **Note:**

        -   A precheck is performed before the migration task starts. You can start the data migration task only after the task passes the precheck.
        -   If the task fails to pass the precheck, you can click the ![Hint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3457359951/p47468.png) icon next to each failed item to view details.
            -   You can troubleshoot the issues based on the causes and run a precheck again.
            -   If you do not need to troubleshoot the issues, you can ignore failed items and run a precheck again.
    5.  After the task passes the precheck, click **Next**.
    6.  In the **Confirm Settings** dialog box, specify the **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
    7.  Click **Buy and Start** to start the migration task.
        -   Full data migration

            Do not manually stop a task during full data migration. Otherwise, the system may fail to perform a full data migration. Wait until the full data migration task automatically stops.

        -   Incremental data migration

            An incremental data migration task does not automatically end. You must manually end the task. Perform the following operations:

            **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the destination ApsaraDB for MongoDB instance.

            1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **Incremental Data Migration** may appear in the progress bar.
            2.  After the status of **incremental data migration** changes to **The migration task is not delayed**, manually stop the migration task.

                ![Incremental data migration without delay](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p33674.png)

    8.  Switch your workloads to the destination ApsaraDB for MongoDB instance.

## What to do next

Determine whether to release the source instance.

-   If the source instance uses the pay-as-you-go billing method, release the source instance. For more information, see [Release an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Release an ApsaraDB for MongoDB instance.md).
-   If the source instance uses the subscription billing method, you cannot release the source instance.

## References

If you migrate data to a sharded cluster instance, you can configure data sharding as needed. For more information, see [Configure sharding to maximize the performance of shards](/intl.en-US/Best Practices/Performance/Configure sharding to maximize the performance of shards.md).

