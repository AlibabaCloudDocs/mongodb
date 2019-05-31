# Connect to an ApsaraDB for MongoDB instance {#concept_oq1_gx1_ffb .concept}

MongoDB sharded cluster instances provide individual addresses to connect to mongos as well as high-availability connection string URIs to connect to applications. This topic describes how to obtain and connect to these two address types.

## Obtain the instance address {#section_j4s_pg1_ffb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the homepage, select the region of the instance.
3.  In the left-side navigation pane, click **Sharding instances**.
4.  Locate the target instance, and then click the instance ID.
5.  On the Basic Information page that appears, click **Database Connection** in the left-side navigation pane to view the addresses of the instance.

    You can see the internal and public IP addresses of all mongos in the instance. \(**Domain Information** is addresses\).

    As shown in the following figure, the instance has three mongos. Each mongos has a different address but uses the same port, 3717. You can log on to the instance through any mongos.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6691/155926656013833_en-US.png)


## Connection information description {#section_l5y_zst_2gb .section}

|Parameter|Description|
|:--------|:----------|
|Network Type| -   Intranet Connection – Classic Network: Cloud services in a classic network are not isolated. Security groups or whitelist policies can be used to block unauthorized access to such services.
-   Intranet Connection – VPC: Virtual Private Cloud \(VPC\) is an isolated network environment with higher security and performance than the classic network. You need to create VPCs in advance. For more information, see [Configure VPC for a new instance](https://www.alibabacloud.com/help/zh/doc-detail/65402.htm).
-   Public IP Connection: Instances are not configured with a public IP address by default to ensure security. You must apply for a public IP address for the instance manually. For more information, see [Apply for a public IP address](intl.en-US/Quick Start for Cluster/Apply for a public IP address.md#).

 |
|mongos ID|The address of a mongos that you obtain from the console is in the following format:```
<host>:<port>
```

-   <host\>: the domain address used to connect to the instance.
-   <port\>: the port used to connect to the instance.

**Note:** During routine tests, you can directly connect to any mongos. Take note that the client cannot provide load balancing and failover when you are only connected to a single mongos.

|
|Connection string URI|The connection string URI you obtain from the console is in the following format:```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][? options]]
```

-   mongodb://: the prefix, representing a connection string URI.
-   username:password@: the username and password used to connect to the instance. Separate them with a colon \(:\).
-   hostX:portX: the address of a mongos in the instance.
-   /database: the name of the authentication database for the instance.
-   ? options: additional connection options.

**Note:** We recommend that in the production environment you use connection string URIs to connect ApsaraDB for MongoDB instances from applications. The client can provide load balancing by automatically distributing requests to multiple mongos. When a mongos fails, the client can automatically fail over to another mongos in the normal state.

|

## Connect to an ApsaraDB for MongoDB instance {#section_j5s_yg1_ffb .section}

1.  In addition to the preceding [Database Connection](#section_j4s_pg1_ffb) information, you also need to obtain the following information.
    -   The username used to connect to the instance.

        **Note:** We recommend that you do not log on to an ApsaraDB for MongoDB instance in the production environment as the root user. You can log on to the instance as the root user, and then create users and grant permissions. For more information, see [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/).

    -   The password used to connect to the instance. If you forget the password of the root account, you can reset the password by using the method specified in [Set a password](intl.en-US/Quick Start for Replica Set/Set a password.md#).
    -   Log on to the authentication database with the corresponding authentication information of the instance. If you log on to the instance as the root user, use the admin information for authentication.
2.  Log on to the ApsaraDB for MongoDB instance.
    -   [Connect to an ApsaraDB for MongoDB instance through the mongo shell](intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance through the mongo shell.md#)
    -   [Connect to an ApsaraDB for MongoDB instance through the program code](intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance through the program code.md#)

