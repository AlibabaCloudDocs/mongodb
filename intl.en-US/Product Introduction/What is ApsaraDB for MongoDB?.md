---
keyword: [ApsaraDB,, ApsaraDB for MongoDB]
---

# What is ApsaraDB for MongoDB?

ApsaraDB for MongoDB is developed based on the distributed system and high-reliability storage engine of Apsara, and is compatible with the MongoDB protocol. ApsaraDB for MongoDB uses a multi-node architecture to ensure high availability and supports elastic scaling, disaster recovery, backup and restoration, and performance optimization.

## Why ApsaraDB for MongoDB?

For more information about the benefits of ApsaraDB for MongoDB, see [Comparison between ApsaraDB for MongoDB and user-created databases](/intl.en-US/Product Introduction/Comparison between ApsaraDB for MongoDB and user-created databases.md) and [Scenarios](/intl.en-US/Product Introduction/Scenarios.md).

## Supported architectures

ApsaraDB for MongoDB supports multiple deployment architectures to meet the requirements of different business scenarios.

|Architecture|Description|
|:-----------|:----------|
|[Architecture of standalone instances](/intl.en-US/Product Introduction/System architecture/Architecture of standalone instances.md)|You can use a standalone instance to perform development and testing or store enterprise data that is not critical. You can purchase a standalone instance at a lower price and enjoy the superior O&M support and kernel-level optimization that is provided by ApsaraDB for MongoDB. For more information about how to create a standalone instance, see [Create a standalone instance](/intl.en-US/Quick Start for Standalone/Create a standalone instance.md).|
|[Architecture of replica set instances](/intl.en-US/Product Introduction/System architecture/Architecture of replica set instances.md)|A replica set instance consists of a primary node that supports read/write operations, one or more high-availability secondary nodes, anda hidden node. For more information about the nodes and their differences, see [Architecture of replica set instances](/intl.en-US/Product Introduction/System architecture/Architecture of replica set instances.md). For more information about how to create a replica set instance, see [Create a replica set instance](/intl.en-US/Quick Start for Replica Set/Create a replica set instance.md).

 You can add or remove secondary nodes based on your business needs. For example, assume that you are running an informational website or an order query system that has more read operations than write operations. To improve the read performance, you can add secondary nodes. You can also add secondary nodes during business spikes and remove unnecessary nodes to save costs after the spikes. For more information, see [Change the number of nodes for a replica set instance](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Change the number of nodes for a replica set instance.md). |
|[Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md)|A sharded cluster instance is created based on multiple three-node replica sets. A sharded cluster instance consists of three components, which are mongos, shard, and config server. You can specify the number and configurations of mongos and shard nodes to create ApsaraDB for MongoDB clusters that have different service capabilities. For more information about how to create a sharded cluster instance, see [Create a sharded cluster instance](/intl.en-US/Quick Start for Cluster/Create a sharded cluster instance.md). For more information about different components, see [Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md).|

## Pricing

For more information, see [Billing items and pricing](/intl.en-US/Purchase Guide/Billing items and pricing.md).

## Deployment suggestions

Consider the following aspects when you create and use an ApsaraDB for MongoDB instance:

-   Region and zone

    A region is an Alibaba Cloud data center. A zone is a physical area with independent power grids and networks in a region. The region and zone determine the physical location of an ApsaraDB for MongoDB instance. You cannot change the region of an ApsaraDB for MongoDB instance after the instance is created. For more information, see [Regions and zones](~~40654~~).

    Select a region and zone based on the geographical location, availability of Alibaba Cloud services, application availability requirements, and whether internal network communication is required. For example, if your application is deployed on an [Elastic Compute Service](~~25367~~) \(ECS\) instance and requires an ApsaraDB for MongoDB instance to function as its database, you must select the same region and zone as the ECS instance when you create your ApsaraDB for MongoDB instance.

    **Note:** An ECS instance and an ApsaraDB for MongoDB instance in the same zone can be interconnected by using the internal network with minimal network latency.

-   Network planning

    We recommend that you use [Virtual Private Cloud](~~34217~~) \(VPC\) to connect to ApsaraDB for MongoDB instances. You can plan your own Classless Inter-Domain Routing \(CIDR\) blocks for VPCs. A VPC is an isolated network with higher security and performance than the classic network. You can use the default VPC or create your own VPC before you use ApsaraDB for MongoDB. For more information, see [Configure a VPC for a new instance](/intl.en-US/User Guide/Network connection management/Configure a VPC for a new instance.md).

-   Security solutions

    ApsaraDB for MongoDB eliminates your data security concerns by providing comprehensive security protection. You can ensure database security by using zone-disaster recovery, Resource Access Management \(RAM\) authorization, audit logs, network isolation, whitelists, password authentication, and Transparent Data Encryption \(TDE\). For more information, see [Best practices for data security of ApsaraDB for MongoDB](/intl.en-US/Best Practices/Best practices for data security of ApsaraDB for MongoDB.md).


## Manage ApsaraDB for MongoDB instances

You can use the following methods to manage ApsaraDB for MongoDB instances, such as creating instances, databases, and accounts, and specifying network-related settings:

-   [Console](https://mongodb.console.aliyun.com/): The ApsaraDB for MongoDB console provides a graphical and easy-to-use web interface.
-   [API](/intl.en-US/API Reference/List of API operations by function.md): All operations that are available in the console can be performed by calling API operations.

After you create an ApsaraDB for MongoDB instance, you can connect to the instance by using one of the following methods:

-   Mongo shell: You can log on to the instance by using the official MongoDB CLI tool to manage databases. For more information, see [Connect to a replica set instance by using the mongo shell](/intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to a replica set instance by using the mongo shell.md).
-   Client: ApsaraDB for MongoDB is compatible with the MongoDB protocol. You can use common database client tools, such as Robo 3T and Studio 3T to connect to ApsaraDB for MongoDB instances.

## Related services

-   [ECS](~~25367~~): The best performance is achieved when you connect to ApsaraDB for MongoDB instances from ECS in the same region over an internal network. ECS and ApsaraDB for MongoDB instances compose a typical business architecture.
-   [Data Transmission Service \(DTS\)](~~26592~~): You can use DTS to migrate data from an on-premises MongoDB database to the cloud.
-   [Object Storage Service \(OSS\)](~~31817~~): OSS is a secure, cost-effective, and reliable cloud storage service that is provided by Alibaba Cloud. OSS allows you to store a large amount of data in the cloud.
