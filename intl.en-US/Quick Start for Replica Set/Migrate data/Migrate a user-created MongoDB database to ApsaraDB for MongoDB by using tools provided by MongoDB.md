# Migrate a user-created MongoDB database to ApsaraDB for MongoDB by using tools provided by MongoDB

This topic describes how to migrate a user-created MongoDB database to ApsaraDB for MongoDB by using mongodump and mongorestore, which are built in MongoDB for data backup and restoration. You can install user-created MongoDB databases on a local server or an ECS instance, and use mongodump and mongorestore to migrate these databases to an ApsaraDB for MongoDB sharded cluster instance.

## Background information

-   To avoid service disruption, we recommend that you use DTS to migrate user-created sharded MongoDB databases to ApsaraDB for MongoDB. For more information, see [Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start for Replica Set/Migrate data/Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS.md).
-   For more information about data migration and synchronization solutions, see [Overview of data migration and synchronization](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).

## Prerequisites

-   mongodump and mongorestore are installed on a different server from the user-created MongoDB databases, but run the same version as the databases. For more information about the installation procedure, visit [Install MongoDB](https://docs.mongodb.com/v3.4/installation/) at the MongoDB official website.

    **Note:** You can also run the mongodump and mongorestore commands on the server where the user-created MongoDB databases reside.

-   The storage capacity of the destination sharded cluster instance is greater than the storage space occupied by the user-created MongoDB databases. If the storage capacity is insufficient, you can upgrade the instance. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Precautions

-   This is full data migration. To ensure data consistency, we recommend that you stop writing data to the user-created MongoDB databases before you migrate data.
-   If you have run the mongodump command to back up a user-created MongoDB database, move the backup files in the dump folder to another directory and make sure that the dump folder is empty. If it is not empty, its historical backup files are overwritten the next time you back up a database.
-   Run the mongodump and mongorestore commands on the servers. Do not run these commands on the mongo shell.

## Step 1: Back up the user-created MongoDB databases

1.  On the server where the user-created MongoDB databases reside, run the following command to back up all the databases:

    ```
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    **Note:**

    -   <mongodb\_host\>: the IP address of the server where the user-created MongoDB databases reside. In this case, enter 127.0.0.1.
    -   <port\>: the service port of the user-created MongoDB databases. The default value is 27017.
    -   <username\>: the username used to log on to a user-created MongoDB database.
    -   <database\>: the database corresponding to the username if authentication is enabled.
    Example:

    ```
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  When `Enter password:` is displayed, enter the password of the database user and press Enter. The data backup operation starts.

Wait until data backup is complete. The data of the user-created MongoDB databases is backed up to the dump folder of the directory where you run this command.

## Step 2: \(Optional\) Configure data sharding

If data sharding is not configured, data is only written to the primary shard. Then the storage and computing resources of other shards are not used. For more information, see [Configure sharding to maximize the performance of shards](/intl.en-US/Best Practices/Performance/Configure sharding to maximize the performance of shards.md).

**Note:** You must create required databases and collections in the destination sharded cluster instance before data migration. However, you can configure data sharding for the databases and collections either before or after data migration.

## Step 3: Migrate data to the destination sharded cluster instance

1.  Obtain the public or internal connection string of a mongos in the destination sharded cluster instance. For more information, see [Overview of sharded cluster instance connections]().

    **Note:** You must apply for a public endpoint manually. For more information, see [Apply for a public endpoint for a sharded cluster instance](/intl.en-US/Quick Start for Cluster/Apply for a public endpoint for a sharded cluster instance.md).

2.  Add the IP address of the server where the user-created MongoDB databases reside to a whitelist of the destination sharded cluster instance. For more information, see [Configure a whitelist for a sharded cluster instance](/intl.en-US/Quick Start for Cluster/Configure a whitelist for a sharded cluster instance.md).

    **Note:**

    -   If you want to connect to a sharded cluster instance over the internal network, you must add the private IP address of the ECS instance where the user-created MongoDB databases reside to a whitelist of the sharded cluster instance.
    -   If you want to connect to a sharded cluster instance over the Internet, you must add the public IP address of the server where the user-created MongoDB databases reside to a whitelist of the sharded cluster instance.
3.  On the server where the user-created MongoDB databases reside, run the following command to restore all the backup files to the destination sharded cluster instance:

    ```
    mongorestore --host <Mongos_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    **Note:**

    -   <Mongos\_host\>: the connection string of any mongos in the ApsaraDB for MongoDB instance.
    -   <username\>: the username used to log on to a database of the destination sharded cluster instance. The initial username is root.
    -   <database\>: the database corresponding to the username if authentication is enabled. If the username is root, enter admin.
    -   <Backup directory\>: the directory where the backup files are stored. The default value is dump.
    Example:

    ```
    mongorestore --host s-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    ```

4.  When `Enter password:` is displayed, enter the password of the database user and press Enter. The data restoration operation starts.

    **Note:**

    -   The password characters are not displayed when you enter the password.
    -   If you forget the password of the root user, you can reset it. For more information, see [Set a password for a sharded cluster instance](/intl.en-US/Quick Start for Cluster/Set a password for a sharded cluster instance.md).

After data restoration is complete, switch over your business to the destination sharded cluster instance. We recommend you perform the switchover during off-peak hours to minimize impact on your business.

