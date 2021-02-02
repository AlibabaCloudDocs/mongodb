# Download the physical backup data of a replica set instance

You can download the physical backup data of a replica set instance based on the backup time and restore the downloaded data to a user-created MongoDB database.

The instance is a replica set instance.

After you [set an automatic backup policy](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md), ApsaraDB for MongoDB performs physical backups for the replica set instance at a regular basis.

A physical backup is carried out on the hidden node of a replica set instance. This does not affect the I/O performance of the primary and secondary nodes. It may take a long time to back up a large amount of data.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Backup and Recovery**.

6.  On the **Backup and Recovery** page that appears, find the target physical backup and choose **![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Download**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13856.png)


## References

After downloading the backup file, you can follow the instructions in [Restore data of an ApsaraDB for MongoDB instance to a self-managed MongoDB database by using physical backup](/intl.en-US/User Guide/Data recovery/Recover physical backup data in a user-created MongoDB instance/Restore data of an ApsaraDB for MongoDB instance to a self-managed MongoDB database
         by using physical backup.md) to recover data.

