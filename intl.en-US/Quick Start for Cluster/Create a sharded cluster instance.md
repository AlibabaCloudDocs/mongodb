# Create a sharded cluster instance {#task_g3q_hyq_w2b .task}

You can use the ApsaraDB for MongoDB console to create a MongoDB sharded cluster instance. For more information about billing methods of MongoDB sharded cluster instances, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#). This topic describes how to create an instance in the ApsaraDB for MongoDB console.

-   You have registered an Alibaba Cloud account. For more information about the registration process, see [Register an Alibaba Cloud account](https://www.alibabacloud.com/help/zh/doc-detail/50482.htm).
-   If you want to create a Pay-As-You-Go instance, make sure that your Alibaba Cloud account has sufficient balance.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the left-side navigation pane, click **Sharding instances**.
3.  On the **Sharding instances** page, click **Create Instance**.
4.  Select **Subscription \(Sharding\)** or **Pay-As-You-Go \(Sharding\)**. 

    **Note:** For more information about billing methods, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#).

5.  Configure the parameters of the instance. 

    For more information about the parameters, see [Table 1](#table_i5n_4cr_w2b).

    |Area|Parameter|Description|
    |:---|:--------|:----------|
    |**Basic Configuration**|**Region**| The region to which the instance belongs. After the instance is created, you cannot modify its region. Use caution when selecting the region.

 Instances in the same region \(such as an [ECS](https://www.alibabacloud.com/help/zh/doc-detail/25367.htm) instance and a MongoDB instance\) are able to access to each other over the internal network.

 |
    |**Zone**| The physical zones within a region that each have an independent power supply and separate network.

 For more information about regions and zones, see [Regions and zones](https://www.alibabacloud.com/help/zh/doc-detail/40654.htm).

 An ECS instance and a MongoDB instance that reside in different zones within the same region can still access each other over the internal network. For more information, see [Connect to a MongoDB instance in a different zone over the internal network](../../../../intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance through a cross-zone intranet.md#).

 ECS instances and MongoDB instances that reside in the same zone are able to access each other with minimal network latency.

 |
    |**Database Version**| MongoDB sharded cluster instances support database versions 3.2, 3.4, and 4.0

 We recommend that you select MongoDB 3.2 or later. Compared with MongoDB 3.2, MongoDB 3.4 provides higher performance and security. For more information, see [Database versions and storage engines](../../../../intl.en-US/Product Introduction/Versions and storage engines.md#).

 **Note:** You can manually upgrade the database version to 3.4 or 4.0 when the instance is running. However, databases cannot be downgraded to previous versions. For more information, see [Upgrade database versions](../../../../intl.en-US/User Guide/Instance management/Upgrade the database version.md#).

 |
    |**Storage Engine**| MongoDB sharded cluster instances support WiredTiger.

 For more information about the relationship between database versions and storage engines, see [Database versions and storage engines](../../../../intl.en-US/Product Introduction/Versions and storage engines.md#).

 |
    |**Network Type**|**Classic Network**|Cloud services in a classic network are not isolated. You can configure security groups or whitelist policies to block unauthorized access to classic network cloud services.|
    |**VPC**|Virtual Private Cloud \(VPC\) is an isolated network environment with higher security and performance than the classic network. You need to create VPCs in advance. For more information, see [Configure VPC for a new instance](../../../../intl.en-US/User Guide/Network connection management/Configure a VPC for a new instance.md#). **Note:** 

    -   You can also modify the network type after creating an instance. For more information, see [Modify the instance network type](../../../../intl.en-US/User Guide/Network connection management/Switch the network type of an instance.md#).
    -   To smoothly migrate applications onto the cloud, you can use a leased line or VPN to integrate your own data center with resources on the cloud to make a virtual data center. For more information about the solution, see [Migrate data from the classic network to VPC](../../../../intl.en-US/User Guide/Network connection management/Configure a hybrid access solution to smoothly switch from a classic network to a VPC.md#).
 |
    |**Mongos Specifications**|**Mongos Type**| The specifications of mongos in sharded cluster instances. For more information about mongos specifications, see [Instance types](../../../../intl.en-US/Product Introduction/Instance specifications.md#).

 When the instance is running, you can add mongos and upgrade or downgrade their configurations.

 After you modify instance specifications, your charges may change. For more information, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#).

 |
    |**Quantity**| The number of mongos.

 A MongoDB sharded cluster instance can contain 2 to 32 mongos.

 |
    |**Shard Specifications**|**Shard Type**| The specifications of the shard in the instance. For more information about the shard specifications, see [Instance types](../../../../intl.en-US/Product Introduction/Instance specifications.md#).

 When the instance is running, you can add shards and upgraded or downgraded their configurations.

 After you modify instance configurations, your charges may change. For more information, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#).

 |
    |**Storage Capacity**| The storage space of the shard in the instance. A shard can provide a storage space of 10 to 1,000 GB.

 The storage space of a shard includes the space for data files, system files, and log files.

 |
    |**Quantity**| The number of shards.

 A MongoDB sharded cluster instance can contain 2 to 32 shards.

 |
    |**Configserver Specifications**|**Configserver Type**| The config server specifications are fixed at 1 core 2 GB CPU and memory with 20 GB of storage space. These specifications cannot be modified.

 |
    |**Set Password**|-| The account password used to connect to the MongoDB database for the first time.

     -   It must contain three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include !@\#$%^&\*\(\)\_+-=
    -   The password must be 8 to 32 characters in length.
 You can specify a password when creating an instance, or specify a password or reset it when the instance is running.

 |

6.  After you configure the parameters, click **Buy Now**.
7.  On the Confirm Order page, select ApsaraDB for MongoDB Agreement of Service and complete the payment process as prompted.

