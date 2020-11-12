# Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using DTS

This topic describes how to migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using Data Transmission Service \(DTS\). DTS supports full data migration and incremental data migration.

For more information about data migration or synchronization solutions, see [Overview](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).

## Prerequisites

-   The version of the user-created MongoDB database is 3.0, 3.2, 3.4, 3.6, or 4.0.
-   The storage capacity of the ApsaraDB for MongoDB instance is larger than the size of the user-created MongoDB database.

## Precautions

-   During full data migration, DTS occupies some storage space of the source and destination databases. This may increase the load of the database servers. If you migrate a large volume of data or the server specifications cannot meet your requirements, the databases may be overloaded or become unavailable. We recommend that you migrate user-created MongoDB databases during off-peak hours.
-   If the source user-created MongoDB database and the destination ApsaraDB for MongoDB instance run different MongoDB versions or storage engines, ensure that your applications can run on both databases. For more information about MongoDB versions and storage engines that are supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## Billing

|Migration type|Instance configurations|Internet traffic|
|--------------|-----------------------|----------------|
|Full data migration|Free of charge.|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, visit [Pricing]().|
|Incremental data migration|Charged. For more information, see [Pricing]().|

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
|Source user-created MongoDB database|Read permissions on the source database|Read permissions on the source database, admin database, and local database|
|Destination ApsaraDB for MongoDB database|Read/write permissions on the destination database|Read/write permissions on the destination database|

For more information about how to create and authorize a database account, see the following topics:

-   [Manage MongoDB users through DMS]() for an ApsaraDB for MongoDB instance
-   [Create User in MongoDB](https://docs.mongodb.com/manual/reference/method/db.createUser/) for a user-created MongoDB database

## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the Migration Tasks section, select the region in which the ApsaraDB for MongoDB instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner, click **Create Migration Task**.
5.  Configure the source and destination database.

    ![Configure the source and destination database](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0034948951/p34129.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|DTS automatically generates a task name. We recommend that you specify an informative name for easy identification. You do not need to use a unique task name.|
    |Source Database|Instance Type|Select an instance type based on the location where the database is deployed. In this topic, a **User-Created Database with Public IP Address** is used as an example. **Note:** If you select other instance types, you must prepare the environment that is required for the source database. For more information, see [Preparation overview](). |
    |Instance Region|If Instance Type is set to **User-Created Database with Public IP Address**, you do not need to specify the **Instance Region** parameter. **Note:** If you have configured a whitelist for the user-created MongoDB database, you must add the CIDR blocks of DTS servers to the whitelist. You can click **Get IP Address Segment of DTS** next to **Instance Region** to obtain the CIDR blocks of DTS servers. |
    |Database Type|Select **MongoDB**.|
    |Hostname or IP Address|Enter the IP address of the user-created MongoDB database. In this example, enter the public IP address.|
    |Port Number|Enter the service port of the user-created MongoDB database. **Note:** In this example, the service port of the user-created MongoDB database must be open to the public network. |
    |Database Name|Enter the name of the authentication database to which the database account belongs.|
    |Database Account|Enter the account that is used to log on to the user-created MongoDB database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_4b9_2qw_i89).|
    |Database Password|Enter the password of the source database account. **Note:** After you specify the source database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the source database configuration is correct, the **Passed** message is displayed. If the **Test Failed** message is displayed, click **Check** next to the **Failed** message to modify the information as prompted. |
    |Connection Method|Select **Non-encrypted**. **Note:** The **SSL-encrypted** option is available only when you migrate MongoDB Atlas. |
    |Destination Database|Instance Type|Select **MongoDB Instance**.|
    |Instance Region|Select the region in which the ApsaraDB for MongoDB instance resides.|
    |MongoDB Instance ID|Select the ID of the ApsaraDB for MongoDB database.|
    |Database Name|Enter the name of the authentication database to which the database account belongs. **Note:** If you want to use the root account, specify admin for the Database Name parameter. |
    |Database Account|Enter the account that is used to log on to the ApsaraDB for MongoDB instance. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_4b9_2qw_i89).|
    |Database Password|Enter the password of the destination database account. **Note:** After you specify the destination database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message is displayed. If the information is incorrect, the **Failed** message is displayed, and you must click **Check** next to the **Failed** message to modify the information as prompted. |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    **Note:** The CIDR blocks of DTS servers are automatically added to the whitelist of the destination RDS instance. This ensures that DTS servers can connect to the destination ApsaraDB for MongoDB instance. After the migration is completed, you can remove these CIDR blocks from the whitelist. For more information, see [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start for Replica Set/Configure a whitelist for a replica set instance.md).

7.  Select the migration types and objects to be migrated.

    ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8924948951/p38327.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   To perform only full data migration, select **Full Data Migration**.
    -   To migrate data with minimal downtime, select both **Full Data Migration** and **Incremental Data Migration**.
 **Note:** If the **Incremental Data Migration** option is not selected, do not write new data to the user-created MongoDB database when full data migration is in progress. Otherwise, data inconsistency may occur. |
    |Migration objects|    -   Select objects from the **Available** section and click the ![Right arrow](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7535298951/p37966.png) icon to move the objects to the **Selected** section.

**Note:**

        -   Data in the admin and local databases cannot be migrated.
        -   The config database is an internal database. We recommend that you do not migrate data in the config database.
    -   A migration object can be a database, collection, or function.
    -   By default, the name of an object remains unchanged after migration. You can change the names of the objects in the destination RDS instance by using the object name mapping feature. For more information, see [Object name mapping](https://www.alibabacloud.com/help/doc-detail/26628.htm). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   Before you can start the data migration task, a precheck is performed. You can start the data migration task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon for each failed check item to view details. Troubleshoot the issues based on the causes and run the precheck again.
9.  After the task passes the precheck, click **Next**.
10. In the Confirm Settings dialog box, specify the **Channel Specification** and select the **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
11. Click **Buy and Start** to start the migration task.
    -   Full data migration

        Do not manually stop a task during full data migration. Otherwise, data migrated to the destination database will be incomplete. Wait until the data migration task succeeds.

    -   Incremental data migration

        An incremental data migration task does not automatically stop. You must manually stop the migration task.

        **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the destination instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **incremental data migration** may be displayed in the progress bar.
        2.  After the status of **Incremental Data Migration** changes to **The migration task is not delayed**, stop the migration task.

            ![No delay exists during incremental data migration](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7535298951/p33674.png)

12. Switch your workloads to the ApsaraDB for MongoDB instance.

## References

[How do I connect to the replica set instance of ApsaraDB for MongoDB?](/intl.en-US/Quick Start for Replica Set/Connect to an instance/Overview of replica set instance connections.md)

