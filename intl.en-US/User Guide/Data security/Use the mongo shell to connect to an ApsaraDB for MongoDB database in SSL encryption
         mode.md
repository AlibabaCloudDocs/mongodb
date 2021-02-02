# Use the mongo shell to connect to an ApsaraDB for MongoDB database in SSL encryption mode

This topic describes how to use the mongo shell to connect to an ApsaraDB for MongoDB database in Secure Sockets Layer \(SSL\) encryption mode. SSL encryption can encrypt network connections at the transport layer to improve data security and ensure data integrity.

## Prerequisites

-   The instance is a replica set instance, and the database version of the instance is 3.4or 4.0..

    **Note:** If the database version of the instance is earlier than required versions, you must upgrade the database version. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md).

-   SSL encryption is enabled for the instance. For more information, see [Configure SSL encryption for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure SSL encryption for an ApsaraDB for MongoDB instance.md).
-   Mongo shell 3.0 or later is installed on the local server or [ECS](~~25367~~) instance from which you want to connect to the database. For more information about the installation procedure, visit [Install MongoDB](https://docs.mongodb.com/v3.4/installation/).
-   The IP address of the local server or the ECS instance is added to a whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

## Precautions

After you enable SSL encryption for an instance, the CPU utilization of this instance is significantly increased. We recommend that you enable it only when necessary. For example, you can enable SSL encryption when you connect to an ApsaraDB for MongoDB instance over the Internet.

**Note:** Internal network connections are more secure than Internet connections and do not need SSL encryption.

## Procedure

A local server with a Linux operating system is used in the following example:

1.  Download an SSL CA certificate package. For more information, see [Configure SSL encryption for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure SSL encryption for an ApsaraDB for MongoDB instance.md).
2.  Decompress the package and upload the certificate files to the local server or the ECS instance where the mongo shell is installed.

    **Note:** In this example, the .pem file is uploaded to the /root/sslcafile/ directory of the local server.

3.  On the local server or in the ECS instance, run the following command to connect to a database of the ApsaraDB for MongoDB instance:

    ```
    mongo --host <host> -u <username> -p --authenticationDatabase <database> --ssl --sslCAFile <sslCAFile_path> --sslAllowInvalidHostnames
    ```

    **Note:**

    -   <host\>: the connection string \(including the port number\) of the primary or secondary node in the ApsaraDB for MongoDB instance. For more information, see [Overview of replica set instance connections]().
        -   If you want to connect to a database of the ApsaraDB for MongoDB instance over the Internet, apply for a public endpoint for this instance. For more information, see [Apply for a public endpoint for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Public IP Connection/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md).
        -   If you want to connect to a database of the ApsaraDB for MongoDB instance over an internal network, make sure that the ApsaraDB for MongoDB instance has the same network type as the ECS instance. If the network type is VPC, make sure that the two instances are in the same VPC.
    -   <username\>: the username you use to log on to a database of the ApsaraDB for MongoDB instance. The initial username is root. We recommend that you do not log on to a database as the root user in a production environment. You can create users and grant permissions to the users as needed. For more information, see [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).
    -   <database\>: the name of database corresponding to the username if authentication is enabled. If the username is root, enter admin.
    -   <sslCAFile\_path\>: the path of the SSL CA certificate files.
    Example:

    ```
    mongo --host dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin --ssl --sslCAFile /root/sslcafile/ApsaraDB-CA-Chain.pem  --sslAllowInvalidHostnames
    ```

4.  When `Enter password:` is displayed, enter the password of the database user and press Enter.

    **Note:**

    -   The password characters are not explicitly displayed when you enter the password.
    -   If you forget the password of the root user, you can reset the password. For more information, see [Set a password](/intl.en-US/Quick Start/Reset the password.md).

## Common connection scenarios

-   [Connect a local client to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account.md)

