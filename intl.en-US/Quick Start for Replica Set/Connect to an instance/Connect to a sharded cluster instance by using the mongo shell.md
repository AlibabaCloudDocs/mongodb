# Connect to a sharded cluster instance by using the mongo shell

This topic describes how to connect to a sharded cluster instance by using the mongo shell, which is a database management tool provided with MongoDB. You can install the mongo shell on your client or an ECS instance.

-   To ensure successful authentication, the version of the mongo shell must match with that of the ApsaraDB for MongoDB instance. For more information about the installation procedure, visit [Install MongoDB](https://docs.mongodb.com/manual/installation/). Select the correct version based on your client.
-   The IP address of your client is added to a whitelist of the sharded cluster instance. For more information, see [Configure a whitelist for a sharded cluster instance](/intl.en-US/Quick Start for Cluster/Configure a whitelist for a sharded cluster instance.md).

    **Note:** If you want to connect to the instance over the Internet, you must [apply for a public endpoint](/intl.en-US/Quick Start for Cluster/Apply for a public endpoint for a sharded cluster instance.md).


## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection** to obtain the connection string of a mongos.

    ![Connection strings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2378317951/p13833.png)

6.  Connect to the sharded cluster instance from your client or ECS instance that has the mongo shell installed.

    ```
    mongo --host <mongos_host> -u <username> -p --authenticationDatabase <database>
    ```

    **Note:**

    -   <mongos\_host\>: the connection string of a mongos in the sharded cluster instance.
    -   <username\>: the username used to log on to a database of the sharded cluster instance. The initial username is root. We recommend that you do not log on to a database as the root user in a production environment. You can create accounts and grant permissions to them as needed. For more information, see [Manage MongoDB users though DMS]().
    -   <database\>: the name of database corresponding to the username if authentication is enabled. If the username is root, enter admin.
    Example:

    ```
    mongo --host s-bp**********.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  When `Enter password:` is displayed, enter the password of the database user and press Enter. If you forget the password of the root user, you can reset it. For more information, see [Set a password for a sharded cluster instance](/intl.en-US/Quick Start for Cluster/Set a password for a sharded cluster instance.md).

    **Note:** The password characters are not displayed when you enter the password.


## Common connection scenarios

-   [Connect a local client to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account.md)

## FAQ

-   [How to troubleshoot logon issues for the mongo shell](/intl.en-US/Product Usage/Hot issues/The system prompts "Timeout while receiving message" when logging on to apsaradb for MongoDB through the Mongo Shell from a Linux instance.md)
-   [How to troubleshoot database connection failures after the number of connections reaches the upper limit](/intl.en-US/Product Usage/Hot issues/Database connection failures caused by exhausted connections to apsaradb for MongoDB instances.md)
-   [How to troubleshoot the high CPU utilization of ApsaraDB for MongoDB](/intl.en-US/Best Practices/Performance/Troubleshoot the high CPU usage of ApsaraDB for MongoDB.md)
-   [How to query and limit the number of connections](/intl.en-US/Product Usage/Hot issues/How to query and limit the number of connections to an apsaradb for MongoDB instance.md)

