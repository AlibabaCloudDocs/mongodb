---
keyword: [ApsaraDB, Alibaba Cloud database, ApsaraDB for MongoDB, standalone]
---

# Architecture of standalone instances

ApsaraDB for MongoDB standalone instances are developed for scenarios that require high fault tolerance and are suitable for the storage of non-core data. The standalone architecture is highly cost-effective and is ideal for environment testing, learning and training, and internal enterprise business.

You can purchase standalone instances at a lower price and enjoy the superior O&M support and engine optimization that is provided by ApsaraDB for MongoDB. The standalone architecture can adapt ApsaraDB for MongoDB to various scenarios to help enterprises minimize their costs and expenses.

Standalone instances support only MongoDB 3.4. When you create a standalone instance, select MongoDB 3.4.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2801129951/p915.png)

## FAQ

Does the architecture of standalone instances provide high availability?

The architecture of standalone instances has only a single replica, which cannot provide high availability. A failure can cause service unavailability for more than 30 minutes in extreme cases. We recommend that you use the replica set architecture in production environments.

**Related topics**  


[Architecture of replica set instances](/intl.en-US/Product Introduction/System architecture/Architecture of replica set instances.md)

[Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md)

