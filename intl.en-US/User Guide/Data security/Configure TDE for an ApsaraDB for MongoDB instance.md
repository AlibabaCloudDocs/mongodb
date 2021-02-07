# Configure TDE for an ApsaraDB for MongoDB instance

This topic describes how to configure Transparent Data Encryption \(TDE\) for an ApsaraDB for MongoDB instance. Before data files are written to disks, TDE encrypts the data files. When data files are loaded from disks to the memory, TDE decrypts the data files. TDE does not increase the sizes of data files. When you use TDE, you do not need to modify your application that uses the ApsaraDB for MongoDB instance. You can enable TDE for an instance in the ApsaraDB for MongoDB console to improve data security.

-   A replica set or sharded cluster instance is used.
-   The storage engine of the instance is WiredTiger.
-   The database engine version of the instance is MongoDB 4.0 or 4.2. If the database engine version of the instance is earlier than MongoDB 4.0, upgrade the database version. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md).

    **Note:** Before you enable TDE, you can create a pay-as-you-go instance of MongoDB 4.0 or 4.2 to test the compatibility between your application and the database version. You can release the instance after you complete the test.


If the architecture or storage engine of your instance does not meet the requirements, you can create an instance that meets the requirements and migrate data of your instance to the new instance. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Notes

-   When you enable TDE, your instance is restarted, and your application is disconnected from the instance. We recommend that you enable TDE during off-peak hours and make sure that your application can reconnect to the instance after it is disconnected.
-   TDE increases the CPU usage of your instance.
-   You cannot [restore TDE-encrypted collections to a user-created ApsaraDB for MongoDB database from physical backup files](/intl.en-US/User Guide/Data recovery/Recover physical backup data in a user-created MongoDB instance/Restore data of an ApsaraDB for MongoDB instance to a self-managed MongoDB database
         by using physical backup.md). To restore TDE-encrypted collections to a user-created ApsaraDB for MongoDB database, [use logical backup files](/intl.en-US/User Guide/Data recovery/Restore data of an ApsaraDB for MongoDB instance to self-managed MongoDB databases
         by using logical backup.md).

## Precautions

-   After you enable TDE, you cannot disable TDE.
-   You can enable TDE for an instance. You can also enable or disable encryption for a collection. If you need a filed-level encryption, see [Explicit \(Manual\) Client-Side Field Level Encryption](https://docs.mongodb.com/manual/core/security-explicit-client-side-encryption/) \(only available on MongoDB 4.2 instances\).

    **Note:** When you create a collection, you can disable encryption for the collection. For more information, see [Disable encryption for a specified collection](#section_1ip_yvb_vv4).

-   After you enable TDE, only new collections are encrypted. Existing collections are not encrypted.
-   [Key Management Service \(KMS\)](https://www.alibabacloud.com/help/zh/doc-detail/28935.htm) generates and manages the keys used by TDE. ApsaraDB for MongoDB does not provide keys or certificates required for encryption.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **TDE**.

6.  Turn on the switch next to **TDE Status:** to enable TDE.

    ![TDE](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8347559951/p56526.png)

7.  In the **Enable TDE** dialog box, you can select **Use Automatically Generated Key** or **Use Custom Key**. Then, click **OK**. The instance status changes to **Modifying TDE**. After the status changes to **Running**, TDE is enabled.

    **Note:** You can use KMS to manage custom keys. For more information, see [KMS](https://www.alibabacloud.com/help/zh/doc-detail/28935.htm).


## Disable encryption for a specified collection

After you enable TDE, all new collections are encrypted. When you create a collection, you can perform the following steps to disable encyption for the collection:

1.  Connect to your instance through the mongo shell. For more information, see [Connect to a replica set instance](/intl.en-US/Quick Start/Connect to an instance/Connect to a replica set instance by using the mongo shell.md) or [Connect to a sharded cluster instance](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md).

2.  Run the following command to create a collection and disable the encryption feature:

    ```
    db.createCollection("<collection_name>",{ storageEngine: { wiredTiger: { configString: "encryption=(name=none)" } } })
    ```

    **Note:** <collection\_name\>: the name of the collection.

    Example:

    ```
    db.createCollection("customer",{ storageEngine: { wiredTiger: { configString: "encryption=(name=none)" } } })
    ```


