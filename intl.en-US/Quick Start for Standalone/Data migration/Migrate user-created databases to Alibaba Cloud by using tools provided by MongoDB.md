# Migrate user-created databases to Alibaba Cloud by using tools provided by MongoDB

mongodump and mongorestore are both built in MongoDB for backup and restoration. You can install the MongoDB database on a local device or ECS instance and use mongodump and mongorestore to migrate a user-created MongoDB database to an ApsaraDB for MongoDB instance.

We recommend that you use DTS to migrate user-created MongoDB databases to Alibaba Cloud, which ensures data migration without service downtime. For more information, see [Migrate user-created standalone MongoDB databases to Alibaba Cloud by using DTS](/intl.en-US/Quick Start for Standalone/Data migration/Migrate user-created standalone MongoDB databases to Alibaba Cloud by using DTS.md).

For more data migration and synchronization solutions, see [Overview](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).

## Prerequisites

-   The version of mongodump and mongorestore is the same as that of the user-created MongoDB database. For more information about the installation procedure, visit [Install MongoDB](https://docs.mongodb.com/v3.4/installation/) at the official MongoDB website.

    **Note:** You can also run the mongodump and mongorestore commands on the server where the user-created MongoDB databases reside.

-   Standalone ApsaraDB for MongoDB instances only support MongoDB 3.4.To ensure compatibility, the version of the user-created MongoDB database must be 3.0, 3.2, 3.4, 4.0, or 4.2 .

    **Note:** If the source user-created MongoDB databases and the destination ApsaraDB for MongoDB instance run different database versions or storage engines, ensure that there are no compatibility issues between them before you start migration. For more information about the database versions and storage engines supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

-   The storage space of the standalone ApsaraDB for MongoDB instance must be larger than that required by the user-created MongoDB database. If the storage space is insufficient, you can expand the storage space. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Precautions

-   This is full data migration. To ensure data consistency, stop related services and data writing operations on the source MongoDB database before the migration starts.
-   If you have run the mongodump command to back up the database, move the backup files in the dump folder to another directory. Ensure that the dump folder is empty. Otherwise, the historical backup files in this folder is overwritten during data backup.
-   Run the mongodump and mongorestore commands on the server where the user-created MongoDB database resides. Do not run them in the mongo shell.

## Step 1: Back up the user-created database

1.  On the server where the user-created database resides, run the following command to back up the whole data:

    ```
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    **Note:**

    -   <mongodb\_host\>: the server address of the user-created MongoDB database. If this database is deployed on the current server, set this parameter to 127.0.0.1.
    -   <port\>: the service port number for the user-created database. The default port number is 27017.
    -   <username\>: the account used to log on to the user-created MongoDB database.
    -   <database\>: the name of the authentication database. It is the database where the database account is created.
    Example:

    ```
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  Enter the password for the database user in the `Enter password:` prompt and press Enter to start the backup.

    **Note:** The password you enter is not displayed.


Wait until the data backup is complete. The data of the user-created database is backed up in the dump folder of the current directory.

## Step 2: Migrate data to the ApsaraDB for MongoDB instance

1.  Obtain the connection address of the primary node of the ApsaraDB for MongoDB instance.

    1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

    2.  In the upper-left corner of the page, select the region where your instance resides.

    3.  In the left-side navigation pane, click **Replica Set Instances**.

    4.  Find the target instance and click its ID.

    5.  In the left-side navigation pane, click **Database Connection** to view the database connection details.

        ![View connection details on a standalone instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5536845951/p35103.png)

        |Address type|Description|Application scenario|
        |------------|-----------|--------------------|
        |VPC connection address|A VPC is an isolated virtual network with better security and performance than a classic network.|The user-created MongoDB database is deployed on the [ECS instance](https://www.alibabacloud.com/help/doc-detail/25367.htm). **Note:** The ECS instance and ApsaraDB for MongoDB instance must be located in the same region and VPC. |
        |Public connection address|By default, ApsaraDB for MongoDB instances do not provide public connection addresses. You need to apply for a public endpoint if required. For more information, see [Apply for a public endpoint](/intl.en-US/Quick Start for Standalone/Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance.md).|The user-created MongoDB database is deployed on a local device.|

2.  Add the IP address of the server where the user-created database resides to a whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](/intl.en-US/Quick Start for Standalone/Configure a whitelist for a standalone ApsaraDB for MongoDB instance.md).

    **Note:**

    -   When you connect to an ApsaraDB for MongoDB instance over a VPC, you must add the internal IP address of the ECS instance where the user-created database resides to the whitelist of the ApsaraDB for MongoDB instance.
    -   When you connect to an ApsaraDB for MongoDB instance over the Internet, you must add the public IP address of the local server where the user-created database resides to a whitelist of the ApsaraDB for MongoDB instance.
3.  On the server where the user-created database resides, run the following command to migrate the whole data to the ApsaraDB for MongoDB instance:

    ```
    mongorestore --host <Primary_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    **Note:**

    -   <Primary\_host\>: the connection address of the primary node in the ApsaraDB for MongoDB instance.
    -   <username\>: the database account of the ApsaraDB for MongoDB instance. The initial account is **root**.
    -   <database\>: the name of the authentication database. It is the database where the database account is created. If the database account is root, enter admin.
    -   <Backup directory\>: the directory that stores backup files. The default backup directory is dump.
    Example:

    ```
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    ```

4.  Enter the password for the database user of the ApsaraDB for MongoDB instance in the `Enter password:` prompt and press Enter to start data migration.

    **Note:**

    -   The password you enter is not displayed.
    -   If you forget the password for the root user, you can reset it. For more information, see [Set a password](/intl.en-US/Quick Start for Standalone/Set a password for a standalone ApsaraDB for MongoDB instance.md).

Wait until the data migration is complete. Switch your business to the ApsaraDB for MongoDB instance during off-peak hours.

## References

After the database is migrated to an ApsaraDB for MongoDB instance, you can connect to the database and manage the database and database account.

-   [Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell](/intl.en-US/Quick Start for Standalone/Connect to an instance/Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell.md)
-   [Manage MongoDB users though DMS]()

