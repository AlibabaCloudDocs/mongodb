---
keyword: [connect to a specified database by using the mongo shell, ApsaraDB for MongoDB secure write, ApsaraDB for MongoDB logon methods, how to connect ApsaraDB for MongoDB, ApsaraDB for MongoDB password that you connect to a database]
---

# Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell

This topic describes how to connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell. The mongo shell is a database management tool that comes with MongoDB. You can install the mongo shell on your client or in an ECS instance.

-   The version of the mongo shell is the same as your instance. This ensures successful authentication. For more information about the installation procedure, visit [Install MongoDB](https://docs.mongodb.com/manual/installation/). Select the correct version based on your client.
-   The IP address of your client is added to a whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist for a standalone ApsaraDB for MongoDB instance]().

    **Note:** If you want to connect to the instance over the Internet, you must apply for a public endpoint. For more information, see [Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance]().


## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/)[ApsaraDB for MongoDB console](https://partners-intl.console.aliyun.com/#/dds).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection** to obtain the endpoint of the primary node.

    ![Obtain the endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1851166951/p13741.png)

    |Item|Description|
    |:---|:----------|
    |Connection type|    -   **Intranet Connection**: A virtual private cloud \(VPC\) is an isolated virtual network that provides higher security and higher performance than the classic network. By default, ApsaraDB for MongoDB provides endpoints on a VPC.
    -   **Public IP Connection**: By default, ApsaraDB for MongoDB instances do not provide public endpoints because connecting to instances over the Internet poses security risks. If you want to connect to a sharded cluster instance from a device outside Alibaba Cloud \(for example, a local client\), you must apply for a public endpoint. For more information, see [Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance](). |
    |**Node**|Primary: indicates the primary node of the ApsaraDB for MongoDB instance. You can connect to this node to perform read/write operations on the database.|
    |Address|The connection string of the primary node is in the format of `<host>:<port>`. **Note:**

    -   <host\>: the endpoint of the primary node.
    -   <port\>: the service port number of the primary node. |
    |The connection string URI is in the following format:     ```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][? options]]
    ```

    -   `mongodb://`: the prefix, which indicates a connection string URI.
    -   `username:password@`: the account and password used to log on to a database of the ApsaraDB for MongoDB instance. Separate the username and password with a colon \(:\).
    -   `hostX:portX`: the endpoint and port number of the instance.
    -   `/database`: the name of the authentication database to which the database account belongs.
    -   `? options`: additional connection options. |

6.  Run the following command on the local server or ECS instance where the mongo shell is installed to connect to the database:

    ```
    mongo --host <host:port> -u <username> -p --authenticationDatabase <database>
    ```

    **Note:**

    -   `<host:port>`: the endpoint of the primary node, which includes the domain name and port number.
    -   `<username>`: the database account of the ApsaraDB for MongoDB instance. The initial account is root. We recommend that you do not log on to a database as the root user in a production environment. You can create accounts and grant permissions to the accounts. For more information, see [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).
    -   `<database>`: the name of the authentication database to which the database account belongs. If the database account is root, enter admin. If you want to specify a database other than the authentication database, run the [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/index.html) command to create an account and then use the account to connect to the database.
    Example:

    ```
    mongo --host dds-bpxxxxxxxxxx.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  When `Enter password:` is displayed, enter the password for the database account and press Enter. If you forget the password of the root user, you can reset the password. For more information, see [Set a password for a standalone ApsaraDB for MongoDB instance]().

    **Note:** The password you enter is not displayed.


## Common connection scenarios

-   [Connect to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in
         different regions.md)
-   [Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud
         account.md)

## Related FAQ

-   [How do I troubleshoot logon issues for the mongo shell?](/intl.en-US/Product Usage/Hot issues/The system prompts "Timeout while receiving message" when logging on to apsaradb for MongoDB through the Mongo Shell from a Linux instance.md)
-   [How to troubleshoot database connection failures after the number of connections reaches the upper limit](/intl.en-US/Product Usage/Hot issues/How to troubleshoot database connection failures after the number of connections reaches
         the upper limit.md)
-   [How do I troubleshoot the high CPU utilization of ApsaraDB for MongoDB?](/intl.en-US/Best Practices/Performance/Troubleshoot the high CPU utilization of ApsaraDB for MongoDB.md)
-   [How do I query and limit the number of connections?](/intl.en-US/Product Usage/Hot issues/How do I query and limit the number of connections?.md)

