# Migrate data from Amazon DynamoDB to ApsaraDB for MongoDB by using mongoimport

This topic describes how to migrate data from Amazon DynamoDB to ApsaraDB for MongoDB by using mongoimport, which is built in MongoDB for data restoration. You can install a MongoDB database on an on-premises server or in an ECS instance as an intermediary, and then use mongoimport to migrate data from an Amazon DynamoDB instance to an ApsaraDB for MongoDB instance.

**Note:** An on-premises server is used in the following example.

## Prerequisites

An ApsaraDB for MongoDB instance is created. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md) or [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md).

## Precautions

-   This is full data migration. Incremental data migration is not supported. To ensure data consistency, we recommend that you do not write data to the source database before you migrate data.
-   Run the mongoimport command on the server. Do not run this command in the mongo shell.

## Term mapping

|Term in Amazon DynamoDB|Term in ApsaraDB for MongoDB|
|:----------------------|:---------------------------|
|Table|Collection|
|Item|Document|
|Attribute|Field|

## Preparation

Install a MongoDB database on the on-premises server. Make sure that the version of the database is the same as the database version of the ApsaraDB for MongoDB instance. This server plays an intermediary role during data migration. In this example, MongoDB is installed on Ubuntu.

1.  Install the MongoDB database to your server. For more information, visit [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).

    **Note:** This server plays an intermediary role in both data backup and restoration. The server is no longer required after the migration is complete.

2.  Add the public IP address of the server to a whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

## Procedure

1.  Log on to the Amazon DynamoDB console.
2.  In the left-side navigation pane, click **Tables**.
3.  Select the table you want to migrate. For this example, select **customer**.

    ![Select an Amazon DynamoDB table](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3535298951/p45065.png)

4.  Select the data you want to migrate and export it to a **.csv** file.

    ![Select Amazon DynamoDB data to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3535298951/p45066.png)

    1.  Click the Items tab.
    2.  Select the items you want to migrate.
    3.  Choose **Actions** \> **Export to .csv**.
5.  Copy the exported .csv file to the server described in [Preparation](#section_u4c_ygw_mhb).
6.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) to obtain the public endpoint of the ApsaraDB for MongoDB instance.

    -   If you migrate data to a replica set instance of ApsaraDB for MongoDB, obtain the public endpoint of the primary node. For more information, see [Overview of replica set instance connections]().
    -   If you migrate data to a sharded cluster instance of ApsaraDB for MongoDB, obtain the public endpoint of a mongos. For more information, see [Overview of sharded cluster instance connections]().
    **Note:** You must manually apply for a public endpoint. For more information, see [Apply for a public endpoint for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Public IP Connection/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md).

7.  On the server, run the following command to import the backup files to an ApsaraDB for MongoDB database:

    ```
    mongoimport --host <mongodb_host:port> --authenticationDatabase admin -u <username> --db <database> --collection <collection> --file <filename>  --type csv --headerline                    
    ```

    **Note:**

    -   <mongodb\_host:port\>: the public endpoint of the primary node in the replica set instance of ApsaraDB for MongoDB, or the public endpoint of a mongos in the sharded cluster instance of ApsaraDB for MongoDB.
    -   <username\>: the username of the destination database in the ApsaraDB for MongoDB instance. The initial username is **root**. This user must have read and write permissions on the destination database.
    -   <database\>: the name of the authentication database. It is the database where the database user is created. If the username is root, enter admin.
    -   <collection\>: the name of the collection to which you want to import data.
    -   <filename\>: the path and name of the .csv file.
    The following command is used to import data from the customer.csv file to the customer collection in the mongodbtest database.

    ```
    mongoimport --host dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root --db mongodbtest --collection customer --file ~/download/customer.csv  --type csv --headerline
    ```

8.  When `Enter password:` is displayed, enter the password of the ApsaraDB for MongoDB database user and press Enter.

    **Note:** If you want to migrate data of other tables, repeat Steps 3 to 8.


After data import is complete, the data of the source Amazon DynamoDB instance is migrated to the destination ApsaraDB for MongoDB instance.

## What to do next

To improve the performance of data operations, we recommend that you create indexes after you import data. For more information, visit [db.collection.createIndex](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/index.html).

