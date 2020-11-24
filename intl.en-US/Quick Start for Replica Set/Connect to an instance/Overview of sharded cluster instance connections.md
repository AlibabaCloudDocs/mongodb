# Overview of sharded cluster instance connections

ApsaraDB for MongoDB supports both connection strings and connection string URIs. You can use a connection string to connect to one mongos, and use a connection string URI to connect to more mongos. For high availability, we recommend that you use connection string URIs to connect your application to more mongos. This topic provides an overview of sharded cluster instance connections.

## View connection strings

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection** to view connection strings.

    ![Connection strings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2378317951/p13833.png)


## Description of connection strings

|Item|Description|
|:---|:----------|
|Type|-   Intranet Connection - Classic Network: Cloud services on a classic network are not isolated. Unauthorized access can only be blocked by using security groups or whitelists.
-   Intranet Connection - VPC: A VPC is an isolated network with higher security and performance than a classic network. By default, an ApsaraDB for MongoDB instance provides VPC connection addresses.
-   Public IP Connection: Connecting to a sharded cluster instance over the Internet is risky. Therefore, ApsaraDB for MongoDB does not provide public endpoints. If you want to connect to a sharded cluster instance from a device outside Alibaba Cloud \(for example, a local client\), you must apply for a public endpoint. For more information, see [Apply for a public endpoint for a sharded cluster instance](/intl.en-US/Quick Start for Cluster/Apply for a public endpoint for a sharded cluster instance.md). |
|mongos ID|The connection string of a mongos is in the following format: ```
<host>:<port>
```

-   <host\>: the endpoint used to connect to the sharded cluster instance.
-   <port\>: the port used to connect to the sharded cluster instance.

**Note:** During regular tests, you can use a connection string to directly connect to a mongos. |
|Connection string URI|A connection string URI is in the following format: ```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
```

-   mongodb://: the prefix, indicating a connection string URI.
-   username:password@: the username and password used to log on to a database of the sharded cluster instance. You must separate the username and password with a colon \(:\).
-   hostX:portX: the endpoint and port of a mongos in the sharded cluster instance.
-   /database: the database corresponding to the username and password if authentication is enabled.
-   ?options: additional connection options.

**Note:** If your application is in a production environment, we recommend that you use a connection string URI to connect to the instance. Then your client can automatically distribute your requests to multiple mongos to balance loads. When a mongos fails, your client automatically redirects requests to other mongos in the normal state. |

## Log on to a database of the sharded cluster instance

1.  Obtain the [connection strings](#section_e2o_ajm_d6k) and the following information:

    -   The username used to log on to the database. The initial username is root.

        **Note:** We recommend that you do not log on to a database as the root user in a production environment. You can create accounts and grant permissions to them based on your needs. For more information, see [Manage MongoDB users through DMS]().

    -   The password of the database user. If you forget the password of the root user, you can reset it. For more information, see [Set a password for a sharded cluster instance](/intl.en-US/Quick Start for Replica Set/Set a password for a replica set instance.md).
    -   The name of the database corresponding to the username if authentication is enabled. If the username is root, enter admin.
2.  Log on to the database.

    -   [Connect to a sharded cluster ApsaraDB for MongoDB instance through DMS](/intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to a sharded cluster ApsaraDB for MongoDB instance through DMS.md)
    -   [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md)
    -   [Connect to an ApsaraDB for MongoDB instance through the program code](/intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance through the program code.md)

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

