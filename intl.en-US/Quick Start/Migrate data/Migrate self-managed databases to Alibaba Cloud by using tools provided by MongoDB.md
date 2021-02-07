# Migrate self-managed databases to Alibaba Cloud by using tools provided by MongoDB

This topic describes how to migrate self-managed MongoDB databases to Alibaba Cloud by using mongodump and mongorestore, which are both built in MongoDB data for backup and restoration. You can install mongodump and mongorestore on a local server or an ECS instance, and use mongodump and mongorestore to migrate these databases to a replica set instance of ApsaraDB for MongoDB.

To avoid service disruption, we recommend that you use DTS to migrate self-managed MongoDB databases to Alibaba Cloud. For more information, see [Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB
         by using DTS.md).

For more information about data migration and synchronization solutions, see [Overview](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).

## Prerequisites

-   mongodump and mongorestore are installed on a different server from the self-managed MongoDB databases, but run the same version as the databases. For more information about the installation procedure, visit [Install MongoDB](https://docs.mongodb.com/v3.4/installation/) at the MongoDB official website.

    **Note:** You can also run the mongodump and mongorestore commands on the server where the self-managed MongoDB databases reside.

-   The storage capacity of the destination replica set instance is greater than the occupied storage space of the self-managed MongoDB databases. If the storage capacity is insufficient, you can upgrade the instance. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Precautions

-   This is full data migration. To ensure data consistency, we recommend that you stop writing data to the self-managed MongoDB databases before you migrate data.
-   If you have run the mongodump command to back up a self-managed MongoDB database, move the backup files in the dump folder to another directory and make sure that the dump folder is empty. If it is not empty, its historical backup files are overwritten the next time you back up a database.
-   Run the mongodump and mongorestore commands on the servers. Do not run these commands on the mongo shell.

## Step 1: Back up the self-managed MongoDB databases

1.  On the server where the self-managed MongoDB databases reside, run the following command to back up all the databases:

    ```
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    **Note:**

    -   <mongodb\_host\>: the address of the server where the self-managed MongoDB databases reside. In this case, enter 127.0.0.1.
    -   <port\>: the service port of the self-managed MongoDB databases. The default value is 27017.
    -   <username\>: the account used to log on to a self-managed MongoDB database.
    -   <database\>: the name of the database corresponding to the account if authentication is enabled.
    Example:

    ```
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  When `Enter password:` is displayed, enter the password of the database account and press Enter. The data backup operation starts.

    **Note:** The password characters are not displayed when you enter the password.


Wait until data backup is complete. The data of the self-managed MongoDB databases is backed up to the dump folder of the directory where you run this command.

## Step 2: Migrate data to the destination sharded cluster instance

1.  Obtain the public or internal connection string of the primary node in the destination replica set instance. For more information, see [Overview of replica set instance connections]().

    **Note:** You must apply for a public endpoint manually. For more information, see [Apply for a public endpoint for a sharded cluster instance](/intl.en-US/Quick Start/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md).

2.  Add the IP address of the server where the self-managed MongoDB databases reside to a whitelist of the destination replica set instance. For more information, see [Configure a whitelist for a replica set instance]().

    **Note:**

    -   If you want to connect to a replica set instance over an internal network, you must add the private IP address of the ECS instance where the self-managed MongoDB databases reside to a whitelist of the replica set instance.
    -   If you want to connect to a replica set instance over the Internet, you must add the public IP address of the server where the self-managed MongoDB databases reside to a whitelist of the replica set instance.
3.  On the server where the self-managed MongoDB databases reside, run the following command to restore all the backup files to the destination replica set instance:

    ```
    mongorestore --host <Primary_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    **Note:**

    -   <Primary\_host\>: the connection string of the primary node in the destination replica set instance.
    -   <username\>: the account used to log on to a database of the destination replica set instance. The initial account is root.
    -   <database\>: the name of the database corresponding to the account if authentication is enabled. If the account is root, enter admin.
    -   <Backup directory\>: the directory where the backup files are stored. The default value is dump.
    Example:

    ```
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    ```

4.  When `Enter password:` is displayed, enter the password of the database account and press Enter. The data restoration operation starts.

    **Note:**

    -   The password characters are not displayed when you enter the password.
    -   If you forget the password of the root account, you can reset it. For more information, see [Set a password for a replica set instance]().

After data restoration is complete, switch over your business to the destination replica set instance. We recommend you perform the switchover during off-peak hours to minimize impact on your business.

