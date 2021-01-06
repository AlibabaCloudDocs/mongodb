# Migrate the data of an ApsaraDB for MongoDB instance across regions

This topic describes how to migrate the data of a standalone instance or a replica set instance across regions by using Data Transmission Service \(DTS\). DTS supports both full data migration and incremental data migration. You can use these two methods together to migrate the data of an ApsaraDB for MongoDB instance across regions without interruptions to your business.

-   The source instance is either a standalone instance or a replica set instance. If the source instance is a sharded cluster instance, we recommend that you use the built-in commands of MongoDB to migrate data. For more information, see [Migrate a user-created MongoDB database to ApsaraDB for MongoDB by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate a user-created MongoDB database to ApsaraDB for MongoDB by using tools provided by MongoDB.md).

    **Note:** You cannot use DTS to incrementally migrate the data of a standalone instance. For more information, see [Migration types](#section_iml_stz_6ef).

-   The destination instance is created in the destination region. For more information, see [Create a standalone instance](/intl.en-US/Quick Start/Create an instance/Create a standalone instance.md), [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md), or [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md).

    **Note:** The storage capacity of the destination instance must be greater than the occupied storage space of the source instance.


You may need to migrate the data of an ApsaraDB for MongoDB instance across regions if:

-   You want to restructure your business.
-   You want to use the ApsaraDB for MongoDB instance to provide database services for applications deployed on an ECS instance, but the two instances are in different regions.

The following procedure illustrates how to migrate data from an ApsaraDB for MongoDB instance in China \(Qingdao\) to an instance in China \(Hangzhou\).

![Migrate the data of an ApsaraDB for MongoDB instance across regions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8435298951/p43672.png)

**Note:** The procedure described in this topic only shows how to migrate the data of the source instance. If you no longer need the source instance after the migration is complete, you can release it.

## Precautions

-   We recommend that you migrate your data during off-peak hours to avoid business interruptions.
-   To ensure data consistency, we recommend that you do not write data to the source instance while full data migration of a standalone instance is in progress.
-   If the source and destination instances run different database versions or storage engines, ensure there are no compatibility issues between them before you start migration. For more information about the database versions and storage engines supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).
-   If the minor version of your instance expires or is not included in the maintenance list and the instance is upgraded, migrated, changed, or cloned, the system will upgrade the minor version to the latest version by default. This ensures better performance and stability of the instance.

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

## Required database account permissions

|Data source|Full data migration|Incremental data migration|
|:----------|:------------------|--------------------------|
|Source ApsaraDB for MongoDB instance|Read permissions on the source database|Read permissions on the source database, admin database, and local database|
|Destination ApsaraDB for MongoDB instance|Read/write permissions on the destination database|Read/write permissions on the destination database|

**Note:** For more information about how to create and authorize a database account, see [Use DMS to manage MongoDB users](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).

## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).

2.  In the left-side navigation pane, click **Data Migration**.

3.  At the top of the Migration Tasks page, select the region where the destination ApsaraDB for MongoDB instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner of the page, click **Create Migration Task**.

5.  Configure both the source and destination databases.

    ![Configure the source and destination ApsaraDB for MongoDB databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8435298951/p43677.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|DTS automatically generates a task name. We recommend that you specify your own task name that helps identify the task. Task names do not need to be unique.|
    |Source Database|Instance Type|Select **ApsaraDB for MongoDB**.|
    |Instance Region|Select the region where the source ApsaraDB for MongoDB instance resides. For this example, select **China \(Qingdao\)**.|
    |MongoDB Instance ID|Select the ID of the source ApsaraDB for MongoDB instance.|
    |Database Name|Enter the name of the authentication database. It is the database where the database account is created. **Note:** If the database account is root, enter admin. |
    |Database Account|Enter the username of the database account you use to manage the source database. For more information about the account permission requirements, see [Required database account permissions](#section_jh6_15m_pea).|
    |Database Password|Enter the password of the database account. **Note:** After you specify the source database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message is displayed. If the information is incorrect, the **Failed** message is displayed, and you must click **Check** next to the **Failed** message to modify the information as prompted. |
    |Destination Database|Instance Type|Select **MongoDB Instance**.|
    |Instance Region|Select the region where the destination ApsaraDB for MongoDB instance resides. For this example, select **China \(Hangzhou\)**.|
    |MongoDB Instance ID|Select the ID of the destination ApsaraDB for MongoDB instance.|
    |Database Name|Enter the name of the authentication database. It is the database where the database account is created. **Note:** If the database account is root, enter admin. |
    |Database Account|Enter the username of the database account you use to manage the destination database. For more information about the account permission requirements, see [Required database account permissions](#section_jh6_15m_pea).|
    |Database Password|Enter the password of the database account. **Note:** After you specify the destination database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message is displayed. If the information is incorrect, the **Failed** message is displayed, and you must click **Check** next to the **Failed** message to modify the information as prompted. |

6.  In the lower-right corner, click **Set Whitelist and Next**.

    **Note:** DTS adds the CIDR blocks of DTS servers to the whitelists of the source and destination ApsaraDB for MongoDB instances. This ensures that DTS servers can connect to the source and destination ApsaraDB for MongoDB instances. After data migration is complete, you can remove the CIDR blocks of DTS servers from the whitelists. For more information, see [Configure a whitelist for a sharded cluster instance]().

7.  Configure migration types and migration objects.

    ![Configure migration types and migration objects](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8435298951/p33662.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   If you want to migrate all data, select **Full Data Migration**.
    -   If you want to migrate data without interruptions to your business, select both **Full Data Migration** and **Incremental Data Migration**.
**Note:**

    -   You cannot use DTS to incrementally migrate the data of a standalone instance.
    -   If **Incremental Data Migration** is not selected, do not write data into the source database during full data migration. This ensures data consistency between the source and destination databases. |
    |Available|    -   In the **Available** section, select the objects you want to migrate and then click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p37966.png) icon to move them to the **Selected** section.

**Note:** Data in the admin database cannot be migrated even if this database is selected.

    -   A migration object can be a database, collection, or function.
    -   By default, the name of an object remains unchanged after migration. If you want a different object name after migration, use the object name mapping feature provided by DTS. For more information, see [Object name mapping](https://www.alibabacloud.com/help/zh/doc-detail/26628.htm). |

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


## What to do next

Determine whether to release the source instance.

-   If the source instance uses pay-as-you-go billing, release it. For more information, see [Release an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Release an ApsaraDB for MongoDB instance.md).
-   If the source instance uses subscription billing, you cannot release it.

