# Use the built-in commands of MongoDB to migrate data {#concept_uvj_jgd_5fb .concept}

MongoDB provides the mongodump and mongorestore commands for you to migrate data from a user-created MongoDB instance to an ApsaraDB for MongoDB instance.

## Notes {#section_rh3_lgd_5fb .section}

-   Operations in this topic apply to newly purchased instances that do not contain data.
-   Use the mongodump and mongorestore commands of MongoDB 3.0 or a later version.
-   If you have used the mongodump command to back up data for any databases, move backup files from the dump folder to other directories. Ensure that the dump folder \(which is the default backup folder\) is empty. If it is not empty, existing backup files are overwritten during the migration.
-   Run the mongodump and mongorestore commands on the server where MongoDB is installed. Do not run these commands in a mongo shell environment.

## Back up the user-created MongoDB instance {#section_czp_sjd_5fb .section}

On the server where the user-created MongoDB instance is deployed, run the following command to export all database data and store the exported files in the dump folder of the current directory:

```
mongodump --host <mongodb_host>:27017 --authenticationDatabase admin -u <username> -p <password>
```

Notes:

-   <mongodb\_host\>: The server address of the user-created MongoDB instance. Set this parameter to 127.0.0.1 if the user-created MongoDB instance is deployed on the current server.
-   <username\>: The database username used to log on to the user-created MongoDB instance.
-   <password\>: The database password used to log on to the user-created MongoDB instance.

Wait until data backup is completed. The data of the user-created MongoDB instance is backed up in the dump folder of the current directory.

## Migrate data to the ApsaraDB for MongoDB instance {#section_nvh_r4d_5fb .section}

1.  Obtain the address used to connect to the primary node of the ApsaraDB for MongoDB replica set instance. For more information, see [Obtain the replica set instance connection information](intl.en-US/Quick Start for Replica Set/Connect to an instance/Obtain the replica set instance connection information.md#).

    **Note:** If you need to connect to your ApsaraDB for MongoDB instance through the Internet, you can [apply for a public address](intl.en-US/Quick Start for Replica Set/Apply for a public address.md#).

2.  On the server where the user-created MongoDB instance is deployed, run the following command to import the backup data of the user-created MongoDB instance into the target ApsaraDB for MongoDB instance:

    ```
    mongorestore --host <Primary_host>:3717 --authenticationDatabase admin -u <username> -p <password> <Backup directory>
    ```

    Notes:

    -   <Primary\_host\>: The address used to connect to the primary node of the ApsaraDB for MongoDB replica set instance.
    -   <username\>: The database username used to log on to the ApsaraDB for MongoDB instance. The default username is root.
    -   <password\>: The database password used to log on to the ApsaraDB for MongoDB instance.
    -   <Backup directory\>: The directory that stores backup files. The default directory is the dump folder.

Wait until data recovery is completed. Data is migrated from the user-created MongoDB instance to the ApsaraDB for MongoDB replica set instance.

