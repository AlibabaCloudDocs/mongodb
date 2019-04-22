# Scenarios {#concept_znp_tgc_bfb .concept}

## Read/Write splitting {#section_nrj_1hc_bfb .section}

ApsaraDB for MongoDB uses the architecture of a three-node replica set to guarantee high availability. Three data nodes are located on different physical servers and automatically synchronize data. The primary node and operable secondary node, each of which is configured with a separate domain name, provide services and help MongoDB drivers relieve the pressure of read operations.

## Flexible services {#section_gjr_shc_bfb .section}

With no schema, ApsaraDB for MongoDB is suitable for start-ups. You do not need to worry about changing the table structure. You can store structured data in ApsaraDB for RDS, business data that has flexible structure in ApsaraDB for MongoDB, and hot data in ApsaraDB for Memcache or ApsaraDB for Redis. This helps you efficiently store and obtain business data and reduce the cost of data storage.

## Mobile applications {#section_v5t_xhc_bfb .section}

ApsaraDB for MongoDB supports two-dimensional spatial indexes, so it can provide great support for location-based mobile applications. At the same time, the dynamic storage mode of ApsaraDB for MongoDB is suitable for storing heterogeneous data from multiple systems, thereby satisfying the requirements of mobile applications.

## IoT applications {#section_urm_23c_bfb .section}

ApsaraDB for MongoDB features high performance and asynchronous data write operations. It can achieve the processing capability of an in-memory database in specific scenarios. Using a sharded cluster instance of ApsaraDB for MongoDB, you can dynamically scale out the configuration of mongos nodes and shards and increase the number of mongos nodes and shards to scale out the performance and storage space of ApsaraDB for MongoDB without limits. In this case, ApsaraDB for MongoDB is suitable for IoT scenarios that require highly-concurrent write operations.

ApsaraDB for MongoDB provides a secondary index feature to meet the requirements for dynamic queries. It can use the MapReduce aggregation framework of MongoDB to conduct multidimensional data analysis.

