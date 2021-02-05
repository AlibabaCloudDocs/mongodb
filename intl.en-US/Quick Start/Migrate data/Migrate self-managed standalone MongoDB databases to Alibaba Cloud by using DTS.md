# Migrate self-managed standalone MongoDB databases to Alibaba Cloud by using DTS

This topic describes how to use Data Transmission Service \(DTS\) to migrate data from standalone self-managed MongoDB databases to Alibaba Cloud. DTS supports full data migration and incremental data migration. The data migration does not interrupt your services if you select the two migration types.

You can also use the built-in commands of MongoDB to migrate self-managed MongoDB databases. For more information, see [Migrate self-managed MongoDB databases to standalone instances by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate self-managed MongoDB databases to standalone instances by using tools provided
         by MongoDB.md).

For more information about data migration or synchronization solutions, see [Overview](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).

## Prerequisites

-   The version of the self-managed MongoDB database is 3.0, 3.2, 3.4, 4,0, or 4.2.
-   The storage space of the ApsaraDB for MongoDB instance is larger than the size of the self-managed MongoDB database.

## Precautions

-   To avoid service disruptions, we recommend that you migrate data during off-peak hours.
-   If the source self-managed MongoDB database and the destination ApsaraDB for MongoDB instance run different MongoDB versions or storage engines, make sure that your applications can run on both databases. For more information about MongoDB versions and storage engines that are supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).
-   To migrate incremental data from a standalone self-managed MongoDB database, you must enable the oplog feature for the database. For more information, see [Preparations for incremental data migration](#section_l3m_8mq_6gb).

## Billing

|Migration type|Instance configuration|Internet traffic|
|--------------|----------------------|----------------|
|Full data migration|Free of charge.|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, see [Pricing]().|
|Incremental data migration|Charged. For more information, see [Pricing]().|

## Migration types

-   Full data migration: All historical data in the source instance is migrated from the source instance to the destination instance.

    **Note:** Data migration is supported at the database, collection, and index levels.

-   Incremental data migration: After full data migration, incremental data is synchronized to the destination instance.

    **Note:**

    -   The create and delete operations on databases, collections, and indexes can also be synchronized.
    -   The create, delete, and update operations on documents can be synchronized.

## Permissions required for database accounts

|Database|Full data migration|Incremental data migration|
|:-------|:------------------|--------------------------|
|Source self-managed MongoDB database|Read permissions on the source database|Read permissions on the source database, admin database, and local database|
|Destination ApsaraDB for MongoDB instance|Read/write permissions on the destination database|Read/write permissions on the destination database|

How to create and authorize a database account:

-   For a self-managed MongoDB database, see [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/).
-   For ApsaraDB for MongoDB instances, see [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).

## Preparations for incremental data migration

Before you use DTS to migrate incremental data, enable the oplog feature for the source database. If you only perform only full data migration, skip the following steps.

**Note:** This operation restarts the MongoDB database. We recommend that you perform this operation during off-peak hours.

1.  Use Mongo Shell to connect to the self-managed MongoDB database.

2.  Run the following commands to shut down the MongoDB database:

    ```
    use admin
    db.shutdownServer()
    ```

3.  Run the following command to start the MongoDB service from the backend as a replica set:

    ```
    mongod --port 27017 --dbpath /var/lib/mongodb --logpath /var/log/mongodb/mongod.log --replSet rs0 --bind_ip 0.0.0.0 --auth --fork
    ```

    **Note:**

    -   The database path used by the preceding command is /var/lib/mongodb. The log file path is /var/log/mongodb/mongod.log. Specify the paths based on business needs.
    -   This command uses 0.0.0.0 as the associated IP address of the MongoDB database. This allows you to access the database by using all IP addresses. After the migration is complete, run the `kill` command to terminate the process, and start the MongoDB database by using the original configuration file.
    -   This command enables authentication. You can access the database only after you pass the authentication.
4.  Use Mongo Shell to reconnect to the self-managed MongoDB database.

5.  Run the following commands to initialize the replica set:

    ```
    use admin
    rs.initiate()
    ```

6.  The role of the current node changes to primary.

    **Note:** You can run the `rs.printReplicationInfo()` command to view the status of oplog.


## Procedure

1.  Log on to the[DTS console](https://dts-intl.console.aliyun.com/).

2.  In the left-side navigation pane, click **Data Migration**.

3.  In the upper part of the Migration Tasks page, select the region where the ApsaraDB for MongoDB instance is deployed.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner of the page, click **Create Migration Task**.

5.  Configure the source and destination databases.

    ![Configure the source and destination databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0034948951/p34129.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|DTS automatically generates a task name. We recommend that you specify an informative name for easy identification. You do not need to use a unique task name.|
    |Source Database|Instance Type|Select an instance type based on the deployment of the source database. In this example, select **Self-Managed Database with Public IP Address**. **Note:** If you select other instance types, you must prepare the environment that is required for the source database. For more information, see [Preparation overview](). |
    |Instance Region|If Instance Type is set to **User-Created Database with Public IP Address**, you do not need to specify the **Instance Region** parameter. **Note:** If you have configured a whitelist for the self-managed MongoDB database, you must add the CIDR blocks of DTS servers to the whitelist. You can click **Get IP Address Segment of DTS** next to **Instance Region** to obtain the CIDR blocks of DTS servers. |
    |Database Type|Select **MongoDB**.|
    |Hostname or IP Address|Enter the endpoint that is used to connect to the self-managed MongoDB database. In this example, enter the public IP address.|
    |Port Number|Enter the service port of the self-managed MongoDB database. **Note:** In this example, the service port of the self-managed MongoDB database must be accessible over the Internet. |
    |Database Name|Enter the name of the authentication database to which the database account belongs.|
    |Database Account|Enter the username of the database account used to manage the source database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_usd_r1p_kp5).|
    |Database Password|Enter the password of the database account. **Note:** After you specify the source database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the information is correct, the **Passed** message is displayed. If the **Failed** message is displayed, click **Check** in the **Failed** message to modify the information. |
    |Connection Method|Select **Non-encrypted**. **Note:** The **SSL-encrypted** option is available only when you migrate MongoDB Atlas. |
    |Destination Database|Instance Type|The type of the instance. In this example, select **MongoDB Instance**.|
    |Instance Region|The region where the ApsaraDB for MongoDB instance is deployed.|
    |MongoDB Instance ID|Select the ID of the ApsaraDB for MongoDB database.|
    |Database Name|Enter the name of the authentication database to which the database account belongs. **Note:** If you want to use the root account, specify admin for the Database Name parameter. |
    |Database Account|Enter the username of the database account used to manage the source database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_usd_r1p_kp5).|
    |Database Password|Enter the password of the database account. **Note:** After you specify the destination database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the information is correct, the **Passed** message is displayed. If the **Failed** message is displayed, click **Check** next to the **Failed** message to modify the information. |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    **Note:** The IP addresses of the DTS servers are automatically added to a whitelist of the destination ApsaraDB for MongoDB instance. This ensures that the DTS servers can connect to the instance. After the migration is complete, you can remove these CIDR blocks from the whitelist. For more information, see [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md).

7.  Configure migration types and objects to be migrated.

    ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8924948951/p38327.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|    -   To perform only full data migration, select **Full Data Migration**.
    -   To migrate data with minimal downtime, select both **Full Data Migration** and **Incremental Data Migration**.

**Note:**

        -   Before you migrate incremental data from a standalone self-managed MongoDB database, you must enable oplog for the database. For more information, see [Preparations for incremental data migration](#section_l3m_8mq_6gb).
        -   If the **Incremental Data Migration** option is not selected, do not write new data to the self-managed MongoDB database when full data migration is in progress. Otherwise, data inconsistency may occur. |
    |Migration objects|    -   Select objects from the **Available** section and click the ![Right arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to move the objects to the **Selected** section.

**Note:**

        -   Data in the admin and local databases cannot be migrated.
        -   The config database is an internal database. We recommend that you do not migrate data in the config database.
    -   A migration object can be a database, collection, or function.
    -   By default, after an object is migrated to the destination database, the name of the object remains unchanged. You can use the object name mapping feature to change the names of the objects that are migrated to the destination database. For more information, see[Object name mapping](https://www.alibabacloud.com/help/doc-detail/26628.htm). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   A precheck is performed before the migration task starts. You can start the data migration task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and perform a precheck again.
9.  After the task passes the precheck, click **Next**.

10. In the Confirm Settings dialog box, specify the **Channel Specification** parameter and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.

11. Click **Buy and Start** to start the migration task.

    -   Full data migration

        Do not manually stop a task during full data migration. Otherwise, the system may fail to perform a full data migration. Wait until the full data migration task automatically stops.

    -   Incremental data migration

        An incremental data migration task does not automatically stop. You must manually stop the migration task.

        **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the ApsaraDB for MongoDB instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **Incremental Data Migration** may appear in the progress bar.
        2.  After the status of **Incremental Data Migration** changes to **The migration task is not delayed**, stop the migration task.

            ![No delay exists during incremental data migration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p33674.png)

12. Switch your workloads to the ApsaraDB for MongoDB instance.


