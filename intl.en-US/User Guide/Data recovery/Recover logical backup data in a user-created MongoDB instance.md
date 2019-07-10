# Recover logical backup data in a user-created MongoDB instance {#task336 .task}

Replica set and sharded cluster instances support logical backup. You can start a full logical backup to back up instance data and download the logical backup file. Then, you can run a mongorestore command to recover the downloaded backup data in a user-created MongoDB instance.

Standalone instances do not support this feature. You can create an instance from a specified backup to recover data. For more information, see [Create an instance based on a backup](intl.en-US/User Guide/Data recovery/Create an instance based on a backup.md#).

To guarantee compatibility, we recommend that the database version of the user-created MongoDB instance be the same as that of the ApsaraDB for MongoDB instance.

You can run a mongodump command to start a full logical backup to back up ApsaraDB for MongoDB data. During the backup, you can still read data from and write data into the ApsaraDB for MongoDB instance.

**Note:** A full logical backup is carried out on the hidden secondary node of an ApsaraDB for MongoDB instance. Therefore, it does not affect the I/O performance of the primary and secondary nodes. It may take a long time to back up a large amount of data. You need to wait patiently.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Backup and Recovery**.
6.  In the upper-right corner of the Backup and Recovery page that appears, click **Backup Instance**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41514/156273996142250_en-US.png)

7.  In the Backup Instance dialog box that appears, select **Logical Backup** as the backup method.
8.  Click **OK** and wait until the instance data is successfully backed up.
9.  On the Backup and Recovery page, locate the completed logical backup and choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6723/156273996113851_en-US.png)** \> **Download** in the Operation column.
10. After downloading the backup file, run the following command to import the backup data into the user-created MongoDB instance: 

    ``` {#codeblock_ip1_wrp_ofs}
    mongorestore -h <hostname> --port <server port> -u <username> -p <password> --drop --gzip --archive=<backupfile> -vvvv --stopOnError
    ```

    **Notes**:

    -   <hostname\>: The server address of the user-created MongoDB instance. Set this parameter to 127.0.0.1 if the user-created MongoDB instance is deployed on the current server.
    -   <server port\>: The port used by the user-created MongoDB instance.
    -   <username\>: The database username used to log on to the user-created MongoDB instance.
    -   <password\>: The database password used to log on to the user-created MongoDB instance.
    -   <backupfile\>: The name of the downloaded logical backup file.
    **Example**:

    ``` {#codeblock_crv_e4d_qgx}
    mongorestore -h 127.0.0.1 --port 27017 -u root -p xxxxxxxx --drop --gzip --archive=hins1111_data_20190710.ar -vvvv --stopOnError
    ```


