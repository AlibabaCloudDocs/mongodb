# Architecture of sharded cluster instances

A sharded cluster instance consists of three components: mongos, shard, and Configserver. You can choose the configuration and number of mongos and shards to create ApsaraDB for MongoDB sharded cluster instances that have different performance.

## Architecture

![Architecture of an ApsaraDB for MongoDB sharded cluster instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3801129951/p39656.png)

## Components

|Component|Architecture|Description|
|:--------|:-----------|:----------|
|Mongos|Standalone architecture|Routes queries and writes to the corresponding shards.

You can purchase multiple mongos in the console to implement load balancing and failover. A single sharded cluster instance supports 2 to 32 mongos. |
|Shard|Replica set architecture \(three nodes\)|Stores database data.

You can purchase multiple shards in the console to scale out the capacity of data storage and concurrent read/write operations. A single sharded cluster instance supports 2 to 32 shards. |
|Configserver|Replica set architecture \(three nodes\)|Stores the metadata for clusters and shards. The metadata contains the data distribution information about each shard in a cluster.

**Note:** You cannot change the specifications of the Configserver \(one core, 2 GB memory, and 20 GB disk storage capacity\). |

**Related topics**  


[Architecture of standalone instances](/intl.en-US/Product Introduction/System architecture/Architecture of standalone instances.md)

[Architecture of replica set instances](/intl.en-US/Product Introduction/System architecture/Architecture of replica set instances.md)

