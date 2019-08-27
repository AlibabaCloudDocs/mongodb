# Use DTS to migrate data {#concept_fdj_twz_zfb .concept}

When using [DTS](https://www.alibabacloud.com/help/zh/doc-detail/26592.htm) to migrate data, you cannot directly migrate data from the user-created database. However, you can migrate data from each shard in the user-created database to the cloud. With the incremental migration feature of DTS, you can migrate data to the cloud without stopping local application services.

## Prerequisites {#section_jx1_5wy_ngb .section}

-   Each shard of the user-created database has a public IP address or a port that is open to the public network.
-   The user-created database supports database versions 3.0, 3.2, 3.4, and 3.6. MongoDB 4.0 is not supported.

    **Note:** For more information about data migration in MongoDB 4.0, see [Use the built-in commands of MongoDB to migrate data](intl.en-US/Quick Start for Cluster/Migrate data/Use the built-in commands of MongoDB to migrate data.md#).

-   The storage space of the ApsaraDB for MongoDB instance should be larger than that of the user-created database.

## Precautions {#section_dww_lmr_zfb .section}

-   Data in the admin database cannot be migrated, even if it is selected.
-   The config database is an internal database. Do not migrate data from the config database unless otherwise required.
-   ApsaraDB for MongoDB supports database versions 3.4 and 4.0.
-   To avoid adverse impacts on your business, try to perform data migration during off-peak hours.

## Billing for data migration {#section_brm_q21_1gb .section}

|Migration type|Billing for link configuration|Billing for public traffic|
|:-------------|:-----------------------------|:-------------------------|
|Full data migration|Free|Free|
|Incremental data migration|Paid. For more information, see [DTS pricing](https://www.alibabacloud.com/zh/product/data-transmission-service/pricing).|Free|

## Migration type description {#section_zjf_5fs_zfb .section}

-   Full data migration: All existing data in the user-created database is migrated to the ApsaraDB for MongoDB instance. The following migration types are supported:
    -   Database migration
    -   Collection migration
    -   Index migration
-   Incremental data migration: Data that is updated in the user-created database is incrementally synchronized to the ApsaraDB for MongoDB instance. The following update operations are synchronized:
    -   Create and delete operations on databases
    -   Create, delete, and update operations on documents
    -   Create and delete operations on collections
    -   Create and delete operations on indexes

## Permission requirements for data migration {#section_mfq_xmr_zfb .section}

|Instance type|Full data migration|Incremental data migration|
|:------------|:------------------|:-------------------------|
|Local MongoDB instance|Read| -   Read permission on the database to be migrated
-   Read permission on the admin database
-   Read permission on the user-created database

 |
|ApsaraDB for MongoDB instance|Read/write|Read/write|

## Preparations before migration {#section_pcx_yhs_zfb .section}

To avoid adverse impacts on your business, try to perform data migration during off-peak hours.

1.  Disable the balancer of the user-created database. For more information, see [Disable MongoDB sharded cluster balancer](../../../../intl.en-US/Best Practices/Manage the ApsaraDB for MongoDB balancer.md#section_k3j_4wl_2gb).
2.  Clean up orphaned files in the user-created database to avoid block migration failure. For more information, see [CleanupOrphaned](https://docs.mongodb.com/manual/reference/command/cleanupOrphaned/).

    Example:

    For some shard, clean up all orphaned files from the user collection of the test database.

    ``` {#codeblock_dkb_lkl_3um}
    var nextKey = { };
    var result;
    
    while ( nextKey ! = null ) {
      result = db.adminCommand( { cleanupOrphaned: "test.user", startingFromKey: nextKey } );
    
      if (result.ok ! = 1)
         print("Unable to complete at this time: failure or timeout.")
    
      printjson(result);
    
      nextKey = result.stoppedAtKey;
    }
    ```

    **Note:** 

    -   You must perform this operation on each shard.
    -   If any orphaned files remain, there may be ID conflicts between migrated files and the migration performance may be affected.
3.  Configure data shards based on business needs. For more information, see [Configure data shards](../../../../intl.en-US/Best Practices/Configure sharding to maximize the performance of shards.md#) \(optional\).

    **Note:** Before migration, you can create a database and collection for which to configure data shards. You can also configure data shards after migration.


## Migration procedure {#section_lnt_knr_zfb .section}

1.  Log on to the [Data Transmission Service console](https://dts-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the upper-right corner of the Data Migration page, click **Create Migration Task**.
4.  Configure the parameters of **Source Database and Destination Database**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156455452334677_en-US.png)

    |Parameters of source and destination databases|
    |:---------------------------------------------|
    |Task Name|     -   DTS automatically generates a name for every task. Task names do not need to be unique.
    -   You can modify task names as required. We recommend that you choose appropriate task names to easily identify tasks later.
 |
    |Source Database|     -   Instance Type: Select **User-Created Database with Public IP Address**.
    -   Instance Region: Select the region where the source MongoDB database is located.
    -   Database Type: Select **MongoDB**.
    -   Hostname or IP Address: the domain name or IP address of a single shard.

**Note:** DTS migrates data from every shard in the sharded cluster instance in sequence. Enter the domain name or IP address of the first shard here. When you create a second migration task later, enter the domain name or IP address of the second shard. Repeat this until all shards are migrated.

    -   Database Name: the name of the authentication database for the source MongoDB database.
    -   Database Account: the account used to log on to the source MongoDB database. For more information about permission requirements, see [Permission requirements for data migration](#).
    -   Database Password: the password used to log on to the source MongoDB database.
 |
    |Destination Database|     -   Instance Type: Select **MongoDB Instance**.
    -   Instance Region: Select the region where the destination MongoDB database is located.
    -   MongoDB Instance ID: Select the ID of a sharded cluster instance.
    -   Database Name: the name of the authentication database for the destination MongoDB database. The default database name is admin.
    -   Database Account: the account used to log on to the destination MongoDB database. For more information about permission requirements, see [Permission requirements for data migration](#).
    -   Database Password: the password used to log on to the destination MongoDB database.
 |

    **Note:** If the DTS server is not authorized to access the user-created database, you must grant access permission to the user-created database first. For more information, click **Get IP Address Segment of DTS** on the Source Database and Destination Database page.

5.  After you configure the parameters, click **Set Whitelist and Next** in the lower-right corner.

    You must add the public IP address of the DTS server to the whitelist of the destination MongoDB database to ensure the server can connect to the database. The public IP address of the DTS server can be removed from the whitelist after migration. For more information, see [Configure a whitelist](../../../../intl.en-US/User Guide/Data security/Configure a whitelist.md#).

6.  Select **Migration Objects** and **Migration Types**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156455452334699_en-US.png)

    |Configure the migration object and migration type|
    |:------------------------------------------------|
    |Migration type|     -   If you want to migrate all data, select **Full Data Migration**.

**Note:** To ensure data consistency, do not write new data to the source MongoDB database when a full migration is being performed.

    -   If live migration is required, select both **Full Data Migration** and **Incremental Data Migration**.
 |
    |Migration object|     -   Select the database to be migrated from the **Available** list and click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156455452348344_en-US.png) to move it to the **Selected** list.

**Note:** 

        -   Data in the admin database cannot be migrated, even if it is selected.
        -   The config database is an internal database. Do not migrate data from the config database unless otherwise required.
    -   The migration object can be a database or a collection.
    -   The object name will remain the same after it is migrated to the destination MongoDB instance as it was in the source MongoDB instance by default.

**Note:** 

        -   Each shard may store different data than other shards or contain only a portion of the whole database. This is determined by the characteristics of the shard. When you perform a data migration, you must select which data is to be migrated.
        -   If the object you migrate has different names in the source and destination instances, you must use the object name mapping feature provided by DTS. For more information, see [Object name mapping](https://www.alibabacloud.com/help/doc-detail/26628.htm).
 |

7.  After you configure the preceding settings, click **Pre-check**.

    **Note:** 

    -   A pre-check is performed before a migration task is formally started. Migration can be started only after a successful pre-check.
    -   If the pre-check fails, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156455452448342_en-US.png) icon after each check item to view the failure details. Perform the pre-check again after you have rectified the failed items.
8.  After the pre-check is successful, click **Next**.
9.  On the **Confirm Purchase Configuration** page, select **Link Type** and **Data Transmission \(Pay-As-You-Go\) Service Terms**.
10. Click **Buy and Start** to start the migration task.
    -   Full data migration

        Wait until the migration task stops automatically.

    -   Incremental data migration

        When the status of the migration task becomes **Incremental migration without delay**, it indicates that the data has been synchronized.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156455452434686_en-US.png)

11. Repeat Steps 1 through 10 to create migration tasks for other shards and wait until all migration tasks are complete.

    **Note:** 

    1.  The incremental migration task does not end automatically. You can click **Refresh** to view the latest status of the migration task. When the migration tasks of all shards are **Incremental migration without delay**, stop the source database for several minutes.
    2.  When the migration tasks of all shards become **Incremental migration without delay** again, stop the migration task.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156455452434689_en-US.png)


Check whether the data is correct. If yes, you can switch your business from the user-created database to the ApsaraDB for MongoDB instance.

