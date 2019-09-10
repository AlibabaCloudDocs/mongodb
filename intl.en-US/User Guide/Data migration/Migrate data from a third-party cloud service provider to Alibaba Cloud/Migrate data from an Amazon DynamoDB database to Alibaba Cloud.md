# Migrate data from an Amazon DynamoDB database to Alibaba Cloud {#concept_186795 .concept}

You can use mongoimport to migrate data from an Amazon DynamoDB database to ApsaraDB for MongoDB. mongoimport is a data import tool provided by MongoDB.

## Prerequisites {#section_pnm_tgw_mhb .section}

An ApsaraDB for MongoDB instance is created. For more information, see [Create an instance](../../../../intl.en-US/Quick Start for Replica Set/Create an instance.md#) or [Create a sharded cluster instance](../../../../intl.en-US/Quick Start for Cluster/Create a sharded cluster instance.md#).

## Precautions {#section_xj3_k3w_mhb .section}

-   This operation is full data migration. Incremental data migration is not supported. To avoid data inconsistency, stop writing data to the database before the migration starts.
-   Run mongoimport commands on the server on which the MongoDB service is installed. Do not run these commands in the mongo shell.

## Relation of terms in DynamoDB and ApsaraDB for MongoDB {#section_ywn_0y5_3jb .section}

|Term in DynamoDB|Term in ApsaraDB for MongoDB|
|:---------------|:---------------------------|
|Table|Collection|
|Item|Document|
|Attribute|Field|

## Preparation of the environment {#section_u4c_ygw_mhb .section}

Install the MongoDB program on the local server. Ensure that the version of the program is the same as that of the ApsaraDB for MongoDB database. This server is an intermediary that transfers the data during data migration. In this case, the MongoDB program is installed on Ubuntu Linux.

1.  Install the MongoDB program on the local server. For more information, see [Install MongoDB](https://docs.mongodb.com/manual/administration/install-community/).

    **Note:** This server is used as the intermediary for data backup and recovery. You will not need it after the migration.

2.  Add the IP address of the local server to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](intl.en-US/User Guide/Data security/Configure a whitelist.md#).

## Migration procedure {#section_p2d_rzv_mhb .section}

1.  Log on to the Amazon DynamoDB console.
2.  In the left-side navigation pane, click **Table**.
3.  Select the **customer** table.

    ![Choose an Amazon DynamoDB table](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161016/156808399845065_en-US.png)

4.  Select the data to be migrated and export it in the **.csv** format.

    ![Select the data in Amazon DynamoDB for migration](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161016/156808399845066_en-US.png)

    1.  Click the Program tab.
    2.  Select the data to be migrated.
    3.  Choose **Operation** \> **Export to .csv** from the shortcut menu.
5.  Copy the exported .csv file to the local server in [Preparation of the environment](#section_u4c_ygw_mhb).
6.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) to obtain the public connection address of the ApsaraDB for MongoDB instance.

    -   If you need to migrate data to ApsaraDB for MongoDB replica set instances, obtain the public connection address of the primary node. For more information, see [Connect to an replica set instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to an replica set instance through the mongo shell.md#).
    -   To migrate data to a sharded cluster instance of ApsaraDB for MongoDB, obtain the public IP address of any mongos. For more information, see [Connect to an ApsaraDB for MongoDB instance](../../../../intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance.md#).
    **Note:** You need to manually apply for the public connection address. For more information, see [Apply for a public address](intl.en-US/User Guide/Network connection management/Apply for a public address.md#).

7.  On the local server, run the following command to import data to the ApsaraDB for MongoDB database:

    ``` {#codeblock_cw2_ac0_794}
    mongoimport --host <mongodb_host:port> --authenticationDatabase admin -u <username> --db <database> --collection <collection> --file <filename>  --type csv --headerline                    
    ```

    **Note:** 

    -   <mongodb\_host:port\>: the connection address of the primary node in the ApsaraDB for MongoDB replica set instance, or the connection address of a mongos in the ApsaraDB for MongoDB sharded cluster instance.
    -   <username\>: the database username of the ApsaraDB for MongoDB instance. Default value: root. This user must have read and write permissions.
    -   <database\>: the name of the database to import data to.
    -   <collection\>: the name of the collection to import data to.
    -   <filename\>: the path and name of the .csv file.
    Example: Import data from customer.csv to the customer collection in the mongodbtest database.

    ``` {#codeblock_z1c_n9f_wv6}
    mongoimport --host dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root --db mongodbtest --collection customer --file ~/download/customer.csv  --type csv --headerline
    ```

8.  In the `Enter password:` prompt, enter the password corresponding to the AparaDB for MongoDB database account. After this operation, data import starts.

    **Note:** If you need to migrate data of other tables, repeat Steps 3 to 8.


Wait until the data import is complete. The migration of data from the Amazon DynamoDB database to Alibaba Cloud is complete.

## Subsequent operations {#section_el1_3ta_198 .section}

To improve the performance of data operations, you also need to create indexes after data import as required. For more information, see [db.collection.createIndex](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/index.html).

