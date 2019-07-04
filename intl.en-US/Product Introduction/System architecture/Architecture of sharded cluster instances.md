# Architecture of sharded cluster instances {#concept_rcj_dc4_tdb .concept}

A sharded cluster instance comprises three components: mongos, shard and ConfigServer. You can choose the configuration and number of mongos and shards to create ApsaraDB for MongoDB sharded cluster instances that have different performance.

## Architecture of sharded cluster instances {#section_agk_qtt_xgb .section}

![Architecture of an ApsaraDB for MongoDB sharded cluster instance](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6646/156222406739656_en-US.png)

## Components {#section_hhp_stt_xgb .section}

-   Mongos

    A mongos is a router server that routes queries and writes to the corresponding shards of sharded cluster instances. A mongos uses a standalone structure. You can purchase multiple mongos in the console to achieve load balancing and failover. A single sharded cluster instance supports 2 to 32 mongos.

-   Shard

    A shard \(sharding server\) stores data in a database. A shard uses a three-node replica set structure. You can scale simultaneous operations of data storage, reading and writing horizontally by purchasing several shards in the console. A single sharded cluster instance supports 2 to 32 shards.

    **Note:** Each shard is a fixed three-node replica set structure. You cannot modify the number of nodes.

-   ConfigServer

    A ConfigServer is a configuration server that is used to store metadata for clusters and shards. Metadata indicates data about what each shard contains. A ConfigServer uses a fixed three-node replica set structure. Its default specification is 1 core, 2 GB memory, and 20 GB disk storage space.

    **Note:** Specifications set for ConfigServer cannot be modified.


Neither the shard nor ConfigServer has an access address. You cannot connect to the shard or ConfigServer directly. All data operations must connect to a mongos for distribution though this node.

