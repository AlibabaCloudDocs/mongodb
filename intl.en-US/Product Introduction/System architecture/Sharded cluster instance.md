# Sharded cluster instance {#concept_rcj_dc4_tdb .concept}

A sharded cluster instance is created based on multiple three-node replica sets. Each sharded cluster instance consists of three components: mongos, shard, and config server. You can specify the number and configuration of mongos nodes and shards as required to create ApsaraDB for MongoDB clusters that provide different service capabilities.

 ![](images/917_en-US.png) 

-   **Mongos**: A service agent configured with only one node. You can purchase multiple mongos nodes to achieve load balancing and failover. A sharded cluster instance supports 2–32 mongos nodes.
-   **Shard**: A shard server. Currently, each shard is deployed as a three-node replica set. You can change the configuration of a shard, but cannot change the number of nodes in its replica set. A sharded cluster instance supports 2–32 shards.

    You can add mongos nodes and shards based on business requirements. However, you cannot run native commands to add them, but need to purchase new mongos nodes and shards from the ApsaraDB for MongoDB console.

-   **Config server**: A required component of a sharded cluster instance. It is configured with a single-core CPU, 2 GB memory, and 20 GB storage space by default. Currently, you cannot change this configuration.
-   Because shards and config servers do not support domain name access, you cannot directly connect to shards and config servers. To perform data operations on shards and config servers, you need to connect to mongos nodes to deliver instructions.

**Note:** ApsaraDB for MongoDB does not allow you to upgrade an existing standalone instance or three-node replica set instance to a sharded cluster instance. If you need to use a sharded cluster instance, you must purchase one.

