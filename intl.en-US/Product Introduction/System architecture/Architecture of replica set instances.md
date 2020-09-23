---
keyword: [ApsaraDB for MongoDB sharded cluster instance,, build ApsaraDB for MongoDB replica set instance,, ApsaraDB for MongoDB replica set instance]
---

# Architecture of replica set instances

ApsaraDB for MongoDB automatically configures replica sets for instances so that you can manage the primary and secondary nodes. Advanced functions such as disaster recovery and failover are available after instances are created. When you use the instances, these functions are triggered without you knowing about it.

## Architecture

![Architecture of an ApsaraDB for MongoDB replica set instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3801129951/p39716.png)

ApsaraDB for MongoDB uses a multi-node architecture to ensure high availability. A replica set instance consists of a primary node that supports read/write operations, one or more secondary nodes, anda hidden node. The following section describes the nodes of a replica set:

-   Primary node: All read and write operations are performed on the primary node. Each replica set instance contains only one primary node.
-   Secondary node: The data of a secondary node is synchronized with the primary node by using oplogs. If the primary node fails, a secondary node can be elected as the new primary node to ensure high availability.

    **Note:** When you connect to an instance by using the endpoint of a secondary node, you can only read data from the instance but cannot write data to it.

-   Hidden node: The data of a hidden node is synchronized with the primary node by using oplogs. If a secondary node fails, the hidden node can be elected as the new secondary node to ensure high availability.

    **Note:** The hidden node is used only to ensure high availability and is not visible to users.


## Scale out nodes in a replica set instance

ApsaraDB for MongoDB allows you to scale out the number of nodes in an instance. You can increase the number of secondary nodes based on your business needs. For more information, see [Change the number of nodes for a replica set instance](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Change the number of nodes for a replica set instance.md).

For example, assume that you are running an informational website or an order query system that has more read operations than write operations. To improve the read performance, you can add secondary nodes. You can also add secondary nodes during business spikes and remove unnecessary nodes to save costs after the spikes.

**Related topics**  


[Architecture of standalone instances](/intl.en-US/Product Introduction/System architecture/Architecture of standalone instances.md)

[Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md)

