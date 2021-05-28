# Manually back up an ApsaraDB for MongoDB instance

This topic describes how to manually back up an ApsaraDB for MongoDB instance. ApsaraDB for MongoDB supports both automatic backup and manual backup. You can configure a backup policy for the system to automatically back up your ApsaraDB for MongoDB instance based on the backup cycle you specify.

## Impacts

-   ApsaraDB for MongoDB stores its backup files in [Object Storage Service](~~31817~~) \(OSS\) to reduce the storage usage of ApsaraDB for MongoDB instances.
-   Standalone instances support only snapshot backup, which decreases their I/O performance.
-   Physical backup and logical backup run on the hidden nodes of replica set instances, and do not affect the performance of the primary and secondary nodes. If the data volume is large, backing up your ApsaraDB for MongoDB instance may require a long time.
-   After the database version is upgraded, the backup files of the original version cannot be used to restore data of the new version.

## Backup methods

-   Snapshot backup: The status of disk data at a specific point in time is retained.
-   Physical backup: Physical database files of an ApsaraDB for MongoDB instance are backed up. This method provides faster backup and restoration compared with logical backup.
-   Logical backup: mongodump is used to logically back up each database. Logical backup restores data in the form of playback commands during restoration.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the upper-right corner of the page, click **Back up Instance**.

6.  In the dialog box that appears, specify **Backup Method**.

    **Note:**

    -   If the instance is a standalone instance, you can select only **Snapshot Backup**.
    -   If the instance is a replica set or sharded cluster instance, you can select **Logical Backup** or **Physical Backup**.
    ![Select a backup method](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6694812261/p7041.png)

7.  Click **OK**.


## References

[Restoration solution overview](/intl.en-US/User Guide/Data recovery/Restoration solution overview.md)

