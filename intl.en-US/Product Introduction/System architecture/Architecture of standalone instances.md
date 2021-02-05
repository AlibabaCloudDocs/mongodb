---
keyword: [ApsaraDB, Alibaba Cloud database, ApsaraDB for MongoDB, standalone]
---

# Architecture of standalone instances

Standalone instances of ApsaraDB for MongoDB are developed for scenarios with high fault tolerance and apply to the storage of non-core data. This architecture is highly cost-effective and is ideal for environment testing, learning and training, and internal enterprise business.

It enables you to purchase ApsaraDB for MongoDB at a lower entry-level price to enjoy superiority in O&M support and kernel-level optimization. The standalone architecture can adapt ApsaraDB for MongoDB to various scenarios to help enterprises minimize their costs and expenses.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2801129951/p915.png)

## FAQ

Does the architecture of standalone instances provide high availability?

The architecture of standalone instances has only one replica, which cannot provide high availability. A failure can cause service unavailability for more than 30 minutes in extreme cases. We recommend that you use the architecture of the replica set in production environments.

**Related topics**  


[Architecture of replica set instances](/intl.en-US/Product Introduction/System architecture/Architecture of replica set instances.md)

[Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md)

