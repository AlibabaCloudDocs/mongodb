# Download the physical backup data of a replica set instance {#task329 .task}

You can download the physical backup data of a replica set instance based on the backup time and recover the downloaded backup data in the user-created MongoDB instance.

Standalone instances do not support this feature. You can create an instance from a specified backup to recover data. For more information, see [Create an instance based on a backup](intl.en-US/User Guide/Data recovery/Create an instance based on a backup.md#).

After [setting an automatic backup policy](intl.en-US/User Guide/Data backup/Automatically back up ApsaraDB for MongoDB data.md#), you can back up data for replica set instances in physical backup mode.

A physical backup is carried out on the hidden secondary node of an ApsaraDB for MongoDB instance. Therefore, it does not affect the I/O performance of the primary and secondary nodes. It may take a long time to back up a large amount of data. You need to wait patiently.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Backup and Recovery**.
6.  On the Backup and Recovery page that appears, locate the target physical backup and choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6723/155618142213851_en-US.png)** \> **Download**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6726/155618142213856_en-US.png)

    **Note:** After downloading the backup file, you can follow the instructions in [Recover ApsaraDB for MongoDB physical backup data in a user-created MongoDB instance](intl.en-US/User Guide/Data recovery/Recover physical backup data in a user-created MongoDB instance/Recover ApsaraDB for MongoDB physical backup data in a user-created MongoDB instance.md#) to recover data.


