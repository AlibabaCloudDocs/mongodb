# Configure automatic backup for an ApsaraDB for MongoDB instance

This topic describes how to configure automatic backup for an ApsaraDB for MongoDB instance. ApsaraDB for MongoDB can automatically back up data based on the default backup policy or the backup policy you specify.

## Usage notes

-   If the database version of an instance is 3.2 or 3.4, the number of collections and indexes in the instance cannot exceed 10,000. Otherwise, physical backup may fail. If you want to increase this limit, we recommend that you upgrade MongoDB versions to 4.0 or later. Alternatively, you can select the database version 4.0 or 4.2 when you create the instance. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md).
-   After the database version is upgraded, the backup files of the original version cannot be used to restore data of the new version.

## Automatic backup

-   ApsaraDB for MongoDB stores backup files in [Object Storage Service](~~31817~~) \(OSS\) to reduce the storage usage of ApsaraDB for MongoDB instances.
-   Standalone instances can use only snapshot backup, which affects their I/O performance in the backup process.

    **Note:** Snapshot backup retains the status of disk data at a specific point in time.

-   Replica set and sharded cluster instances support physical backup.

    **Note:** With physical backup, all physical database files in an ApsaraDB for MongoDB instance are backed up. Physical backup runs on the hidden node of an ApsaraDB for MongoDB instance, and does not affect the I/O performance of the primary and secondary nodes. If the data volume is large, backing up your ApsaraDB for MongoDB instance may require a long time.


## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Backup and Recovery**.

6.  Click **Backup Settings**.

    ![Backup and Recovery in the ApsaraDB for MongoDB console](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8445298951/p37422.png)

7.  In the dialog box that appears, configure the following parameters.

    ![Set an automatic backup policy for an ApsaraDB for MongoDB instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8445298951/p34383.png)

    |Parameter|Description|
    |:--------|:----------|
    |**Retention Days**|The number of days for which you want to retain backup data. It can only be seven days.|
    |**Backup Time**|The hour at which you want to perform the backup task. We recommend that you select an off-peak hour.|
    |**Day of Week**|The backup cycle. You can select one or more days in a week.|

8.  Click **OK**.


## References

[Restoration solution overview](/intl.en-US/User Guide/Data recovery/Restoration solution overview.md)

