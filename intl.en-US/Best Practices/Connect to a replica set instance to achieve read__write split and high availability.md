# Connect to a replica set instance to achieve read/write split and high availability {#concept_57670_zh .concept}

An ApsaraDB for MongoDB replica set instance provides multiple copies of data to ensure the high reliability of data. It also provides an automatic failover mechanism to guarantee the high availability of services. You need to use a correct method to connect to a replica set instance to achieve high availability. You can also configure the connection to split read and write.

## Before you start {#section_ebn_n5m_1gb .section}

-   The primary node of a replica set instance is not permanent. A failover between the primary and secondary nodes may be triggered when nodes of the replica set instance are upgraded in turn, the primary node is faulty, or the network is partitioned. In these scenarios, the replica set can elect a new primary node and downgrade the original primary node to a secondary node.
-   If you have used the address of the primary node to directly connect to the primary node of a replica set instance, the primary node needs to bear heavy load to process all read and write operations. If a failover is triggered in the replica set instance and the connected primary node is downgraded to a secondary node, you can no longer perform write operations and your business is seriously affected.

## Connection string URI {#section_t1w_2bn_1gb .section}

To correctly connect to a replica set instance, you need to understand the [connection string URI format](https://docs.mongodb.com/manual/reference/connection-string/) of MongoDB. All official MongoDB [drivers](https://docs.mongodb.com/manual/applications/drivers/) allow you to use a connection string URI to connect to MongoDB.

```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][? options]]
```

Notes:

-   mongodb://: The prefix, which indicates that this address is a connection string URI.
-   `username:password@`: The username and password used to log on to a database. If authentication is enabled, a password is required.
-   `hostX:portX`: The list of addresses used to connect to nodes in the replica set instance. Each address consists of an IP address and a port number. Multiple addresses are separated with commas \(,\).
-   `/database`: The database corresponding to the username and password if authentication is enabled.
-   `? options`: The additional connection options.

**Note:** For more information about the connection string URI, see [Connection String URI Format](https://docs.mongodb.com/manual/reference/connection-string/).

## Use a connection string URI to connect to a replica set instance {#section_j1s_4xm_1gb .section}

ApsaraDB for MongoDB allows you to use a connection string URI to connect to a replica set instance.

1.  Obtain the connection string URI of a replica set instance. For more information, see [Obtain the replica set instance connection information](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Obtain the replica set instance connection information.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6749/155624469433809_en-US.png)

2.  Use the obtained connection string URI to connect your applications to the instance. For more information, see [Connection sample code for MongoDB drivers](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connection sample code for MongoDB drivers.md#).

    **Note:** 

    To split read and write, you need to add `readPreference=secondaryPreferred` to **options** in a connection string URI to set read preference to secondary nodes.

    For more information about read preference options, see [Read Preference](https://docs.mongodb.com/manual/core/read-preference/).

    The following is an example of a connection string URI with the read preference specified:

    ```
    mongodb://root:xxxxxxxx@dds-xxxxxxxxxxxx:3717,xxxxxxxxxxxx:3717/admin? replicaSet=mgset-xxxxxx&readPreference=secondaryPreferred
    ```


After you use the preceding method to connect to a replica set instance, a client can preferentially send read requests to secondary nodes to achieve read/write split. In the meantime, the client automatically detects the relationship between the primary and secondary nodes. If the primary node is changed, the client automatically switches over write operations to the new primary node to guarantee the high availability of services.

