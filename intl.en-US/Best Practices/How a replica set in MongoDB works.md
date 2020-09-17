# How a replica set in MongoDB works

A replica set in ApsaraDB for MongoDB is a group of mongod processes and contains a primary node and multiple secondary nodes. MongoDB drivers write data to the primary node only. Then, data is synchronized from the primary node to secondary nodes. This ensures data consistency across all nodes in the replica set. Therefore, replica sets provide high availability.

The following figure is extracted from the official documentation of MongoDB. It shows a typical MongoDB replica set that contains one primary node and two secondary nodes.

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/52344/cn_zh/1491806556479/1.png)

## Primary node election \(1\)

A replica set is initialized by running the `replSetInitiate` command or running the `rs.initiate()` command in the mongo shell. After the replica set is initialized, the members send heartbeat messages to each other and initiate the primary node election. The node that receives votes from a majority of the members becomes the primary node and the other nodes become secondary nodes.

Initialize the replica set

```
    config = {
        _id : "my_replica_set",
        members : [
             {_id : 0, host : "rs1.example.net:27017"},
             {_id : 1, host : "rs2.example.net:27017"},
             {_id : 2, host : "rs3.example.net:27017"},
       ]
    }
    rs.initiate(config)
```

Definition of majority

A group of voting members is considered a majority only if it contains members of more than the average of the total number of members. If the number of members in a replica set is equal to or less than the average number of all voting members, the election cannot be implemented. In this case, you cannot write data to the replica set.

|Number of voting members|Majority|Maximum number of failed nodes|
|:-----------------------|:-------|:-----------------------------|
|1|1|0|
|2|2|0|
|3|2|1|
|4|3|1|
|5|3|2|
|6|4|2|
|7|4|3|

We recommend that you set the number of members in a replica set to an odd number. The preceding table shows that both a replica set with three nodes and a replica set with four nodes tolerate the failure of one node. The two replica sets provide the same service availability. However, the replica set with four nodes provides more reliable data storage.

## Special secondary nodes

Secondary nodes of a replica set participate in the primary node election. A secondary node may also be elected as the primary node. The latest data written to the primary node is synchronized to secondary nodes to ensure data consistency across all nodes.

You can read data from secondary nodes. Therefore, you can add secondary nodes to a replica set to improve the read performance and service availability of the replica set. ApsaraDB for MongoDB allows you to configure secondary nodes of a replica set to meet the requirements of different scenarios.

-   Arbiter

    An arbiter node participates in the election as a voter only. It cannot be elected as the primary node or synchronize data from the primary node.

    Assume that you deploy a replica set that contains one primary node and one secondary node. If one node fails, the primary node election cannot be implemented. As a result, the replica set becomes unavailable. In this case, you can add an arbiter node to the replica set to enable primary node election.

    An arbiter node is a lightweight node that does not store data. If the number of members in a replica set is an even number, we recommend that you add an arbiter node to increase the availability of the replica set.

-   Priority0

    A node that has priority 0 in the primary node election cannot be elected as the primary node.

    Assume that you deploy a replica set that contains nodes in both Data center A and Data center B. To ensure that the elected primary node is deployed in Data center A, set the priorities of the replica set members in Data center B to 0.

    **Note:** If you set the priorities of the members in Data center B to 0, we recommend that you deploy a majority of replica set nodes in Data center A. Otherwise, the primary node election may fail during network partitioning.

-   Vote0

    In MongoDB 3.0, a replica set contains a maximum of 50 members, and up to seven members can vote in a primary node election. You must set the members\[n\].votes attribute to 0 for members that are not expected to vote.

-   Hidden

    A hidden member in a replica set cannot be elected as the primary node because its priority is 0. Hidden nodes are invisible to MongoDB drivers.

    You can use hidden nodes to back up data or perform offline computation tasks. This does not affect the services of the replica set because hidden nodes do not process requests from MongoDB drivers.

-   Delayed

    A delayed node must be a hidden node. Data on a delayed node reflects an earlier state of the data on the primary node. If you configure a one-hour delay, data on the delayed node is the same as the data on the primary node an hour ago.

    Therefore, if you write incorrect or invalid data to the primary node, you can use the data on the delayed node to restore the data on the primary node to an earlier state.


## Primary node election \(2\)

A primary node election is triggered not only after replica set initialization but also in the following scenarios:

-   Replica set reconfiguration

    A primary node election is triggered if the primary node fails or voluntarily steps down and becomes a secondary node. A primary node election is affected by various factors, such as heartbeat messages among nodes, priorities of nodes, and the time when the last oplog entry was generated.

    -   Node priorities

        All nodes tend to vote for the node that has the highest priority. A priority 0 node cannot trigger primary node elections. If a secondary node has a higher priority than the primary node and the time difference between the latest log entry of the secondary node and that of the primary node is within 10 seconds, the primary node steps down. In this case, this secondary node becomes a candidate for the primary node.

    -   Optime

        Only secondary nodes that have the latest oplog entry are eligible to be elected as the primary node.

-   Network partitioning

    Only nodes that are connected to a majority of voting nodes can be elected as the primary node. If the primary node is disconnected from a majority of the other nodes in the replica set, the primary node voluntarily steps down and becomes a secondary node. A replica set may have multiple primary nodes for a short period of time during network partitioning. When MongoDB drivers write data, we recommend that you set a policy that allows data synchronization from only the primary node that is connected to a majority of nodes.


## Data synchronization

Data is synchronized from the primary node to secondary nodes based on the oplog. After a write operation on the primary node is complete, an oplog entry is written to the special local.oplog.rs collection. Secondary nodes constantly import new oplog entries from the primary node and apply the operations.

To prevent unlimited growth in the size of the oplog, local.oplog.rs is configured as a capped collection. When the amount of oplog data reaches the specified threshold, the earliest entries are deleted. All operations in the oplog must be idempotent. This ensures that an operation produces the same results regardless of whether it is repeatedly applied to secondary nodes.

The following code block is a sample oplog entry, which contains fields such as ts, h, op, ns, and o:

```
    {
      "ts" : Timestamp(1446011584, 2),
      "h" : NumberLong("1687359108795812092"), 
      "v" : 2, 
      "op" : "i", 
      "ns" : "test.nosql", 
      "o" : { "_id" : ObjectId("563062c0b085733f34ab4129"), "name" : "mongodb", "score" : "100" } 
    }
```

-   ts: the time when the operation was performed. The value contains two numbers. The first number is a UNIX timestamp. The second number is a counter that indicates the serial number of each operation that occurs within a second. The counter is reset every second.
-   h: the unique identifier of the operation
-   v: the version of the oplog
-   op: the type of the operation
-   i: insert
-   u: update
-   d: delete
-   c: run commands such as createDatabase and dropDatabase
-   n: null. This value is used for special purposes.
-   ns: the collection on which the operation is performed
-   o: the operation details. This field is valid for update operations only.
-   o2: the conditions of an update operation. This field is valid for update operations only.

During the initial synchronization, a secondary node runs the `init sync` command to synchronize all data from the primary node or another secondary node that stores the latest data. Then, the secondary node continuously uses the `tailable cursor` feature to query the latest oplog entries in the local.oplog.rs collection of the primary node and applies the operations in these oplog entries.

The initial synchronization process includes the following steps:

1.  Before the time of T1, the data synchronization tool runs the `listDatabases`, `listCollections`, and `cloneCollection` commands. At the time of T1, all data in the cloud databases \(except the local.oplog.rs database\) starts to be synchronized from the primary node to the secondary node. Assume that the synchronization is completed at the time of T2.
2.  All the operations in oplog entries generated from T1 to T2 are applied to the secondary node. Operations in oplog entries are idempotent. Therefore, operations that have been applied in Step 1 can be reapplied.
3.  Based on the index for each collection on the primary node, indexes for the corresponding collections are created on the secondary node. The index for each collection on the primary node was created in Step 1.

    **Note:** You must configure the oplog size based on the database size and the volume of data to be written by the application. If the oplog is oversized, the storage space may be wasted. If the oplog size is too small, the secondary node may fail to complete initial synchronization. For example, in Step 1, if the database stores a large amount of data and the oplog is not large enough, the oplog may fail to store all the oplog entries generated from T1 to T2. As a result, the secondary node cannot synchronize all the data sets from the primary node.


Modify a replica set

You can modify a replica set by running the `replSetReconfig` command or running the `rs.reconfig()` command in the mongo shell. For example, you can add or delete members, and change the priority, vote, hidden, and delayed attributes of a member.

For example, you can run the following command to set the priority of the second member in the replica set to 2:

```
    cfg = rs.conf();
    cfg.members[1].priority = 2;
    rs.reconfig(cfg);
```

Roll back operations on the primary node

Assume that the primary node of a replica set fails. If write operations have been performed on the new primary node when the former primary node rejoins the replica set, the former primary node must roll back operations that have not been synchronized to other nodes. This ensures data consistency between the former primary node and the new primary node.

The former primary node writes the rollback data to a dedicated directory. This allows the database administrator to run the `mongorestore` command to restore operations as needed.

## Replica set read/write settings

-   Read Preference

    By default, all the read requests for a replica set are routed to the primary node. However, you can modify the read preference modes on the drivers to route read requests to other nodes.

    -   primary: This is the default mode. All read requests are routed to the primary node.
    -   primaryPreferred: Read requests are routed to the primary node preferentially. If the primary node is unavailable, read requests are routed to secondary nodes.
    -   secondary: All read requests are routed to secondary nodes.
    -   secondaryPreferred: Read requests are routed to secondary nodes preferentially. If all secondary nodes are unavailable, read requests are routed to the primary node.
    -   nearest: Read requests are routed to the nearest reachable node, which can be detected by running the `ping` command.
-   Write Concern

    By default, the primary node returns a message that indicates a successful write operation after data is written to the primary node. You can set the write concern on drivers to specify the rule for a successful write operation. For more information, see [Write concern](https://docs.mongodb.org/manual/core/write-concern/?spm=a2c4g.11186623.2.18.4a4262d7fa2tVZ).

    The following write concern indicates that a write operation is successful only after the data is written to a majority of nodes before the request times out. The timeout period is five seconds.

    ```
        db.products.insert(
          { item: "envelopes", qty : 100, type: "Clasp" },
          { writeConcern: { w: majority, wtimeout: 5000 } }
        )
    ```

    The preceding settings apply to individual requests. You can also modify the default write concern of a replica set. The write concern of a replica set applies to all the requests for the replica set.

    ```
        cfg = rs.conf()
        cfg.settings = {}
        cfg.settings.getLastErrorDefaults = { w: "majority", wtimeout: 5000 }
        rs.reconfig(cfg)
    ```


