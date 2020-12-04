---
keyword: [ApsaraDB for MongoDB, ApsaraDB for MongoDB instance]
---

# Instance types

This topic describes the instance types available in ApsaraDB for MongoDB.

## IOPS

The IOPS of the local SSD is fixed to the instance type. The IOPS of the enhanced SSD is proportional to the storage capacity. The ECS instance type also limits the maximum IOPS. For more information, see the lists in this topic.

The IOPS of the enhanced SSD:

```
min {1,800 + 50 × Storage capacity, 50,000, ECS-limited IOPS}
```

The values in the preceding formula:

-   `1,800 + 50 × Storage capacity`: the basic calculation formula for the IOPS of the enhanced SSD.
-   `50,000`: the maximum IOPS of a single PL1 enhanced SSD. For more information, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md).
-   `ECS-limited IOPS`: the maximum IOPS of the ECS instance type. For more information about ECS-limited IOPS of each instance type, see the list in this topic.

The actual IOPS of an instance is the minimum of the three values. Example:

-   The storage capacity of an instance is 20 GB. The result of 1,800 + 50 × 20 is 2,800. Then the actual IOPS of the instance is 2,800.
-   If the instance type is `mdb.shard.2x.xlarge.d`, the ECS-limited IOPS is 21,000. If the storage space of the instance is 6,000 GB, the calculated value is 301,800, which exceeds the maximum IOPS of a single PL1 enhanced SSD and the ECS-limited IOPS. Then the actual IOPS of the instance is 21,000.

**Note:** If the throughput of an instance reaches the upper limit, the IOPS of the instance also decreases. For more information, see [Storage I/O performance of the new generation of enterprise-level instance families](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

## Current instance types

The following instance types are available for instances that were created on and after July 10, 2017 or whose configurations have been changed.

|Architecture|Category|Specification|Instance type|Maximum connections|Maximum IOPS|Storage capacity|
|:-----------|:-------|:------------|:------------|:------------------|:-----------|:---------------|
|Replica set instance|General purpose|1 vCPU, 2 GiB memory|dds.mongo.mid|500|8,000|10 to 2,000 GB|
|2 vCPUs, 4 GiB memory|dds.mongo.standard|1,000|8,000|
|4 vCPUs, 8 GiB memory|dds.mongo.large|3,000|8,000|
|8 vCPUs, 16 GiB memory|dds.mongo.xlarge|5,000|8,,000|
|8 vCPUs, 32 GiB memory|dds.mongo.2xlarge|8,000|14,000|
|16 vCPUs, 64 GiB memory|dds.mongo.4xlarge|16,000|16,000|
|Dedicated CPU|2 vCPUs, 16 GiB memory|mongo.x8.medium|2,500|4,500|250 GB|
|4 vCPUs, 32 GiB memory|mongo.x8.large|5,,000|9,000|500 GB|
|8 vCPUs, 64 GiB memory|mongo.x8.xlarge|10,000|18,000|1,000 GB|
|16 vCPUs, 128 GiB memory|mongo.x8.2xlarge|20,000|36,000|-   Subscription: 2,000 to 3,000 GB
-   Pay-as-you-go: 2,000 GB |
|32 vCPUs, 256 GiB memory|mongo.x8.4xlarge|40,000|72,000|2,000 to 3,000 GB|
|Dedicated host|60 vCPUs, 440 GiB memory|dds.mongo.2xmonopolize|100,000|100,000|2,000 to 6,000 GB|
|Standalone instance|General purpose|1 vCPU, 2 GiB memory|dds.n2.small.1|2,000|min \{30 × Storage capacity, 20,000\}|20 to 2,000 GB|
|2 vCPUs, 4 GiB memory|dds.sn2.medium.1|4,000|
|2 vCPUs, 8 GiB memory|dds.sn4.large.1|6,000|
|4 vCPUs, 8 GiB memory|dds.sn2.large.1|6,000|
|4 vCPUs, 16 GiB memory|dds.sn4.xlarge.1|8,000|
|8 vCPUs, 16 GiB memory|dds.sn2.xlarge.1|8,000|

|Node type|Category|Specification|Instance type|Maximum connections|Maximum IOPS|Storage capacity|
|:--------|:-------|:------------|:------------|:------------------|:-----------|----------------|
|Mongos|General purpose|1 vCPU, 2 GiB memory|dds.mongos.mid|1,000|N/A|N/A|
|2 vCPUs, 4 GiB memory|dds.mongos.standard|2,000|
|4 vCPUs, 8 GiB memory|dds.mongos.large|4,000|
|8 vCPUs, 16 GiB memory|dds.mongos.xlarge|8,000|
|8 vCPUs, 32 GiB memory|dds.mongos.2xlarge|16,000|
|16 vCPUs, 64 GiB memory|dds.mongos.4xlarge|16,000|
|Shard|General purpose|1 vCPU, 2 GiB memory|dds.shard.mid|N/A|1,000|10 to 2,000 GB|
|2 vCPUs, 4 GiB memory|dds.shard.standard|2,000|
|4 vCPUs, 8 GiB memory|dds.shard.large|4,000|
|8 vCPUs, 16 GiB memory|dds.shard.xlarge|8,000|
|8 vCPUs, 32 GiB memory|dds.shard.2xlarge|14,000|
|16 vCPUs, 64 GiB memory|dds.shard.4xlarge|16,000|
|Dedicated CPU|2 vCPUs, 16 GiB memory|dds.shard.sn8.xlarge.3|4,500|10 to 250 GB|
|4 vCPUs, 32 GiB memory|dds.shard.sn8.2xlarge.3|9,000|10 to 500 GB|
|8 vCPUs, 64 GiB memory|dds.shard.sn8.4xlarge.3|18,000|10 to 1,000 GB|
|16 vCPUs, 128 GiB memory|dds.shard.sn8.8xlarge.3|36,000|10 to 2,000 GB|
|32 vCPUs, 256 GiB memory|dds.shard.sn8.16xlarge.3|72,000|10 to 3,000 GB|
|Configserver|General purpose|1 vCPU, 2 GiB memory|dds.cs.mid|1,000|20 GB|

## Historical instance types

The following instance types are available for instances that were created before July 10, 2017 and whose configurations have not been changed.

|Category|Specification|Instance type|Maximum connections|Maximum IOPS|
|:-------|:------------|:------------|:------------------|:-----------|
|General purpose|1 vCPU, 2 GiB memory|dds.mongo.mid|200|800|
|2 vCPUs, 4 GiB memory|dds.mongo.standard|400|1,600|
|4 vCPUs, 8 GiB memory|dds.mongo.large|1,000|3,200|
|8 vCPUs, 16 GiB memory|dds.mongo.xlarge|2,000|6,400|
|8 vCPUs, 32 GiB memory|dds.mongo.2xlarge|4,000|12,800|
|16 vCPUs, 64 GiB memory|dds.mongo.4xlarge|8,000|12,800|
|Dedicated CPU|2 vCPUs, 16 GiB memory|mongo.x8.medium|2,000|4,500|
|4 vCPUs, 32 GiB memory|mongo.x8.large|4,000|9,000|
|8 vCPUs, 64 GiB memory|mongo.x8.xlarge|8,000|18,000|
|16 vCPUs, 128 GiB memory|mongo.x8.2xlarge|16,000|36,000|
|32 vCPUs, 256 GiB memory|mongo.x8.4xlarge|32,000|72,000|
|Dedicated host|60 vCPUs, 440 GiB memory|dds.mongo.2xmonopolize|36,000|40,000|

|Node type|Category|Specification|Instance type|Maximum connections|Maximum IOPS|
|:--------|:-------|:------------|:------------|:------------------|:-----------|
|Mongos|General purpose|1 vCPU, 2 GiB memory|dds.mongos.mid|200|N/A|
|2 vCPUs, 4 GiB memory|dds.mongos.standard|400|
|4 vCPUs, 8 GiB memory|dds.mongos.large|1,000|
|8 vCPUs, 16 GiB memory|dds.mongos.xlarge|2,000|
|8 vCPUs, 32 GiB memory|dds.mongos.2xlarge|4,000|
|16 vCPUs, 64 GiB memory|dds.mongos.4xlarge|8,000|
|Shard|General purpose|1 vCPU, 2 GiB memory|dds.shard.mid|N/A|800|
|2 vCPUs, 4 GiB memory|dds.shard.standard|1,600|
|4 vCPUs, 8 GiB memory|dds.shard.large|3,200|
|8 vCPUs, 16 GiB memory|dds.shard.xlarge|6,400|
|8 vCPUs, 32 GiB memory|dds.shard.2xlarge|12,800|
|16 vCPUs, 64 GiB memory|dds.shard.4xlarge|12,800|
|Configserver|General purpose|1 vCPU, 2 GiB memory|dds.cs.mid|800|

