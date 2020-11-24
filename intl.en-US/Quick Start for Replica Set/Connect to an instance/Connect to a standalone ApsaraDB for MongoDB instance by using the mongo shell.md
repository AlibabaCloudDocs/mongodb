# Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell

This topic describes how to connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell, which is a database management tool built in MongoDB. You can install the mongo shell on your client or in an ECS instance.

-   Mongo shell 3.0 or later is installed to ensure successful authentication. For more information about the installation process, visit [Install MongoDB](https://docs.mongodb.com/v3.4/installation/) at the official MongoDB website.
-   The IP address of your client is added to a whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist for a standalone ApsaraDB for MongoDB instance](/intl.en-US/Quick Start for Standalone/Configure a whitelist for a standalone ApsaraDB for MongoDB instance.md).

    **Note:** If you want to connect to the instance over the Internet, you must [apply for a public endpoint](/intl.en-US/Quick Start for Standalone/Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance.md).


## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection** to obtain the connection addresses of the primary node.

    ![Obtain the connection addresses](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1851166951/p13741.png)

    |Item|Description|
    |:---|:----------|
    |Address type|    -   **Intranet Connection**: A VPC is an isolated virtual network with better security and performance than a classic network. By default, an ApsaraDB for MongoDB instance provides VPC connection addresses.
    -   **Public IP Connection**: By default, ApsaraDB for MongoDB instances do not provide public connection addresses because connecting to instances over the Internet poses security risks. If you want to connect to an ApsaraDB for MongoDB instance from a device outside of Alibaba Cloud \(such as a local device\), you must apply for a public endpoint. For more information, see [Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance](/intl.en-US/Quick Start for Standalone/Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance.md). |
    |**Node**|Primary: indicates the primary node of the ApsaraDB for MongoDB instance. You can connect to this node to perform read/write operations on the database.|
    |Connection string|The address of the primary node is in the format of `<host>:<port>`. **Note:**

    -   <host\>: the endpoint of the primary node.
    -   <port\>: the service port of the primary node. |
    |The connection string URI is in the following format:     ```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][? options]]
    ```

    -   `mongodb://`: the prefix, indicating a connection string URI.
    -   `username:password@`: the username and password used to connect to the ApsaraDB for MongoDB instance. Separate them with a colon \(:\).
    -   `hostX:portX`: the endpoint and port number of the instance.
    -   `/database`: the name of the authentication database. It is the database where the database account is created.
    -   `? options`: additional connection options. |

6.  Run the following command on the local server or ECS instance where the mongo shell is installed to connect to the database:

    ```
    mongo --host <host:port> -u <username> -p --authenticationDatabase <database>
    ```

    **Note:**

    -   <host:port\>: the connection string of the primary node, including the endpoint and port number.
    -   <username\>: the database account of the ApsaraDB for MongoDB instance. The initial account is root. We recommend that you do not log on to a database as the root user in the production environment. You can create users and grant permissions based on your business needs. For more information, see [Manage MongoDB users though DMS]().
    -   <database\>: the name of the authentication database. It is the database where the database account is created. If the database account is root, enter admin.
    Example:

    ```
    mongo --host dds-bpxxxxxxxxxx.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  When `Enter password:` is displayed, enter the password for the database user and press Enter. If you forgot the password for the root user, you can reset it. For more information, see [Set a password](/intl.en-US/Quick Start for Standalone/Set a password for a standalone ApsaraDB for MongoDB instance.md).

    **Note:** The password you enter is not displayed.


## Common connection scenarios

-   [Connect a local client to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account.md)

## FAQ

-   [How to troubleshoot logon issues for the mongo shell](/intl.en-US/Product Usage/Hot issues/The system prompts "Timeout while receiving message" when logging on to apsaradb for MongoDB through the Mongo Shell from a Linux instance.md)
-   [How to troubleshoot database connection failures after the number of connections reaches the upper limit](/intl.en-US/Product Usage/Hot issues/Database connection failures caused by exhausted connections to apsaradb for MongoDB instances.md)
-   [How to troubleshoot high CPU utilization of ApsaraDB for MongoDB](/intl.en-US/Best Practices/Performance/Troubleshoot the high CPU usage of ApsaraDB for MongoDB.md)
-   [How to query and limit the number of connections](/intl.en-US/Product Usage/Hot issues/How to query and limit the number of connections to an apsaradb for MongoDB instance.md)

