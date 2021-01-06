# Migrate data from a standalone MongoDB instance to a replica set or sharded cluster instance

ApsaraDB for MongoDB provides standalone instances, replica set instances, and sharded cluster instances. Standalone instances are designed to store non-core enterprise data, for example, in development and testing scenarios. Replica set instances and sharded cluster instances are more suitable for production scenarios. This topic describes how to migrate data from a standalone instance to a replica set instance or a sharded cluster instance by using Data Transmission Service \(DTS\).

The available storage space of the destination instance is larger than the total size of the data in the source instance.

## Precautions

-   During full data migration, DTS uses read and write resources of the source and destination databases. This may increase the load of the database server. If you migrate a large volume of data or the server specifications cannot meet your requirements, database services may become unavailable. Before you migrate data, evaluate the impact of data migration on the performance of the source and destination databases. We recommend that you migrate data during off-peak hours.
-   DTS does not support incremental data migration from a standalone instance. To ensure data consistency, do not write data to the source instance during full data migration.
-   If the source and destination ApsaraDB for MongoDB instances have different versions or storage engines, make sure that the versions or storage engines are compatible. For more information, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).
-   If the minor version of your instance expires or is not included in the maintenance list and the instance is upgraded, migrated, changed, or cloned, the system will upgrade the minor version to the latest version by default. This ensures better performance and stability of the instance.

## Billing

|Migration type|Instance configuration|Internet traffic|
|:-------------|:---------------------|:---------------|
|Full data migration|Free of charge|Free of charge|

## Migration types

Full data migration: DTS migrates all historical data of the required objects from the source MongoDB database to the destination MongoDB database.

**Note:** The following types of objects are supported: database, collection, and index.

## Permissions required for database accounts

|Instance|Permission|
|:-------|:---------|
|Source ApsaraDB for MongoDB instance|The read permission on the source database|
|Destination ApsaraDB for MongoDB instance|The read/write permissions on the destination database|

For more information about how to create and authorize a database account, see [Use DMS to manage MongoDB users](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).

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
    |Database Account|Enter the database account of the source ApsaraDB for MongoDB instance. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_atn_bv3_u7r).|
    |Database Password|Enter the password of the source database account. **Note:** After you specify the source database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the source database parameters based on the check results. |
    |Destination Database|Instance Type|Select **MongoDB Instance**.|
    |Instance Region|Select the region where the destination ApsaraDB for MongoDB instance resides.|
    |MongoDB Instance ID|Select the ID of the destination ApsaraDB for MongoDB instance.|
    |Database Name|Enter the name of the authentication database. The database account is created in this database. **Note:** If the database account is root, enter admin. |
    |Database Account|Enter the database account of the destination ApsaraDB for MongoDB instance. For more information about the permissions that are required for the account, see [Permissions required for database accounts](#section_atn_bv3_u7r).|
    |Database Password|Enter the password of the destination database account. **Note:** After you specify the destination database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the destination database parameters based on the check results. |

6.  In the lower-right corner, click **Set Whitelist and Next**.

    **Note:** DTS adds the CIDR blocks of DTS servers to the whitelists of the source and destination ApsaraDB for MongoDB instances. This ensures that DTS servers can connect to the source and destination ApsaraDB for MongoDB instances. After data migration is complete, you can remove the CIDR blocks of DTS servers from the whitelists. For more information, see [Configure a whitelist for a sharded cluster instance]().

7.  Select the migration types and objects to be migrated.

    ![Select the migration types and objects to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5435298951/p35725.png)

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|Select **Full Data Migration**. **Note:** If the data source is a standalone instance, you can select only **Full Data Migration**. To ensure data consistency, do not write data to the source instance during full data migration. |
    |Objects|    -   Select objects from the **Available** section and click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p37966.png) icon to move the objects to the **Selected** section.

**Note:** You cannot migrate data from the admin or local database.

    -   You can select databases, collections, or functions as the objects to be migrated.
    -   After an object is migrated to the destination instance, the name of the object remains unchanged. You can change the names of the objects that are migrated to the destination instance by using the object name mapping feature. For more information about how to use this feature, see [Object name mapping](https://www.alibabacloud.com/help/doc-detail/26628.htm). |

8.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   Before you can start the data migration task, a precheck is performed. You can start the data migration task only after the task passes the precheck.
    -   If the task fails to pass the precheck, click the ![Info icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7535298951/p50068.png) icon next to each failed item to view details. Troubleshoot the issues based on the causes and run the precheck again.
9.  After the task passes the precheck, click **Next**.

10. In the **Confirm Settings** dialog box, specify the **Channel Specification** and select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**.

11. Click **Buy and Start** to start the data migration task.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6435298951/p51339.png)

    **Note:** We recommend that you do not manually stop a data migration task. Otherwise, data migrated to the destination instance will be incomplete. Wait until the data migration task automatically stops.

12. Switch your workloads to the destination ApsaraDB for MongoDB instance.


## References

-   [Overview of replica set instance connections]()
-   [Overview of sharded cluster instance connections]()
-   [Configure sharding to maximize the performance of shards](/intl.en-US/Best Practices/Performance/Configure sharding to maximize the performance of shards.md)

