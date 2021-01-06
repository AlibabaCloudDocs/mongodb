---
keyword: [ApsaraDB for MongoDB, ApsaraDB for MongoDB instance]
---

# Instance types

This topic describes the available instance types in ApsaraDB for MongoDB.

## IOPS

The maximum input/output operations per second \(IOPS\) of a local SSD is fixed to the instance type. The IOPS of an enhanced SSD is proportional to the storage capacity. The ECS instance type also limits the maximum IOPS. For more information, see the lists in this topic.

The IOPS of an enhanced SSD is calculated based on the following formula:

```
min {1,800 + 50 × Storage capacity, 50000, ECS-limited IOPS}
```

Description of the values in the preceding formula:

-   `1,800 + 50 × Storage capacity`: the basic calculation formula for the IOPS of the enhanced SSD.
-   `50,000`: the maximum IOPS of a single PL1 enhanced SSD. For more information, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).
-   `ECS-limited IOPS`: the maximum IOPS of the ECS instance type. For more information about ECS-limited IOPS of each instance type, see the list in this topic.

The actual IOPS of an instance is the minimum of the three values. Example:

-   The storage capacity of an instance is 20 GB. The result of 1,800 + 50 × 20 is 2800. Therefore, the actual IOPS of the instance is 2,800.
-   If the instance type is `mdb.shard.2x.xlarge.d`, the ECS-limited IOPS is 21,000. If the storage capacity of the instance is 6,000 GB, the calculated value is 301,800, which exceeds the maximum IOPS of a single PL1 enhanced SSD and the ECS-limited IOPS. In this case, the actual IOPS of the instance is 21,000.

**Note:** If the throughput of an instance reaches the upper limit, the IOPS of the instance also decreases. For more information, see [Storage I/O performance of the new generation of enterprise-level instance families](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

## Instance categories

The maximum number of connections and maximum IOPS vary based on different instance categories. Instances may not be able to support the maximum number of connections and maximum IOPS that are listed in [Current instance types](#section_l1p_xlc_bfb). The following list describes the instance categories.

|Category|Description|Assurance to maximum connections|Assurance to maximum IOPS|
|--------|-----------|--------------------------------|-------------------------|
|Dedicated cloud disk|Instances that occupy exclusive CPU, memory, storage media, and I/O resources.|Yes|Yes|
|Dedicated host|Instances that occupy exclusive CPU, memory, storage media, and I/O resources.|Yes|Yes|
|Dedicated local disk|Instances that occupy exclusive CPU and memory and share I/O resources with other instances on the same physical server.|Yes|No|
|General-purpose|Instances that occupy exclusive memory and share CPU and I/O resources with other instances on the same physical server.|Yes|No|

**Note:** For more information, see [Instance categories](/intl.en-US/Product Introduction/Instance type families.md).

## Current instance types

The following instance types are available for instances that were created on and after July 10, 2017 or whose configurations have been changed.

|Architecture|Category|Specification|Instance type|Maximum connections|Maximum IOPS|Storage capacity|
|:-----------|:-------|:------------|:------------|:------------------|:-----------|:---------------|
|Replica set instance|General-purpose|1 vCPU, 2 GiB memory|dds.mongo.mid|500|8000|10~2000GB|
|2 vCPUs, 4 GiB memory|dds.mongo.standard|1000|8000|
|4 vCPUs, 8 GiB memory|dds.mongo.large|3000|8000|
|8 vCPUs, 16 GiB memory|dds.mongo.xlarge|5000|8000|
|8 vCPUs, 32 GiB memory|dds.mongo.2xlarge|8000|14000|
|16 vCPUs, 64 GiB memory|dds.mongo.4xlarge|16000|16000|
|Dedicated local disk|2 vCPUs, 16 GiB memory|mongo.x8.medium|2500|4500|250GB|
|4 vCPUs, 32 GiB memory|mongo.x8.large|5000|9000|500GB|
|8 vCPUs, 64 GiB memory|mongo.x8.xlarge|10000|18000|1000GB|
|16 vCPUs, 128 GiB memory|mongo.x8.2xlarge|20000|36000|-   Subscription: 2000 to 3000 GB
-   Pay-as-you-go: 2000 GB |
|32 vCPUs, 256 GiB memory|mongo.x8.4xlarge|40000|72000|2000~3000GB|
|Dedicated host|60 vCPUs, 440 GiB memory|dds.mongo.2xmonopolize|100000|100000|2000~6000GB|
|Standalone instance|General-purpose|1 vCPU, 2 GiB memory|dds.n2.small.1|2000|min \{30 × Storage capacity, 20,000\}|20~2000GB|
|2 vCPUs, 4 GiB memory|dds.sn2.medium.1|4000|
|2 vCPUs, 8 GiB memory|dds.sn4.large.1|6000|
|4 vCPUs, 8 GiB memory|dds.sn2.large.1|6000|
|4 vCPUs, 16 GiB memory|dds.sn4.xlarge.1|8000|
|8 vCPUs, 16 GiB memory|dds.sn2.xlarge.1|8000|

|Node type|Category|Specification|Instance type|Maximum connections|Maximum IOPS|Storage cpacity|
|:--------|:-------|:------------|:------------|:------------------|:-----------|---------------|
|Mongos|General-purpose|1 vCPU, 2 GiB memory|dds.mongos.mid|1000|N/A|N/A|
|2 vCPUs, 4 GiB memory|dds.mongos.standard|2000|
|4 vCPUs, 8 GiB memory|dds.mongos.large|4000|
|8 vCPUs, 16 GiB memory|dds.mongos.xlarge|8000|
|8 vCPUs, 32 GiB memory|dds.mongos.2xlarge|16000|
|16 vCPUs, 64 GiB memory|dds.mongos.4xlarge|16000|
|Shard|General-purpose|1 vCPU, 2 GiB memory|dds.shard.mid|N/A|1000|10~2000GB|
|2 vCPUs, 4 GiB memory|dds.shard.standard|2000|
|4 vCPUs, 8 GiB memory|dds.shard.large|4000|
|8 vCPUs, 16 GiB memory|dds.shard.xlarge|8000|
|8 vCPUs, 32 GiB memory|dds.shard.2xlarge|14000|
|16 vCPUs, 64 GiB memory|dds.shard.4xlarge|16000|
|Dedicated local disk|2 vCPUs, 16 GiB memory|dds.shard.sn8.xlarge.3|4500|10~250GB|
|4 vCPUs, 32 GiB memory|dds.shard.sn8.2xlarge.3|9000|10~500GB|
|8 vCPUs, 64 GiB memory|dds.shard.sn8.4xlarge.3|18000|10~1000GB|
|16 vCPUs, 128 GiB memory|dds.shard.sn8.8xlarge.3|36000|10~2000GB|
|32 vCPUs, 256 GiB memory|dds.shard.sn8.16xlarge.3|72000|10~3000GB|
|Configserver|General-purpose|1 vCPU, 2 GiB memory|dds.cs.mid|1000|20GB|

## Historical instance types

The following instance types are available for instances that were created before July 10, 2017 and whose configurations have not been changed.

|Category|Specification|Instance type|Maximum connections|Maximum IOPS|
|:-------|:------------|:------------|:------------------|:-----------|
|General-purpose|1 vCPU, 2 GiB memory|dds.mongo.mid|200|800|
|2 vCPUs, 4 GiB memory|dds.mongo.standard|400|1600|
|4 vCPUs, 8 GiB memory|dds.mongo.large|1000|3200|
|8 vCPUs, 16 GiB memory|dds.mongo.xlarge|2000|6400|
|8 vCPUs, 32 GiB memory|dds.mongo.2xlarge|4000|12800|
|16 vCPUs, 64 GiB memory|dds.mongo.4xlarge|8000|12800|
|Dedicated CPU|2 vCPUs, 16 GiB memory|mongo.x8.medium|2000|4500|
|4 vCPUs, 32 GiB memory|mongo.x8.large|4000|9000|
|8 vCPUs, 64 GiB memory|mongo.x8.xlarge|8000|18000|
|16 vCPUs, 128 GiB memory|mongo.x8.2xlarge|16000|36000|
|32 vCPUs, 256 GiB memory|mongo.x8.4xlarge|32000|72000|
|Dedicated host|60 vCPUs, 440 GiB memory|dds.mongo.2xmonopolize|36000|40000|

|Node type|Category|Specification|Instance type|Maximum connections|Maximum IOPS|
|:--------|:-------|:------------|:------------|:------------------|:-----------|
|Mongos|General-purpose|1 vCPU, 2 GiB memory|dds.mongos.mid|200|N/A|
|2 vCPUs, 4 GiB memory|dds.mongos.standard|400|
|4 vCPUs, 8 GiB memory|dds.mongos.large|1000|
|8 vCPUs, 16 GiB memory|dds.mongos.xlarge|2000|
|8 vCPUs, 32 GiB memory|dds.mongos.2xlarge|4000|
|16 vCPUs, 64 GiB memory|dds.mongos.4xlarge|8000|
|Shard|General-purpose|1 vCPU, 2 GiB memory|dds.shard.mid|N/A|800|
|2 vCPUs, 4 GiB memory|dds.shard.standard|1600|
|4 vCPUs, 8 GiB memory|dds.shard.large|3200|
|8 vCPUs, 16 GiB memory|dds.shard.xlarge|6400|
|8 vCPUs, 32 GiB memory|dds.shard.2xlarge|12800|
|16 vCPUs, 64 GiB memory|dds.shard.4xlarge|12800|
|Configserver|General-purpose|1 vCPU, 2 GiB memory|dds.cs.mid|800|

