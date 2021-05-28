---
keyword: [Connect mongodb to a specified database, ApsaraDB for MongoDB secure write, ApsaraDB for MongoDB logon methods, how to connect ApsaraDB for MongoDB, ApsaraDB for MongoDB password that you connect to a database]
---

# Connect to a replica set instance by using the mongo shell

This topic describes how to use the mongo shell to connect to a replica set instance.The mongo shell is a database management tool provided by ApsaraDB for MongoDB. You can install it on your client or in an ECS instance. This topic describes how to log on to an ApsaraDB for MongoDB instance.

-   The version of the mongo shell is the same as that of your instance. This ensures successful authentication. For information about the installation procedure, visit [MongoDB official documentation](https://docs.mongodb.com/manual/installation/). Choose the version in the upper-left corner of the page based on your client version.
-   The IP address of your client is added to a whitelist of the sharded cluster instance. For more information, see [Configure a whitelist for a standalone ApsaraDB for MongoDB instance]().

    **Note:** If you want to connect to the instance over the Internet, you must apply for a public endpoint. For more information, see [Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance]().


## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connections** to obtain the connection string of a node and the connection string URI.

    **Note:** For more information about how to query the connection addresses, see [Description of connection strings]().

6.  Connect to the sharded cluster instance from your client or ECS instance that has the mongo shell installed.

    -   Single-node connection

        During routine tests, you can directly connect to a primary or secondarynode. A [failover](/intl.en-US/User Guide/Primary/Secondary failover/Trigger a primary/secondary failover for a replica set instance.md) changes the roles of connected nodes, which affects read/write operations.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2074812261/p31535.png)

        Command syntax:

        ```
        mongo --host <host> -u <username> -p --authenticationDatabase <database>
        ```

        **Note:**

        -   <host\>: the connection string of the primary or secondary node.
            -   Primary node: If you connect to this node, you can perform read/write operations on the databases of the replica set instance.
            -   Secondary node: If you connect to this node, you can perform only read operations on the databases of the replica set instance.
        -   <username\>: the username you use to log on to a database of the ApsaraDB for MongoDB instance. The default username is root. We recommend that you do not log on to a database as the root user in a production environment. You can create users and grant permissions to the users. For more information, see [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).
        -   <database\>: the name of the authentication database. It is the database where the database user is created. If the database username is root, enter admin. If you want to specify another database, run the [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/index.html) command to create an account, and then use the account to connect to this database.
        Example:

        ```
        mongo --host dds-bp**********.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
        ```

        When `Enter password:` is displayed, enter the password of the database user and press the Enter key. If you forget the password of the root user, you can reset the password. For more information, see [Reset the password](/intl.en-US/Quick Start/Reset the password.md).

        **Note:** The password characters are not displayed when you enter the password.

    -   HA connection \(recommended\): You can use a connection string URI to connect to both the primary and secondary nodes of a replica set instance. This ensures that your application is always connected to the primary node and the read/write operations of your application are not affected even if the roles of the primary and secondary nodes are switched.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2074812261/p34449.png)

        Command syntax:

        ```
        mongo "<ConnectionStringURI>"    
        ```

        **Note:**

        -   The connection string URI must be enclosed in a pair of double quotation marks \(""\).
        -   <ConnectionStringURI\>: the connection string URI of the replica set instance.

            You must replace `****` in the connection string URI with the database password. For more information about how to set a database password, see [Reset the password](/intl.en-US/Quick Start/Reset the password.md).


## Common connection scenarios

-   [Connect to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance over the Internet.md)

    **Note:** Before you connect to a replica set instance over the Internet, we recommend that you enable SSL encryption. For more information, see [Use the mongo shell to connect to an ApsaraDB for MongoDB database in SSL encryption mode](/intl.en-US/User Guide/Data security/Use the mongo shell to connect to an ApsaraDB for MongoDB database in SSL encryption
         mode.md).

-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in
         different regions.md)
-   [Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud
         account.md)

## FAQ

-   [How to troubleshoot logon issues for the mongo shell](/intl.en-US/Product Usage/Database connections/The system prompts "Timeout while receiving message" when logging on to apsaradb for MongoDB through the Mongo Shell from a Linux instance.md)
-   [How to troubleshoot database connection failures after the number of connections reaches the upper limit](/intl.en-US/Product Usage/Database connections/How to troubleshoot database connection failures after the number of connections reaches the upper limit.md)
-   [Troubleshoot the high CPU usage of ApsaraDB for MongoDB](/intl.en-US/Best Practices/Performance/Troubleshoot the high CPU utilization of ApsaraDB for MongoDB.md)
-   [How to query and limit the number of connections](/intl.en-US/Product Usage/Database connections/How do I query and limit the number of connections?.md)

