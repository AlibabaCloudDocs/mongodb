# What is ApsaraDB for MongoDB {#concept_egq_tvn_tdb .concept}

ApsaraDB for MongoDB is a stable, reliable, and scalable database service that fully complies with the MongoDB protocols. The service provides a complete database solution for disaster recovery, data backup, data recovery, monitoring, and alerts.

ApsaraDB for MongoDB supports flexible deployment architecture. It provides standalone, replica set, and sharded cluster instances to meet requirements in different business scenarios.

-   **Standalone instance**: A standalone instance applies to development, testing, and other scenarios where non-core enterprise data is stored. It enables you to purchase ApsaraDB for MongoDB at a lower entry-level price to enjoy its superiority in O&M support and kernel-level optimization. The standalone architecture can adapt ApsaraDB for MongoDB to various scenarios to help enterprises minimize their costs and expenses.
-   **Replica set instance**:
    -   Three-node replica set: ApsaraDB for MongoDB automatically creates a three-node replica set. You can directly perform operations on the primary node and a secondary node, whereas the other secondary node is hidden. Advanced features such as disaster recovery switchover and failover are packaged to ensure that they are completely transparent to you when you use the instance.
    -   Replica set with more nodes \(such as a five-node or seven-node replica set\): You can increase nodes to apply the replica set instance to certain business scenarios that require databases with better read performance, such as reading websites and order query systems where there are more read operations than write operations, or scenarios with burst business requirements such as temporary activities. You can add or delete secondary nodes on demand to flexibly scale out or in the read performance of ApsaraDB for MongoDB.
-   **Sharded cluster instance**: A sharded cluster instance is created based on multiple three-node replica sets. Each sharded cluster instance consists of three components: mongos, shard, and config server. You can specify the number and configuration of mongos nodes and shards as required to create ApsaraDB for MongoDB clusters that provide different service capabilities.

    **Note:** 

    -   Mongos: A service agent configured with only one node. You can purchase multiple mongos nodes to achieve load balancing and failover. A sharded cluster instance supports 2–32 mongos nodes.
    -   Shard: A shard server. Currently, each shard is deployed as a three-node replica set. You can change the configuration of a shard, but cannot change the number of nodes in its replica set. A sharded cluster instance supports 2–32 shards.
    -   Config server: A required component of a sharded cluster instance. It is configured with a single-core CPU, 2 GB memory, and 20 GB storage space by default. Currently, you cannot change this configuration.

