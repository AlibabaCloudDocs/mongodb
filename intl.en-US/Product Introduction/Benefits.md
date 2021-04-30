# Benefits

ApsaraDB for MongoDB is a MongoDB-compatible database service that is developed based on the distributed Apsara system and high-reliability storage engine. ApsaraDB for MongoDB uses a multi-node architecture to ensure high availability, and supports elastic scaling, disaster recovery, backup and restoration, and performance optimization.

## Multiple deployment architectures

ApsaraDB for MongoDB supports multiple deployment architectures to meet the requirements of different business scenarios.

Deployment architectures of ApsaraDB for MongoDB:

-   Architecture of standalone instances

    Standalone instances apply to development, testing, education, and scenarios where non-core enterprise data is stored. You can select the instance specifications that are most suitable for your business scenarios to minimize costs. For more information, see [Architecture of standalone instances](/intl.en-US/Product Introduction/System architecture/Architecture of standalone instances.md).

-   Architecture of replica set instances

    Replica set instances are applicable to burst traffic scenarios that require more reads than writes or temporary activities. A replica set instance consists of a primary node that supports read and write operations, one, three, or five high-availability secondary nodes, and a hidden node, as well as up to five optional read-only nodes. You can add or remove secondary nodes and read-only nodes based on your business needs. For more information, see [Architecture of replica set instances](/intl.en-US/Product Introduction/System architecture/Architecture of replica set instances.md).

-   Architecture of sharded cluster instances

    Sharded cluster instances are suitable for scenarios that require highly concurrent read and write operations. A sharded cluster instance is based on multiple three-node replica set instances. Each replica set instance contains three nodes in primary/secondary mode and up to five optional read-only nodes. A sharded cluster instance consists of three components: mongos, shard, and Configserver nodes. You can specify the number and specifications of mongos and shard nodes to create sharded cluster instances that have different service capabilities. For more information, see [Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md).


## Elastic scaling

ApsaraDB for MongoDB allows you to change instance configurations to adapt to shifting business needs. You can change the configurations of an instance \(instance specifications, storage capacity, and number of nodes\) based on your business needs. You can also specify that the new configurations take effects during off-peak hours to avoid possible impacts on your business. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Compatibility with DynamoDB

ApsaraDB for MongoDB is fully compatible with the MongoDB protocol. Sharded cluster instances of MongoDB 4.0 are highly compatible with the DynamoDB protocol. You can directly create DynamoDB-compatible sharded cluster instances in the console. For more information, see [t1887092.md\#]().

## Support for Alibaba Cloud developed tools

ApsaraDB for MongoDB allows you to migrate and synchronize data in the console or by using native MongoDB tools. In addition, you can use the following Alibaba Cloud developed tools.

|Tool|Description|
|----|-----------|
|NimoShake|A data synchronization tool. You can use this tool to migrate Amazon DynamoDB databases to Alibaba Cloud. For more information, see [Migrate an Amazon DynamoDB database to ApsaraDB for MongoDB by using NimoShake](/intl.en-US/User Guide/Data migration and synchronization/Migrate data from a third-party cloud service provider to Alibaba Cloud/Migrate an Amazon DynamoDB database to ApsaraDB for MongoDB by using NimoShake.md).|
|MongoShake|A general tool developed in the Go language to synchronize data. You can use this tool to synchronize data between MongoDB databases. For more information, see [Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica set instances](/intl.en-US/User Guide/Data migration and synchronization/Data synchronization/Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica set instances.md).|
|NimoFullCheck|A tool used to verify the data consistency between source DynamoDB and destination MongoDB databases. You can use this tool to check data consistency when you migrate data in a DynamoDB database to an ApsaraDB for MongoDB instance. For more information, see [Use NimoFullCheck to check data consistency after migration](/intl.en-US/User Guide/Data migration and synchronization/Migrate data from a third-party cloud service provider to Alibaba Cloud/Use NimoFullCheck to check data consistency after migration.md).|

## MongoDB engine supported in ApsaraDB for MyBase

You can purchase ApsaraDB for MongoDB instances in the ApsaraDB for MyBase console because ApsaraDB for MyBase already supports the MongoDB engine. For more information, see [What is ApsaraDB for MyBase?]() and [Create a MyBase for MongoDB instance]().

## Latest MongoDB version

Alibaba Cloud and MongoDB have started strategic cooperation and jointly developed the latest MongoDB 4.4 to solve the problems of previous MongoDB versions.

MongoDB 4.4 mainly solves the following problems:

-   Write performance degradation when a large number of indexes are maintained in databases.
-   Jumbo chunks \(beyond the specified chunk size\) or query hotspots on a single shard due to changes in workload.
-   Uneven distribution of data across shards because hash indexes are not supported.
-   Long page response time.
-   Latency in primary/secondary replication.
-   Asynchronous creation of indexes on the primary and secondary databases.

For more information about MongoDB 4.4, see [Features of ApsaraDB for MongoDB V4.4]().

## Others

ApsaraDB for MongoDB also excels in service availability, data reliability, security, and O&M costs. For more information, see [Comparison between ApsaraDB for MongoDB and self-managed databases](/intl.en-US/Product Introduction/Comparison between ApsaraDB for MongoDB and self-managed databases.md).

