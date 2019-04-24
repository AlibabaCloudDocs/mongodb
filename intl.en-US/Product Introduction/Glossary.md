# Glossary {#concept_qjx_w3g_hfb .concept}

|Term|Description|
|:---|:----------|
|Region| -   The geographical location of the server for an ApsaraDB for MongoDB instance that you have purchased. You need to specify the region when purchasing the instance. For now, you cannot change the region after purchasing the instance.
-   ApsaraDB for MongoDB only supports intranet access. When purchasing an ApsaraDB for MongoDB instance, ensure that you have purchased an ECS instance in the same region. For more information about how to connect to an ApsaraDB for MongoDB instance through an intranet, see [Connect to an ApsaraDB for MongoDB instance through a cross-zone intranet](../../../../intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance through a cross-zone intranet.md#).

 |
|Zone| -   The physical area with its power supply and network isolated from other counterparts in the same region.
-   A zone is insulated from faults in other zones, and provides network connectivity to other zones in the same region through an intranet. The network latency within a zone is lower that across zones.
-   If an ApsaraDB for MongoDB replica set instance is a single-zone instance, all three nodes of the instance are located in the same zone. If a pair of ApsaraDB for MongoDB and ECS instances are deployed in the same zone, the network latency can be lower.

 |
|Instance| -   The ApsaraDB for MongoDB instance, which is the basic unit of the ApsaraDB for MongoDB service that you can purchase.
-   The instance is the operating environment for ApsaraDB for MongoDB and exists as a separate process on the host.
-   Users can use the console to create, modify, and delete MongoDB instances. Instances are mutually independent and configured with isolated resources. They do not need to compete for CPU, memory, and I/O resources.
-   Each instance has its own characteristics such as the database type and version. ApsaraDB for MongoDB provides parameters to control the behavior of each instance.

 |
|Memory|The maximum memory that can be used by an ApsaraDB for MongoDB instance.|
|Disk capacity| -   Disk capacity is the size of the disk which the user selects when purchasing the MongoDB instance.
-   The disk capacity occupied by the instance includes set data and the space required for normal instance operation, such as the system database, database rollback log, redo log, and indexing.
-   You need to ensure that an ApsaraDB for MongoDB instance has sufficient disk capacity to store data, otherwise the instance may be locked. If an instance is locked due to insufficient disk capacity, you can purchase more disk capacity to unlock the instance.

 |
|IOPS|The maximum number of read and write operations performed by a block device per second, measured in units of 4 KB.|
|CPU core| This is the instance's maximum computing power.

 A CPU core has the minimum computing power at 2.3 GHz \(equivalent to an Intel Xeon processor which adopts Hyper-Threading technology\).

 |
|Connections| TCP connections between clients and the MongoDB instances.

 If a client uses a connection pool, the client establishes persistent connections with ApsaraDB for MongoDB instances. Otherwise, it establishes transient connections.

 |
|ApsaraDB for MongoDB cluster|The cluster version of ApsaraDB for MongoDB. You can purchase multiple mongos nodes, multiple shards, and a config server to create an ApsaraDB for MongoDB cluster conveniently, which serves as a MongoDB distributed database system.|
|Mongos| -   The entry to an ApsaraDB for MongoDB cluster for requests. Mongos nodes act as a request distribution center to coordinate all requests. They are responsible for forwarding data requests to the corresponding shards.
-   You can configure multiple mongos nodes as the entry for requests. In this case, if a mongos node is faulty, others can still process requests.

 |
|Shard| -   Shards are the parts of MongoDB clusters.
-   Each shard is deployed as a three-node replica set to guarantee its high availability. Based on your application performance and storage requirements, you can purchase multiple shards to scale out the read and write performance and storage space of ApsaraDB for MongoDB and deploy a distributed database system.

 |
|Config server| -   The configuration server that stores all database metadata for mongos nodes and shards in an ApsaraDB for MongoDB cluster. A mongos node does not store data, but caches the shard data and data routing information in its memory. The config server actually stores such data.
-   When a mongos node is started for the first time or is shut down and then restarted, it loads configuration information from the config server. If the configuration information changes, the config server notifies all mongos nodes, so that they can update their status to correctly route data.
-   The config server stores the metadata of mongos nodes and shards. Considering high requirements for service availability and data reliability, ApsaraDB for MongoDB deploys the config server as a three-node replica set to comprehensively ensure its service reliability.

 |

