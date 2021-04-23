# Restore data of an ApsaraDB for MongoDB instance to self-managed MongoDB databases by using logical backup

This topic describes how to restore the data of an ApsaraDB for MongoDB instance to self-managed MongoDB databases by using logical backup. Data restoration uses the mongorestore command. You must have created a logical backup and downloaded the logical backup file to the server where you plan to run the mongorestore command.

-   A replica set instance with three or more nodes is created.
-   The ApsaraDB for MongoDB instance and the self-managed MongoDB databases run the same database version.

Full logical backup uses the mongodump command to back up a database. During the backup process, you can still perform read/write operations on the database.

**Note:** Full logical backup runs on the hidden node of the ApsaraDB for MongoDB instance. This does not affect the read/write performance of the primary and secondary nodes. It may take a long time to back up a large volume of data.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the upper-right corner of the page, click **Back up Instance**.

    ![Back up an instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7545298951/p42250.png)

6.  In the **Back up Instance** panel, select **Logical Backup** for **Backup Method**.

7.  Click **OK**. Then, wait for the backup to complete.

8.  On the **Backup and Recovery** page, find the logical backup file and choose **![More](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Download**.

9.  Copy the downloaded file to the server where you plan to run the mongorestore command.

10. Run the following command to import the file to self-managed MongoDB databases:

    ```
    mongorestore -h <hostname> --port <server port> -u <username> -p <password> --drop --gzip --archive=<backupfile> -vvvv --stopOnError
    ```

    Parameter description:

    -   <hostname\>: the address of the server where the self-managed MongoDB databases reside. If you also run the mongorestore command on this server, enter 127.0.0.1.
    -   <server port\>: the port number of the self-managed MongoDB databases.
    -   <username\>: the username you use to log on to the self-managed MongoDB databases.
    -   <password\>: the password of the preceding account.
    -   <backupfile\>: the name of the logical backup file you downloaded.
    Example:

    ```
    mongorestore -h 127.0.0.1 --port 27017 -u root -p xxxxxxxx --drop --gzip --archive=hins1111_data_20190710.ar -vvvv --stopOnError
    ```


