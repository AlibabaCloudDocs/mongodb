# Migrate user-created databases to Alibaba Cloud through tools provided by MongoDB {#concept_ztl_f4w_fgb .concept}

MongoDB provides two command tools: mongodump and mongorestore. You can use these command tools to migrate data from user-created MongoDB database to standalone ApsaraDB for MongoDB instances.

## Prerequisites {#section_yvn_5hk_pgb .section}

-   The version of mongodump and mongorestore is the same as the version of the user-created MongoDB database.
-   The storage space of the standalone instance must be larger than the storage space of the user-created MongoDB instance. If the storage space is insufficient, you can use [Change the configuration](../../../../intl.en-US/User Guide/Instance management/Change the configuration.md#) to expand the storage space.

## Precautions {#section_rh3_lgd_5fb .section}

-   This is a full migration. To avoid data inconsistency, stop writing into the database before the migration starts.
-   If you have used mongodump to back up the database, move the files in the dump folder to other directories. Ensure that the dump folder is empty before data migration. Otherwise, existing backup files in this folder will be overwritten.
-   Run the mongodump and mongorestore commands on the server where the user-created database is deployed. Do not run these in the mongo shell.

## Back up the user-created database {#section_czp_sjd_5fb .section}

This is a full migration. To avoid inconsistencies in data, stop the services related to the user-created database and stop data writing before migration.

1.  On the server where the user-created database is deployed, run the following command to back up all the data:

    ``` {#codeblock_yp1_gq3_p9p}
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    Note:

    -   <mongodb\_host\>: the server address of the user-created database. If this database is deployed on the current server, set this parameter to 127.0.0.1.
    -   <port\>: the service port number for the user-created database. The default port number is 27017.
    -   <username\>: the account used to log on to the user-created MongoDB database.
    -   <database\>: the name of the authentication database for the user-created database. The default database name is admin.
    Example:

    ``` {#codeblock_xmd_yf6_kf5}
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  Enter the password in the `Enter password:` prompt to start data backup.

Wait until the data backup is complete. The data of the user-created database is backed up in the dump folder of the current directory.

## Migrate data to ApsaraDB for MongoDB {#section_nvh_r4d_5fb .section}

1.  Obtain the connection address of the primary node of standalone instance.

    1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
    2.  Select the region where the destination instance is located.
    3.  In the left-side navigation pane, click **Replica Set Instances**.
    4.  Click the ID of the instance.
    5.  In the left-side navigation pane, click **Database Connection**.

        ![View connection details on a standalone MongoDB node](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82882/156222521435103_en-US.png)

    **Note:** 

    -   Intranet Connection - VPC: A Virtual Private Cloud \(VPC\) is an isolated virtual network that has higher security and performance than a classic network.

        The VPC network is suitable for user-created MongoDB databases built based on [ECS instances](https://www.alibabacloud.com/help/zh/doc-detail/25367.htm). The ECS instance and ApsaraDB to MongoDB instances must be in the same region and VPC. You also need to add the private IP address of the ECS instance to the MongoDB instance whitelist. For more information, see [Configure a whitelist](intl.en-US/Quick Start for Standalone/Configure a whitelist.md#).

    -   Public IP Connection: Instances are not automatically configured with a public IP address to ensure security. You must manually apply for a public IP address for the instance. For more information, see [Apply for a public IP address](intl.en-US/Quick Start for Standalone/Apply for a public address.md#).

        To migrate instances through the public network connection address, you must add the public IP address of the user-created MongoDB database to the whitelist of the ApsaraDB for MongoDB instance.

2.  On the server of the user-created MongoDB database, run the following command to import all the data of the database to ApsaraDB for MongoDB.

    ``` {#codeblock_k6c_o56_5rs}
    mongorestore --host <Primary_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    Note:

    -   <Primary\_host\>: the connection address of the primary node in the replica set instance.
    -   <username\>: the database account for the ApsaraDB for MongoDB instance. The default username is root.
    -   <database\>: the name of the authentication database for the ApsaraDB for MongoDB instance. The default database name is admin.
    -   <Backup directory\>: the directory that stores backup files. The default backup directory is dump.
    Example:

    ``` {#codeblock_dht_j22_7u7}
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    						
    ```

3.  Enter the password in the `Enter password:` prompt to start data migration.

    **Note:** For more information about how to set a database password, see [Set a password](intl.en-US/Quick Start for Standalone/Set a password.md#).


Wait until the data migration is complete. Switch your businesses to the ApsaraDB for MongoDB instance during off-peak hours to avoid negatively affecting your businesses.

## More information {#section_kqs_yjk_pgb .section}

After migrating databases to ApsaraDB to MongoDB instances, you can connect to the database, manage the database, and manage database users as required.

[Connect to ApsaraDB for MongoDB through the mongo shell](intl.en-US/Quick Start for Standalone/Connect to an instance/Connect to ApsaraDB for MongoDB through the mongo shell.md#)

