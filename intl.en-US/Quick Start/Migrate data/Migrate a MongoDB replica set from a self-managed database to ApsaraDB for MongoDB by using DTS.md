# Migrate a MongoDB replica set from a self-managed database to ApsaraDB for MongoDB by using DTS

This topic describes how to migrate a MongoDB replica set from a self-managed database to ApsaraDB for MongoDB by using Data Transmission Service \(DTS\). DTS supports full data migration and incremental data migration. The data migration does not interrupt your services if you select both of the two migration types.

You can also use the tools provided by MongoDB to perform the migration. For more information, see [Migrate self-managed databases to Alibaba Cloud by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate self-managed databases to Alibaba Cloud by using tools provided by MongoDB.md). For more information about data migration and synchronization solutions, see [Overview](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).

## Prerequisites

-   The version of the self-managed MongoDB database is 3.0, 3.2, 3.4, 3.6, or 4.0.
-   The storage capacity of the ApsaraDB for MongoDB instance is larger than the size of the self-managed MongoDB database.

## Precautions

-   DTS uses resources of the source and destination instances during full data migration. This may increase the load of the database server. If you migrate a large volume of data or if the server specifications cannot meet your requirements, the databases may be overloaded or become unavailable. We recommend that you migrate data during off-peak hours.
-   If the source self-managed MongoDB database and the destination ApsaraDB for MongoDB instance run different MongoDB versions or storage engines, make sure that your applications can run on both the source database and the destination instance. For more information about MongoDB versions and storage engines that are supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## Billing information

|Migration type|Instance fee|Internet traffic fee|
|--------------|------------|--------------------|
|Full data migration|Free of charge.|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, see [Pricing]().|
|Incremental data migration|Charged. For more information, see [Pricing]().|

## Migration types

-   Full data migration: All historical data in the source self-managed sharded MongoDB database is migrated to the destination ApsaraDB for MongoDB instance.

    **Note:** Data migration is supported at the database, collection, and index levels.

-   Incremental data migration: After full data migration, incremental data is synchronized to the destination ApsaraDB for MongoDB instance.

    **Note:**

    -   The create and delete operations on databases, collections, and indexes can also be synchronized.
    -   The create, delete, and update operations on documents can be synchronized.

## Required database account permissions

|Database|Full data migration|Incremental data migration|
|:-------|:------------------|--------------------------|
|Source self-managed MongoDB database|Read permissions on the source database|Read permissions on the source database, admin database, and local database|
|Destination ApsaraDB for MongoDB instance|Read and write permissions on the destination ApsaraDB for MongoDB instance|Read and write permissions on the destination ApsaraDB for MongoDB instance|

-   For more information about how to create and authorize a database account for an ApsaraDB for MongoDB instance, see [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).
-   For more information about how to create and authorize a database account for a self-managed MongoDB database, see [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/).

## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the Migration Tasks section, select the region in which the destination ApsaraDB for MongoDB instance is deployed.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner, click **Create Migration Task**.
5.  Configure the source and destination databases.

    ![Configure the source and destination databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0034948951/p34129.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |None|Task Name|The name of the migration task. DTS automatically generates a task name. We recommend that you set a descriptive name that makes it easy to identify. Task names do not have to be unique.|
    |Source Database|Instance Type|The category of the source database. Select a category based on the location where the database resides. In this example, select **User-Created Database with Public IP Address**. **Note:** If you select other instance types, you must prepare the environment that is required for the source database. For more information, see [Preparation overview](). |
    |Instance Region|The region where the source database resides. If Instance Type is set to **User-Created Database with Public IP Address**, you do not need to set **Instance Region**. **Note:** If a whitelist is configured for the self-managed MongoDB database, you must add the CIDR blocks of DTS servers to the whitelist. You can click **Get IP Address Segment of DTS** next to **Instance Region** to obtain the CIDR blocks of DTS servers. |
    |Database Type|The database engine of the source database. In this example, select **MongoDB**.|
    |Hostname or IP Address|The endpoint or IP address of the self-managed database. In this example, enter the public IP address of the self-managed database.|
    |Port Number|The service port number for the self-managed database. **Note:** In this example, the service port of each shard for self-managed MongoDB database must be open to the Internet. |
    |Database Name|The name of the authentication database to which the database account belongs.|
    |Database Account|The account of the self-managed database. For more information about the permissions that are required for the account, see [Required database account permissions](#section_kvw_kb1_kfb).|
    |Database Password|The password of the source database account. **Note:** After you specify the source database information, click **Test Connectivity** next to **Database Password** to verify whether the information is valid. If the information is valid, the **Passed** message appears. If the information is invalid, the **Failed** message appears, and you must click **Check** next to the **Failed** message to modify the information. |
    |Connection method|Specifies whether to encrypt the connection. In this example, select **Non-encrypted**. **Note:** You can select **SSL-encrypted** only when you migrate data from MongoDB Atlas. |
    |Destination Database|Instance Type|The category of the destination instance. In this example, select **MongoDB Instance**.|
    |Instance Region|The region where the destination instance is deployed.|
    |MongoDB Instance ID|The ID of the destination instance.|
    |Database Name|The name of the authentication database to which the database account belongs. **Note:** If the database account is root, enter admin. |
    |Database Account|The account that is used to log on to the destination database. For more information about the permissions that are required for the account, see [Required database account permissions](#section_kvw_kb1_kfb).|
    |Database Password|The password of the destination database account. **Note:** After you specify the destination database information, click **Test Connectivity** next to **Database Password** to verify whether the information is valid. If the information is valid, the **Passed** message appears. If the information is invalid, the **Failed** message appears, and you must click **Check** next to the **Failed** message to modify the information. |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    **Note:** The CIDR blocks of DTS servers are automatically added to the whitelist of the destination ApsaraDB for MongoDB instance. This ensures that DTS servers can connect to the destination ApsaraDB for MongoDB instance. After the migration is complete, you can remove the CIDR blocks from the whitelist. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md).

7.  Select the migration types and objects to be migrated.

    ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2940421261/p38327.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   To perform only full data migration, select **Full Data Migration**.
    -   To migrate data with minimal downtime, select both **Full Data Migration** and **Incremental Data Migration**.
**Note:** If **Incremental Data Migration** is not selected, do not write data to the source MongoDB database when the migration is in progress. This can ensure data consistency. |
    |Migration objects|    -   Select objects from the **Available** section and click the ![Right arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p37966.png) icon to move the objects to the **Selected** section.

**Note:**

        -   Data in the admin and local databases cannot be migrated.
        -   The config database is an internal database. We recommend that you do not migrate data in the config database.
    -   A migration object can be a database, collection, or function.
    -   By default, the name of an object remains unchanged after migration. You can change the names of the objects in the destination instance by using the object name mapping feature. For more information, see [Object name mapping](https://www.alibabacloud.com/help/zh/doc-detail/26628.htm). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   A precheck is performed before the migration task starts. You can start the data migration task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Hint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and run the precheck again.
9.  After the task passes the precheck, click **Next**.
10. In the Confirm Settings dialog box, specify the **Channel Specification** parameter and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
11. Click **Buy and Start** to start the migration task.
    -   Full data migration

        Do not manually stop a task during full data migration. Otherwise, the system may fail to perform a full data migration. Wait until the full data migration task automatically stops.

    -   Incremental data migration

        An incremental data migration task does not automatically end. You must manually end the task.

        **Note:** Manually stop the migration task at an appropriate point of time. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the destination instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The latency time of **incremental data migration** may be displayed in the progress bar.
        2.  After the status of **Incremental Data Migration** changes to **The migration task is not delayed**, stop the migration task.

            ![No latency exists during incremental data migration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p33674.png)

12. Switch over your workloads to the destination ApsaraDB for MongoDB instance.

## References

[How do I connect to the replica set instance of ApsaraDB for MongoDB?]()

