# Terms

This topic describes the terms that are used in ApsaraDB for MongoDB.

|Term|Description|
|:---|:----------|
|region|-   The geographical location of the server for the ApsaraDB for MongoDB instance that you create. You must specify a region when you create an ApsaraDB for MongoDB instance. The region cannot be changed after the instance is created.
-   When you create an ApsaraDB for MongoDB instance, you must use an Elastic Compute Service \(ECS\) instance. ApsaraDB for MongoDB supports access over the internal network. The specified region must be the same as that of the ECS instance. For more information, see [Connect to an ApsaraDB for MongoDB instance over the internal network across zones](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance over the internal network across zones.md). |
|zone|-   A physical area with an independent power supply and network in a region.
-   Resources in zones that are in the same region can communicate with each other over the internal network. The network latency within a zone is lower that across zones. Faults are isolated between zones.
-   In the single-zone deployment mode, the three nodes of an ApsaraDB for MongoDB replica set instance are deployed in the same zone. If an ECS instance and an ApsaraDB for MongoDB instance are both deployed in the same zone, network latency is reduced. |
|instance|-   An ApsaraDB for MongoDB instance, which is the basic unit of ApsaraDB for MongoDB.
-   An instance is the runtime environment for ApsaraDB for MongoDB and exists as a separate process on a host.
-   You can create, modify, and delete an instance by using the ApsaraDB for MongoDB console. Instances are independent and their resources are isolated. They do not compete for resources such as CPU, memory, and I/O.
-   Each instance has its own unique features, such as database engine and version. ApsaraDB for MongoDB controls instance behavior by using the parameters that correspond to the features. |
|memory|The maximum memory that an instance can use.|
|disk capacity|-   The disk size that you select when you create an ApsaraDB for MongoDB instance.
-   The disk capacity occupied by the instance includes datasets and the space required for normal instance operations, such as the system database, database rollback log, redo log, and indexes.
-   Make sure that an ApsaraDB for MongoDB instance has sufficient disk capacity to store data. Otherwise, the instance may be locked. If the instance is locked due to insufficient disk capacity, you can unlock the instance by expanding the disk capacity. |
|IOPS|The maximum number of read/write operations performed per second on block devices at a granularity of 4 KB.|
|CPU core|The maximum computing power of an ApsaraDB for MongoDB instance.

A single Intel Xeon series CPU core has at least 2.3 GHz of computing power with hyper-threading capabilities. |
|connections|The number of Transmission Control Protocol \(TCP\) connections between a client and an ApsaraDB for MongoDB instance.

If the client uses a connection pool, the connections between the client and the instance are persistent connections. Otherwise, they are short-lived connections. |
|sharded cluster instance|An ApsaraDB for MongoDB sharded cluster instance. You can purchase multiple mongos nodes, multiple shard nodes, and a Configserver node to create an ApsaraDB for MongoDB sharded cluster instance, which serves as a MongoDB distributed database system.|
|mongos|-   The routing service that processes requests. All requests must be coordinated by using mongos that serves as a request distribution center and forwards data requests to the corresponding shard server.
-   You can use multiple mongos nodes to process requests. If one mongos node fails, other mongos nodes can continue to process the requests. |
|shard|-   An ApsaraDB for MongoDB instance that holds a subset of the sharded data.
-   Each shard can be deployed as a three-node replica set to increase availability. You can create multiple shards to improve read and write performance and expand storage capacity. This way, you can implement a distributed database system based on your application performance and storage requirements. |
|Configserver|-   A configuration server that stores all database metadata for mongos nodes and shards in an ApsaraDB for MongoDB sharded cluster instance. Mongos nodes cache shard data and data routing information in their memory, whereas Configservers store such data.
-   When mongos nodes in a sharded cluster instance are started for the first time or shut down and then restarted, they load configuration information from the Configserver node. If the information of the Configserver node changes, all mongos nodes are notified to update their status. This ensures that mongos nodes can always obtain the correct routing information.
-   Configserver nodes store metadata of shards and routers and have high requirements for service availability and data reliability. ApsaraDB for MongoDB uses three-node replica sets to ensure the reliability of the Configserver nodes. |

