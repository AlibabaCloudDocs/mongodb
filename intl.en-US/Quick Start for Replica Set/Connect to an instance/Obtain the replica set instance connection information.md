# Obtain the replica set instance connection information {#concept_44623_zh .concept}

An ApsaraDB for MongoDB replica set instance provides separate addresses for you to connect to the primary and secondary nodes, and a connection string URI for you to connect your applications to the instance in high availability mode.

## Required information {#section_in3_5c1_wfb .section}

Before connecting to an ApsaraDB for MongoDB instance, obtain the following information:

-   Database name, which is admin by default
-   Username of an instance account
-   Password of the instance account
-   Connection information
    -   Domain names and port numbers of the primary and secondary nodes
    -   Connection string URI for the high availability mode

## Procedure { .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  Click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6671/155609832613267_en-US.png)** \> **More**in the Operation column corresponding to the target instance.
3.  On the Basic Information page that appears, you can view the connection string URI for connections in high availability mode and the connection information of the primary and secondary nodes \(including their domain names and port numbers\), as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6672/155609832613778_en-US.png)

4.  In the left-side navigation pane, click **Accounts** to view the username, which is root by default.

    **Note:** You can set a database logon password when creating an instance or reset the password after creating the instance. For more information, see [Set a password](intl.en-US/Quick Start for Replica Set/Set a password.md#).


## Connection instructions { .section}

ApsaraDB for MongoDB provides two connection modes for a replica set instance as follows:

-   Separate addresses for you to connect to the primary and secondary nodes of the instance.
    -   If you connect to the primary node, you have read and write permissions.
    -   If you connect to a secondary node, you have only the read permission.
    -   During daily testing, you can use this connection mode to directly connect to the primary node or a secondary node.
    -   We do not recommend that you use these separate addresses to directly connect your online applications to an instance. If you do so and a failover is triggered between the primary and secondary nodes, read and write operations may be affected in your applications.
-   A connection string URI for you to connect to the instance to achieve load balancing.

    **Note:** We recommend that you use the connection string URI to connect your applications in the production environment to an instance. In this case, if a node is faulty and a failover is triggered between the primary and secondary nodes, the connection of your applications is not affected.

    The following example shows a connection string URI that you can obtain from the console.

    ```
    mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][? options]]
    ```

    Notes:

    -   mongodb://: The prefix, which indicates that this address is a connection string URI.
    -   username:password@: The username and password used to log on to a database. If authentication is enabled, a password is required.
    -   hostX:portX: The list of addresses used to connect to nodes in the replica set.
    -   /database: The database corresponding to the username and password if authentication is enabled.
    -   ? options: The additional connection options.
-   All official MongoDB drivers support the connection to an instance by using a connection string URI. For more information, see [Connection sample code for MongoDB drivers](https://www.alibabacloud.com/help/doc-detail/44630.htm).


