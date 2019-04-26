# Use a connection string URI to connect to a sharded cluster instance {#concept_51059_zh .concept}

An ApsaraDB for MongoDB sharded cluster instance provides connection information for each mongos node. You can connect to a mongos node to access ApsaraDB for MongoDB. However, you need to use a correct method to connect to a sharded cluster instance to achieve load balancing and high availability.

## Background {#section_n22_mpv_mgb .section}

![Sharded cluster architecture](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6750/155624507337678_en-US.png)

A MongoDB sharded cluster distributes and stores data on multiple shards to facilitate high scalability. When creating a sharded cluster, MongoDB introduces a config server to store the metadata of the cluster and introduces one or more mongos nodes to provide the entry to the cluster for applications. The mongos nodes read routing information from the config server to route requests to corresponding shards at the backend.

-   When you connect to a mongos node, it can function as a mongod process.
-   All mongos nodes are equal. You can connect to one or more mongos nodes to access a sharded cluster.
-   The mongos nodes are stateless and can be scaled out as required. The service capability of a sharded cluster is subject to the smaller one between the total service capability of shards and that of mongos nodes.
-   When you access a sharded cluster, we recommend that you share the load of applications evenly among multiple mongos nodes.

## Connection string URI { .section}

To correctly connect to a sharded cluster instance, you need to understand the [connection string URI format](https://docs.mongodb.com/manual/reference/connection-string/) of MongoDB. All official MongoDB [drivers](https://docs.mongodb.com/manual/applications/drivers/) allow you to use a connection string URI to connect to MongoDB.

The following example shows a connection string URI.

```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][? options]]
```

**Note:** 

-   `mongodb://`: The prefix, which indicates that this address is a connection string URI.
-   `username:password@`: The username and password used to log on to a database if authentication is enabled.
-   `hostX:portX`: The list of addresses used to connect to mongos nodes.
-   `/database`: The database corresponding to the username and password if authentication is enabled.
-   `? options`: The additional connection options.

## Use a connection string URI to connect to a sharded cluster instance {#section_tm2_lqv_mgb .section}

ApsaraDB for MongoDB allows you to use a connection string URI to connect to a sharded cluster instance to achieve load balancing and high availability.

1.  Obtain the connection string URI of a sharded cluster instance. For more information, see [Retrieve the seven connection elements](https://www.alibabacloud.com/help/doc-detail/55188.htm).

    ![Connection string URI](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6750/155624507337679_en-US.png)

2.  Use the obtained connection string URI to connect your applications to the instance. For more information, see [MongoDB driver connection](https://www.alibabacloud.com/help/doc-detail/55250.htm).

    The following is an example of the Java sample code:

    ```language-java
    MongoClientURI connectionString = new MongoClientURI("mongodb://:****@s-xxxxxxxx.mongodb.rds.aliyuncs.com:3717,s-xxxxxxxx.mongodb.rds.aliyuncs.com:3717/admin"); // Replace **** with the password of the root user.
    MongoClient client = new MongoClient(connectionString);
    MongoDatabase database = client.getDatabase("mydb");
    MongoCollection<Document> collection = database.getCollection("mycoll");
    ```

    **Note:** 

    After you use the preceding method to connect to a sharded cluster instance, a client can automatically distribute requests to multiple mongos nodes to balance their load. In the meantime, if you have used a connection string URI to connect to two or more mongos nodes and a mongos node is faulty, the client can automatically skip this faulty node and distribute requests to the other functional mongos nodes.


If there are many mongos nodes, you can group them by application. For example, you have application A, application B, and four mongos nodes. You can specify only the connection addresses of mongos 1 and mongos 2 in the URI for application A, and specify only the connection addresses of mongos 3 and mongos 4 in the URI for application B. In this way, you can isolate mongos nodes to provide separate entry for different applications.

**Note:** Although applications are connected to mutually isolated mongos nodes, they share shards at the backend.

## Common connection options { .section}

-   Split read and write

    Add `readPreference=secondaryPreferred` to **options** in a connection string URI to set read preference to secondary nodes of shards.

    The following is an example of a connection string URI with the read preference specified:

    ```
    mongodb://root:xxxxxxxx@dds-xxxxxxxxxxxx:3717,xxxxxxxxxxxx:3717/admin? replicaSet=mgset-xxxxxx&readPreference=secondaryPreferred
    ```

-   Limit connections

    Add `maxPoolSize=xx` to **options** in a connection string URI to limit the maximum number of connections in the connection pool of a client to xx.

-   Guarantee acknowledgement after data has been written to the majority of nodes

    Add `w=majority` to **options** in a connection string URI to guarantee that ApsaraDB for MongoDB sends acknowledgement to a client after writing data to the majority of nodes for a write request.


