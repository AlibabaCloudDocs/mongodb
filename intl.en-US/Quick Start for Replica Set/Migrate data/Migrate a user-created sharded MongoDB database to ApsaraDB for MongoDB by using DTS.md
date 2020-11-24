# Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS

This topic describes how to migrate shards of a user-created sharded MongoDB database to ApsaraDB for MongoDB by using Data Transmission Service \(DTS\). DTS allows you to migrate historical and incremental data without service disruptions.

For more information about data migration and synchronization solutions, see [Overview of data migration and synchronization](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).

## Prerequisite

-   The version of the user-created MongoDB database is 3.0, 3.2, 3.4, 3.6, or 4.0.
-   Each shard in the destination sharded cluster instance has sufficient storage space.

    **Note:** For example, a user-created MongoDB database has three shards, and one of these shards occupies the maximum storage space of 500 GB. In this case, the storage space of each shard in destination instance must be greater than 500 GB.


## How it works

DTS migrates a user-created MongoDB database by migrating each shard in the instance. You must create a data migration task for each shard.

**Note:** The distribution of migrated data in the destination instance depends on the shard key that you specify. For more information, see [Configure sharding to maximize the performance of shards](/intl.en-US/Best Practices/Performance/Configure sharding to maximize the performance of shards.md).

![How it works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1435298951/p50227.png)

## Usage notes

-   DTS uses resources of the source and destination instances during full data migration. This may increase the load of the database server. If the data volume is large or the specification is low, the database server may become unavailable. We recommend that you migrate user-created MongoDB databases during off-peak hours.
-   If the source user-created MongoDB database and the destination ApsaraDB for MongoDB instance run different MongoDB versions or storage engines, ensure that your applications can run on both instances. For more information about MongoDB versions and storage engines that are supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## Billing information

|Migration type|Instance fee|Internet traffic fee|
|--------------|------------|--------------------|
|Full data migration|Free of charge|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, see [Data Transmission Service Pricing](https://www.alibabacloud.com/zh/product/data-transmission-service/pricing).|
|Incremental data migration|Charged. For more information, see[Data Transmission Service Pricing](https://www.alibabacloud.com/zh/product/data-transmission-service/pricing).|

## Migration types

-   Full data migration: All historical data in the source instance is migrated to the destination instance.

    **Note:** Data migration is supported at the database, collection, and index levels.

-   Incremental data migration: After full data migration, incremental data is synchronized to the destination instance.

    **Note:**

    -   The create and delete operations on databases, collections, and indexes can also be synchronized.
    -   The create, delete, and update operations on documents can be synchronized.

## Required database account permissions

|Data source|Support for full data migration|Support for incremental data migration|
|:----------|:------------------------------|--------------------------------------|
|Source user-created MongoDB database|Read permissions on the source database|Read permissions on the source database, admin database, and local database|
|Destination ApsaraDB for MongoDB instance|Read/write permissions on the destination database|Read/write permissions on the destination database|

How to create and authorize a database account:

-   For a user-created MongoDB database, see [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/).
-   For an ApsaraDB for MongoDB instance, see [Manage MongoDB users through DMS]().

## Prerequisites

1.  To avoid the impact of block migration on data consistency, you must disable the balancer of the user-created MongoDB databases during migration. For more information, see [Manage the ApsaraDB for MongoDB balancer](/intl.en-US/Best Practices/Manage the ApsaraDB for MongoDB balancer.md).

    **Warning:** If the balancer is not disabled, block migration will affect the consistency of the data read by DTS.

2.  Delete the orphaned documents generated due to migration failures from the user-created MongoDB database.

    **Note:** If the orphaned documents are not deleted, the documents with `_id` conflicts may exist during migration and unwanted data may be migrated.

    1.  Download the [cleanupOrphaned.js](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/120562/cn_zh/1564451237979/cleanupOrphaned.js) file.

        ```
        wget "http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/120562/cn_zh/1564451237979/cleanupOrphaned.js"
        ```

    2.  Replace `test` in the cleanupOrphaned.js file with the name of the database where you want to delete orphaned documents.

        **Note:** If you want to delete orphaned documents from multiple databases, repeat Steps ii and iii.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0034948951/p53814.png)

    3.  Run the following command on a shard to delete the orphaned documents from all collections in the specified database:

        **Note:** You must repeat this step on each shard.

        ```
        mongo --host <Shardhost> --port <Primaryport>  --authenticationDatabase <database> -u <username> -p <passowrd> cleanupOrphaned.js
        ```

        **Note:**

        -   <Shardhost\>: the IP address of the shard.
        -   <Primaryport\>: the service port of the primary node of the shard.
        -   <database\>: the database corresponding to the username and password if authentication is enabled.
        -   <username\>: the account used to log on to the user-created MongoDB database.
        -   <password\>: the password used to log on to the user-created MongoDB database.
        The following figure shows an example.

        In this example, a user-created MongoDB database has three shards, and you must delete the orphaned documents on each of the shards.

        ```
        mongo --host 172.16.1.10 --port 27018  --authenticationDatabase admin -u root -p 'Test123456' cleanupOrphaned.js
        ```

        ```
        mongo --host 172.16.1.11 --port 27021 --authenticationDatabase admin -u root -p 'Test123456' cleanupOrphaned.js
        ```

        ```
        mongo --host 172.16.1.12 --port 27024  --authenticationDatabase admin -u root -p 'Test123456' cleanupOrphaned.js
        ```

3.  Create required databases and collections in the destination sharded cluster instance, and configure data sharding for the databases and collections. For more information, see [Configure sharding to maximize the performance of shards](/intl.en-US/Best Practices/Performance/Configure sharding to maximize the performance of shards.md).

    **Note:** If you configure data sharding before you start data migration, data in the user-created MongoDB database is evenly migrated to the shards in the destination sharded cluster instance. This prevents overloading a single shard.


## Procedure

1.  Log on to the [Data Transmission Service console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the Migration Tasks section, select the region in which the ApsaraDB for MongoDB instance is deployed.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner, click **Create Migration Task**.
5.  Click Create Migration Task. In the Configure Source and Destination step, configure the source and destination databases for the migration task.

    ![Configure the source and destination databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0034948951/p34129.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|DTS automatically generates a task name. We recommend that you specify an informative name for easy identification. You do not need to use a unique task name.|
    |Source Database|Instance Type|Select an instance type based on the location where the database is deployed. In this topic, a **User-Created Database with Public IP Address** is used as an example. **Note:** If you select other instance types, you must prepare the environment that is required for the source database. For more information, see [Preparation overview](). |
    |Instance Region|If Instance Type is set to **User-Created Database with Public IP Address**, you do not need to specify the **Instance Region**. **Note:** If you have configured a whitelist for the user-created MongoDB database, you must add the CIDR blocks of DTS servers to the whitelist. You can click **Get IP Address Segment of DTS** next to **Instance Region** to obtain the CIDR blocks of DTS servers. |
    |Database Type|Select **MongoDB**.|
    |Hostname or IP Address|Enter the endpoint of a shard for the source database. In this example, enter the public IP address of the shard. **Note:** DTS migrates each shard of the source database in turn. In this example, enter the endpoint of the first shard. Then enter the endpoint of the second shard in the second migration task. Repeat this until all shards are migrated. |
    |Port Number|Enter the service port of the shard. **Note:** The service port of each shard for user-created MongoDB database must be open to the public network. |
    |Database Name|Enter the name of the authentication database to which the database account belongs.|
    |Database Account|Enter the username of the database account used to manage the source database. For more information about the permissions that are required for the account, see [Required database account permissions](#section_kvw_kb1_kfb).|
    |Database Password|Enter the password of the destination database account. **Note:** After you specify the source database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message is displayed. If the **Failed** message is displayed, click **Check** in the **Failed** message to modify the information as prompted. |
    |Encryption|Select **Non-encrypted**. **Note:** The **SSL-encrypted** option is available only when you migrate MongoDB Atlas. |
    |Destination Database|Instance Type|The type of the instance. In this example, select **MongoDB Instance**.|
    |Instance Region|The region where the ApsaraDB for MongoDB instance resides.|
    |MongoDB Instance ID|Select the ID of the ApsaraDB for MongoDB instance.|
    |Database Name|Enter the name of the authentication database to which the database account belongs. **Note:** If you want to use the root account, specify admin for the Database Name parameter. |
    |Database Account|Enter the username of the database account used to manage the source database. For more information about the permissions that are required for the account, see [Required database account permissions](#section_kvw_kb1_kfb).|
    |Database Password|Enter the password of the destination database account. **Note:** After you specify the destination database information, click **Test Connectivity** next to **Database Password** to check whether the information is correct. If the information is correct, the **Passed** message is displayed. If the information is incorrect, the **Failed** message is displayed, and you must click **Check** next to the **Failed** message to modify the information as prompted. |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    **Note:** The CIDR blocks of DTS servers are automatically added to the whitelist of the destination ApsaraDB for MongoDB instance. This ensures that DTS servers can connect to the destination ApsaraDB for MongoDB instance. After the migration is completed, you can remove these CIDR blocks from the whitelist. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

7.  Select the migration types and objects to be migrated.

    ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0034948951/p34699.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   To perform only full data migration, select **Full Data Migration**.
    -   To migrate data with minimal downtime, select both **Full Data Migration** and **Incremental Data Migration**.
 **Note:** If the **Incremental Data Migration** option is not selected, do not write new data to the user-created MongoDB database when full data migration is in progress. Otherwise, data inconsistency may occur. |
    |Migration objects|    -   Select objects from the **Available** section and click the ![Right arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p37966.png) icon to move the objects to the **Selected** section.

**Note:**

        -   Data in the admin and local databases cannot be migrated.
        -   The config database is an internal database. We recommend that you do not migrate data in the config database.
    -   A migration object can be a database, collection, or function.
    -   By default, the name of an object remains unchanged after migration. You can change the names of the objects in the destination RDS instance by using the object name mapping feature. For more information, see [Object name mapping](https://www.alibabacloud.com/help/doc-detail/26628.htm). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   A precheck is performed before the migration task starts. You can start the data migration task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and run the precheck again.
9.  After the task passes the precheck, click **Next**.
10. In the **Confirm Settings** dialog box, specify the **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.
11. Click **Buy and Start** to start the migration task.
12. Repeat Steps 1 to 11 to create data migration tasks for the remaining shards.
13. Stop the data migration task.
    -   Full data migration

        Do not manually stop a task during full data migration. Otherwise, the system may fail to perform a full data migration. Wait until the data migration task automatically stops.

    -   Incremental data migration

        An incremental data migration task does not automatically stop. You must manually stop the migration task.

        **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the destination instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **incremental data migration** may be displayed in the progress bar.
        2.  After the status of **Incremental Data Migration** changes to **The migration task is not delayed**, stop the migration task.

            ![Stop a migration task](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1435298951/p34689.png)

14. Switch over your business to the destination ApsaraDB for MongoDB instance.

