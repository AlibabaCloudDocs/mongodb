# Scenarios

ApsaraDB for MongoDB supports replica set and sharded cluster deployment architectures and provides enterprise-class capabilities such as security audit and point-in-time backup. It has been widely used in Internet, IoT, games, and finance fields.

## Read/write splitting

ApsaraDB for MongoDB uses the architecture of three-node replica sets to guarantee high availability. Three data nodes are located on different physical servers and automatically synchronize data. The primary and secondary nodes are configured with different endpoints. MongoDB drivers allocate read/write requests to them. For more information, see [Architecture of ApsaraDB for MongoDB](/intl.en-US/Product Introduction/System architecture/Architecture of ApsaraDB for MongoDB.md).

## Flexible business scenarios

ApsaraDB for MongoDB has no schema and is suitable for startup business needs. You do not need to worry about changing schemas. You can store structured data in [ApsaraDB for Relational Database Service \(RDS\)](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md), flexible business data in ApsaraDB for MongoDB, and hot data in [ApsaraDB for Redis](/intl.en-US/Product Introduction/What is ApsaraDB for Redis?.md) or [ApsaraDB for Memcache](~~26530~~). This helps you write and read business data with high efficiency and reduce the cost of data storage.

## Apps

ApsaraDB for MongoDB supports two-dimensional spatial indexes, so it can provide support for location-based apps. Its dynamic storage mode is also suitable for storing heterogeneous data from multiple systems. This satisfies the requirements of apps.

## IoT scenarios

ApsaraDB for MongoDB features high performance and asynchronous data writing. It can achieve the processing capability of an in-memory database in specific scenarios. In a sharded cluster instance of ApsaraDB for MongoDB, you can adjust the configuration and quantity of mongos and shards to improve performance and expand storage space without limits. ApsaraDB for MongoDB is suitable for IoT scenarios with highly concurrent write operations. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

ApsaraDB for MongoDB provides a secondary index feature for dynamic queries. It can use the MapReduce aggregation framework of MongoDB to conduct multidimensional data analysis.

