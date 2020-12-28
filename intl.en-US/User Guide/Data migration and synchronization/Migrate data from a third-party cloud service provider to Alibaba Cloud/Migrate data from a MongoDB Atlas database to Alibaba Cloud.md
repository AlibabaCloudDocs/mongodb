# Migrate data from a MongoDB Atlas database to Alibaba Cloud

This topic describes how to migrate incremental data from a MongoDB Atlas database to Alibaba Cloud by using Data Transmission Service \(DTS\). DTS supports full data migration and incremental data migration. When you migrate data from a MongoDB Atlas database, you can select both migration types to ensure service continuity.

The available storage space of the destination ApsaraDB for MongoDB instance is larger than the total size of the data in the MongoDB Atlas database.

## Precautions

-   DTS uses resources of the source and destination instances during full data migration. This may increase the loads of the database servers. If you migrate a large volume of data or the server specifications cannot meet your requirements, database services may become unavailable. Before you migrate data, evaluate the impact of data migration on the performance of the source and destination databases. We recommend that you migrate data during off-peak hours.
-   You cannot migrate data from the admin or local database.
-   The config database is an internal database. We recommend that you do not migrate this database.
-   If the source MongoDB Atlas database and the destination ApsaraDB for MongoDB instance have different versions or storage engines, make sure that the versions or storage engines are compatible. For more information, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## Billing

|Migration type|Instance configuration fee|Internet traffic fee|
|--------------|--------------------------|--------------------|
|Full data migration|Free of charge|Charged only when data is migrated from Alibaba Cloud over the Internet. For more information, see [Pricing]().|
|Incremental data migration|Charged. For more information, see [Pricing]().|

## Migration types

|Migration type|Description|
|--------------|-----------|
|Full data migration|DTS migrates all historical data of the required objects from the source MongoDB database to the destination MongoDB database. **Note:** The following types of objects are supported: database, collection, and index. |
|Incremental data migration|After full data migration is complete, DTS synchronizes incremental data from the source MongoDB database to the destination MongoDB database. **Note:**

-   The create and delete operations that are performed on databases, collections, and indexes can be synchronized.
-   The create, delete, and update operations that are performed on documents can be synchronized. |

## Permissions required for database accounts

|Database|Full data migration|Incremental data migration|
|:-------|:------------------|--------------------------|
|MongoDB Atlas database|The read permission on the source database and the permission to perform the listDatabases operation|-   The read permission on the source database, admin database, and local database
-   The permission to perform the listDatabases operation |
|ApsaraDB for MongoDB instance|The read and write permissions on the destination database|The read and write permissions on the destination database.|

For more information about how to create and authorize a database account, see the following topics:

-   MongoDB Atlas database: [Create User in MongoDB](https://docs.mongodb.com/manual/reference/method/db.createUser/)
-   ApsaraDB for MongoDB instance: [Manage MongoDB users through DMS](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md)

## Before you begin

1.  Log on to the MongoDB Atlas console.

2.  In the left-side navigation pane, click **Network Access**. On the page that appears, click **ADD IP ADDRESS**.

    ![Create an Atlas whitelist](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p65819.png)

3.  In the dialog box that appears, click **ALLOW ACCESS FROM ANYWHERE**, and click **Confirm**.

    ![Configure an Atlas whitelist](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p65820.png)

    **Note:** This step allows all IP addresses to access the MongoDB Atlas database. Delete this rule after data migration is complete.


## Procedure

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com/).

2.  In the left-side navigation pane, click **Data Migration**.

3.  At the top of the Migration Tasks page, select the region where the ApsaraDB for MongoDB instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p50190.png)

4.  In the upper-right corner of the page, click **Create Migration Task**.

5.  Configure the source and destination databases.

    ![Configure the source and destination databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6535298951/p65834.png)

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |N/A|Task Name|DTS automatically generates a task name. We recommend that you specify an informative name for easy identification. You do not need to use a unique task name.|
    |Source Database|Instance Type|Select **User-Created Database with Public IP Address**.|
    |Instance Region|If the instance type is set to **User-Created Database with Public IP Address**, you do not need to specify the **instance region**.|
    |Database Type|Select **MongoDB**.|
    |Hostname or IP Address|Enter the endpoint of the PRIMARY node in the MongoDB Atlas database.

 You can obtain the endpoint in the MongoDB Atlas console, as shown in the following figure.

 ![Obtain the Atlas endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p65835.gif) |
    |Port Number|Enter the service port number of the MongoDB Atlas database. The default port number is **27017**.|
    |Database Name|Enter the name of the authentication database. The database account is created in this database.|
    |Database Account|Enter the account of the MongoDB Atlas database. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_b6u_wl6_su6).|
    |Database Password|Enter the password of the database account. **Note:** After you specify the source database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the source database parameters based on the check results. |
    |Encryption|Select **SSL-encrypted**.|
    |Destination Database|Instance Type|Select **MongoDB Instance**.|
    |Instance Region|Select the region where the ApsaraDB for MongoDB instance resides.|
    |MongoDB Instance ID|Select the ID of the ApsaraDB for MongoDB instance.|
    |Database Name|Enter the name of the authentication database. The database account is created in this database. **Note:** If the database account is root, enter admin. |
    |Database Account|Enter the database account of the ApsaraDB for MongoDB instance. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_b6u_wl6_su6).|
    |Database Password|Enter the password of the destination database account. **Note:** After you specify the destination database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the destination database parameters based on the check results. |

6.  In the lower-right corner of the page, click **Set Whitelist and Next**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p65836.png)

    **Note:** DTS adds the CIDR blocks of DTS servers to the whitelist of the ApsaraDB for MongoDB instance. This ensures that DTS servers can connect to the ApsaraDB for MongoDB instance.

7.  Select the migration types and the objects to be migrated.

    |Setting|Description|
    |-------|-----------|
    |Select the migration types|    -   To perform only full data migration, select only **Full Data Migration**.
    -   To ensure service continuity during data migration, select both **Full Data Migration** and **Incremental Data Migration**.
 **Note:** If **Incremental Data Migration** is not selected, do not write data to the source database during full data migration. This ensures data consistency between the source and destination databases. |
    |Select the objects to be migrated|    -   Select objects from the **Available** section and click the ![Right arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p37966.png) icon to move the objects to the **Selected** section.

**Note:** You cannot migrate data from the admin or local database.

    -   You can select databases, collections, or functions as the objects to be migrated.
    -   After an object is migrated to the destination database, the name of the object remains unchanged. You can use the object name mapping feature to change the names of the objects that are migrated to the ApsaraDB for MongoDB instance. For more information, see [Object name mapping](~~26628~~). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   Before you can start the data migration task, a precheck is performed. You can start the data migration task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and run the precheck again.
9.  After the task passes the precheck, click **Next**.

10. In the **Confirm Settings** dialog box, specify the **Channel Specification** parameter and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.

11. Click **Buy and Start** to start the migration task.

    -   Full data migration

        We recommend that you do not manually stop a migration task. Otherwise, data migrated to the destination database will be incomplete. Wait until the data migration task automatically stops.

    -   Incremental data migration

        An incremental data migration task does not automatically stop. You must manually stop the migration task.

        **Note:** Select an appropriate time to manually stop the migration task. For example, you can stop the migration task during off-peak hours or before you switch your workloads to the ApsaraDB for MongoDB instance.

        1.  Wait until **Incremental Data Migration** and **The migration task is not delayed** appear in the progress bar of the migration task. Then, stop writing data to the source database for a few minutes. The delay time of **incremental data migration** may be displayed in the progress bar.
        2.  After the status of **incremental data migration** changes to **The migration task is not delayed**, manually stop the migration task.

            ![Incremental data migration without delay](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p33674.png)

12. Switch your workloads to the ApsaraDB for MongoDB instance.


