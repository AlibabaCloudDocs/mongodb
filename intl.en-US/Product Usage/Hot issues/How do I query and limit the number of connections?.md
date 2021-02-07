# How do I query and limit the number of connections?

This topic describes how to query the connection usage and how to specify the maximum number of connections for a connection pool. You can use Data Management \(DMS\) or the mongo shell to log on to ApsaraDB for MongoDB databases.

## Query the number of current connections

The maximum number of connections varies based on the specifications of the ApsaraDB for MongoDB instance that you purchase. For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

**Note:** The maximum number of connections applies to each node of the instance. For example, if you purchase a three-node replica set instance that has 1 vCPU and 2 GiB memory, up to 500 connections are allowed for each of the primary and secondary nodes of the instance. The hidden node does not provide services for external systems due to the special architecture of hidden nodes.

Use the mongo shell to connect to the instance. For more information, see [Connect to an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance.md). Then, run the `db.serverStatus().connections` command.

```
mgset-123456:PRIMARY> db.serverStatus().connections
{
        "current" : 1,
        "available" : 999,
        "internal_current" : 10,
        "internal_available" : 990,
        "totalCreated" : 632
}             
```

**Note:** Take note of the following parameters and the values of the parameters.

-   "current": the number of established connections.
-   "available": the number of available connections.

## Query the source IP addresses of the current connections

1.  Use the mongo shell to connect to an ApsaraDB for MongoDB instance. For more information, see [Connect to an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance.md). Then, switch to the admin database.

    ```
    use admin
    ```

2.  Run the `db.runCommand({currentOp: 1, $all: true})` command.

    ```
    mgset-123456:PRIMARY> db.runCommand({currentOp: 1, $all:[{"active" : true}]})                    
    ```


You can query the source IP address of each connection in the command output. This way, you can obtain the number of connections that are established between each terminal and the ApsaraDB for MongoDB instance. For more information, visit [db.currentOp\(\)](https://docs.mongodb.com/manual/reference/method/db.currentOp/index.html).

## Limit the number of connections

You can use a connection string URI to connect to an ApsaraDB for MongoDB instance. If you use a connection string URI to connect to a database, append `&maxPoolSize=<integer>` to the URI. maxPoolSize specifies the maximum number of connections in the connection pool.

The following code shows how to use the mongo shell to connect to the database. The maximum number of connections is set to 10 in this example.

```
mongo "mongodb://root:xxxxxx@dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717/admin? replicaSet=mgset-xxxxxx&maxPoolSize=10"
```

**Note:** For more information about how to limit the number of connections in the connection pool for clients in different programming languages, visit [Start Developing with MongoDB](https://docs.mongodb.com/ecosystem/drivers/).

