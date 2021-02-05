# Migrate self-managed MongoDB databases to standalone instances by using tools provided by MongoDB

mongodump and mongorestore are both built in MongoDB for backup and restoration. You can install the MongoDB database on a local device or ECS instance and use mongodump and mongorestore to migrate a self-managed MongoDB database to an ApsaraDB for MongoDB instance.

To avoid service disruption, we recommend that you use DTS to migrate self-managed MongoDB databases to Alibaba Cloud. For more information, see [Migrate user-created standalone MongoDB databases to Alibaba Cloud by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate user-created standalone MongoDB databases to Alibaba Cloud by using DTS.md).

For more information about data migration and synchronization solutions, see [Overview](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).

## Prerequisites

-   mongodump and mongorestore are installed on a different server from the self-managed MongoDB databases, but run the same version as the databases. For more information about the installation procedure, visit [Install MongoDB](https://docs.mongodb.com/v3.4/installation/) at the MongoDB official website.

    **Note:** You can also run the mongodump and mongorestore commands on the server where the self-managed MongoDB databases are deployed.

-   Standalone ApsaraDB for MongoDB instances support only MongoDB 3.4.To ensure compatibility, the version of the self-managed MongoDB database must be 3.0, 3.2, 3.4, 4.0, or 4.2.

    **Note:** If the source self-managed MongoDB databases and the destination ApsaraDB for MongoDB instance run different database versions or storage engines, make sure that no compatibility issues are between them before you start migration. For more information about the database versions and storage engines supported by ApsaraDB for MongoDB, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

-   The storage space of the standalone ApsaraDB for MongoDB instance must be larger than that required by the self-managed MongoDB database. If the storage space is insufficient, you can expand the storage space. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Precautions

-   This is full data migration. To ensure data consistency, we recommend that you stop writing data to the self-managed MongoDB databases before you migrate data.
-   If you have run the mongodump command to back up a self-managed MongoDB database, move the backup files in the dump folder to another directory and make sure that the dump folder is empty. If it is not empty, its historical backup files are overwritten the next time you back up a database.
-   Run the mongodump and mongorestore commands on the server where the self-managed MongoDB database is deployed. Do not run them in the mongo shell.

## Step 1: Back up the self-managed MongoDB database

1.  On the server where the self-managed MongoDB databases reside, run the following command to back up all the databases:

    ```
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    **Note:**

    -   <mongodb\_host\>: the address of the server where the self-managed MongoDB databases reside. In this case, enter 127.0.0.1.
    -   <port\>: the service port of the self-managed MongoDB databases. The default value is 27017.
    -   <username\>: the username used to log on to a uself-managed MongoDB database.
    -   <database\>: the name of the authentication database. It is the database where the database account is created.
    Example:

    ```
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  When `Enter password:` is displayed, enter the password of the database user and press the Enter key. The data backup operation starts.

    **Note:** The password characters are not displayed when you enter the password.


Wait until data backup is complete. The data of the self-managed MongoDB databases is backed up to the dump folder of the directory where you run this command.

## Step 2: Migrate data to the destination sharded cluster instance

1.  Obtain the connection address of the primary node of the ApsaraDB for MongoDB instance.

    1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

    2.  In the upper-left corner of the page, select the region where the instance is deployed.

    3.  In the left-side navigation pane, click **Replica Set Instances**.

    4.  On the page that appears, find the instance and click its ID.

    5.  In the left-side navigation pane, click **Database Connection** to view connection information.

        ![View connection details on a standalone instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5536845951/p35103.png)

        |Address type|Description|Application scenario|
        |------------|-----------|--------------------|
        |VPC connection address|A VPC is an isolated network with higher security and performance than the classic network.|The self-managed MongoDB database is deployed on the[ECS instance](https://www.alibabacloud.com/help/zh/doc-detail/25367.htm). **Note:** The ECS instance and ApsaraDB for MongoDB instance must be located in the same region and VPC. |
        |Public connection address|By default, ApsaraDB for MongoDB instances do not provide public connection addresses. You must apply for a public endpoint if necessary. For more information, see [Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance]().|The self-managed MongoDB database is deployed on a local device.|

2.  Add the IP address of the server where the self-managed database is deployed to a whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist for a standalone ApsaraDB for MongoDB instance]().

    **Note:**

    -   When you connect to an ApsaraDB for MongoDB instance over a VPC, you must add the internal IP address of the ECS instance where the self-managed database is deployed to the whitelist of the ApsaraDB for MongoDB instance.
    -   When you connect to an ApsaraDB for MongoDB instance over the Internet, you must add the public IP address of the local server where the self-managed database is deployed to a whitelist of the ApsaraDB for MongoDB instance.
3.  On the server where the self-managed database is deployed, run the following command to migrate the whole data to the ApsaraDB for MongoDB instance:

    ```
    mongorestore --host <Primary_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    **Note:**

    -   <Primary\_host\>: the connection address of the primary node in the ApsaraDB for MongoDB instance.
    -   <username\>: the database account of the ApsaraDB for MongoDB instance. The initial account is **root**.
    -   <database\>: the name of the authentication database. It is the database where the database account is created. If the database account is root, enter admin.
    -   <Backup directory\>: the directory where the backup files are stored. The default value is dump.
    Example:

    ```
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    ```

4.  Enter the password for the database user of the ApsaraDB for MongoDB instance in the `Enter password:` prompt and press Enter to start data migration.

    **Note:**

    -   The password characters are not displayed when you enter the password.
    -   If you forget the password of the root user, you can reset it. For more information, see [Set a password for a sharded cluster instance]().

Wait until the data migration is complete. Switch your business to the ApsaraDB for MongoDB instance during off-peak hours.

## References

After the database is migrated to an ApsaraDB for MongoDB instance, you can connect to the database and manage the database and database account.

-   [Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell.md)
-   [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md)

