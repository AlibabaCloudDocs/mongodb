# Use the built-in commands of MongoDB to migrate data {#concept_uvj_jgd_5fb .concept}

MongoDB provides the mongodump and mongorestore commands to migrate data from a user-created database to an ApsaraDB for MongoDB instance.

## Precautions {#section_rh3_lgd_5fb .section}

-   The operations in this topic apply to newly purchased instances that do not contain data.
-   They are all full migration operations. To avoid inconsistencies in data, we recommend that you stop all write operations on the database before migration.
-   Ensure that the mongodump and mongorestore versions are consistent with that of the user-created database.
-   If you have used the mongodump command to back up data for any databases, back up the files in the dump folder to other directories. Ensure that the dump folder \(which is the default backup folder\) is empty. Otherwise, existing backup files are overwritten during the migration.
-   Only run the mongodump and mongorestore commands on servers that MongoDB is installed on.

## Back up the user-created database {#section_czp_sjd_5fb .section}

This is a full migration operation. To avoid inconsistencies in data, stop the services related to the user-created database and stop all write operations on the database before migration.

1.  On the server where the user-created database is deployed, run the following command to fully back up the data:

    ```
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    Note:

    -   <mongodb\_host\>: the server address of the user-created database. If this database is deployed on the current server, set this parameter to 127.0.0.1.
    -   <port\>: the port number for the user-created database. It is 27017 by default.
    -   <username\>: the username for the user-created database.
    -   <database\>: the name of the authentication database for the user-created database. The default database name is admin.
    Example:

    ```
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  When `Enter password:` is displayed, enter the password to start data backup.

Wait until data backup is complete. The data of the user-created database is backed up in the dump folder of the current directory.

## Configure data shards \(optional\) {#section_l13_zhp_fgb .section}

If data shards are not configured, data is migrated to the primary shard. In this case, the storage space and computing performance of other shards are not used for data migration. For more information, see [Configure data shards](../../../../intl.en-US/Best Practices/Configure sharding to maximize the performance of shards.md#).

**Note:** Before migration, you can create a database and collection for which to configure data shards. You can also configure data shards after migration.

## Migrate data to the ApsaraDB for MongoDB instance {#section_nvh_r4d_5fb .section}

1.  Obtain the public IP address of any mongos. For more information, see [Connect to an ApsaraDB for MongoDB instance](intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance.md#).

    **Note:** You must apply for a public IP address. For more information, see [Apply for a public IP address](intl.en-US/Quick Start for Cluster/Apply for a public IP address.md#).

2.  On the server where the user-created database is deployed, run the following command to fully migrate the data to the ApsaraDB for MongoDB instance:

    ```
    mongorestore --host <Mongos_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    Note:

    -   <Mongos\_host\>: the address of any mongos in the ApsaraDB for MongoDB instance.
    -   <username\>: the account for the ApsaraDB for MongoDB instance. The default username is root.
    -   <database\>: the name of the authentication database for the ApsaraDB for MongoDB instance. The default database name is admin.
    -   <Backup directory\>: the directory that stores backup files. The default backup directory is dump.
    Example:

    ```
    mongorestore --host s-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    
    ```

3.  When `Enter password:` is displayed, enter the password to start data migration.

    **Note:** If you have forgotten your password, see [Set a password](intl.en-US/Quick Start for Cluster/Set a password.md#).


Wait until data migration is complete and check whether the data is correct. If yes, you can switch your business to the ApsaraDB for MongoDB instance.

