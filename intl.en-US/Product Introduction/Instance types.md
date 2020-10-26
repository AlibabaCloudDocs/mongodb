---
keyword: [ApsaraDB for MongoDB, Alibaba Cloud ApsaraDB Instance]
---

# Instance types

This topic describes the instance types available in ApsaraDB for MongoDB.

## Current instance types

The following new instance types are used for instances that were created on and after July 10, 2017 or whose configurations have been changed.

|Category|Instance type|Specification|Code|Maximum connections|Maximum IOPS|Storage capacity|
|:-------|:------------|:------------|:---|:------------------|:-----------|:---------------|
|Replica set instances|General-purpose|1 Core - 2 GB|dds.mongo.mid|500|8,000|10 GB to 2000 GB|
|2 Core - 4 GB|dds.mongo.standard|1,000|8,000|
|4 Core - 8 GB|dds.mongo.large|3,000|8,000|
|8 Core - 16 GB|dds.mongo.xlarge|5,000|8000|
|8 Core - 32 GB|dds.mongo.2xlarge|8000|14000|
|16 Core - 64 GB|dds.mongo.4xlarge|16,000|16,000|
|Dedicated specifications|2-core 16 GB|mongo.x8.medium|2500|4,500|250 GB|
|4-core 32 GB|mongo.x8.large|5,000|9,000|500 GB|
|8-core 64 GB|mongo.x8.xlarge|10000|18,000|1,000 GB|
|16-core 128 GB|mongo.x8.2xlarge|20,000|36,000|-   Subscription: 2000-3000GB
-   Pay-as-you-go: 2,000 GB |
|32-core 256 GB|mongo.x8.4xlarge|40,000|72,000|2000-3000GB|
|Dedicated physical machine|60-core 440 GB|dds.mongo.2xmonopolize|100000|100000|2000-6000GB|
|Standalone instance|General-purpose|1-core 2 GB|dds.n2.small.1|2,000|min\{30 × Storage capacity, 20,000\}|20 GB to 2000 GB|
|2-core 4 GB|dds.sn2.medium.1|4,000|
|2-core 8 GB|dds.sn4.large.1|6000|
|4-core 8 GB|dds.sn2.large.1|6000|
|4-core 16 GB|dds.sn4.xlarge.1|8000|
|8-core 16 GB|dds.sn2.xlarge.1|8000|

|Node Type|Instance type|Specification|Code|Maximum connections|Maximum IOPS|Storage capacity|
|:--------|:------------|:------------|:---|:------------------|:-----------|----------------|
|Mongos|General-purpose|1-core 2 GB|dds.mongos.mid|1,000|N/A|All partitions are selected by default.|
|2-core 4 GB|dds.mongos.standard|2,000|
|4 Core - 8 GB|dds.mongos.large|4,000|
|8 Core - 16 GB|dds.mongos.xlarge|8000|
|8 Core - 32 GB|dds.mongos.2xlarge|16,000|
|16-core 64 GB|dds.mongos.4xlarge|16,000|
|Shard|General-purpose|1-core 2 GB|dds.shard.mid|N/A|1,000|10 GB to 2000 GB|
|2-core 4 GB|dds.shard.standard|2,000|
|4 Core - 8 GB|dds.shard.large|4,000|
|8 Core - 16 GB|dds.shard.xlarge|8000|
|8 Core - 32 GB|dds.shard.2xlarge|14,000|
|16 Core - 64 GB|dds.shard.4xlarge|16,000|
|Dedicated specifications|2-core 16 GB|dds.shard.sn8.xlarge.3|4,500|10-250GB|
|4 cores, 32 GB|dds.shard.sn8.2xlarge.3|9,000|10-500GB|
|8 cores, 64 GB|dds.shard.sn8.4xlarge.3|18,000|10-1000GB|
|16 cores, 128 GB|dds.shard.sn8.8xlarge.3|36,000|10 GB to 2000 GB|
|32 cores, 256 GB|dds.shard.sn8.16xlarge.3|72,000|10-3000GB|
|Configserver|General-purpose|1-core 2 GB|dds.cs.mid|1,000|20 GB|

## Historical instance types

The following instance types will be used for instances that were created before July 10, 2017 and whose configurations have not been changed.

|Instance type|Specification|Code|Maximum connections|Maximum IOPS|
|:------------|:------------|:---|:------------------|:-----------|
|General specifications|1 Core - 2 GB|dds.mongo.mid|200|800|
|2 Core - 4 GB|dds.mongo.standard|400|1600|
|4 Core - 8 GB|dds.mongo.large|1,000|3200|
|8-core 16 GB|dds.mongo.xlarge|2,000|6400|
|8-core 32 GB|dds.mongo.2xlarge|4000|12800|
|16-core 64 GB|dds.mongo.4xlarge|8000|12,800|
|Dedicated|2-core 16 GB|mongo.x8.medium|2,000|4500|
|4-core 32 GB|mongo.x8.large|4,000|9,000|
|8-core 64 GB|mongo.x8.xlarge|8000|18000|
|16-core 128 GB|mongo.x8.2xlarge|16,000|36000|
|32-core 256 GB|mongo.x8.4xlarge|32000|72000|
|Dedicated host|60-core 440 GB|dds.mongo.2xmonopolize|36,000|40000|

|Node type|Instance type|Specification|Code|Maximum connections|Maximum IOPS|
|:--------|:------------|:------------|:---|:------------------|:-----------|
|Mongos|General-purpose|1-core 2 GB|dds.mongos.mid|200|N/A|
|2-core 4 GB|dds.mongos.standard|400|
|4-core 8 GB|dds.mongos.large|1,000|
|8-core 16 GB|dds.mongos.xlarge|2,000|
|8-core 32 GB|dds.mongos.2xlarge|4,000|
|16-core 64 GB|dds.mongos.4xlarge|8000|
|Shard|General-purpose|1-core 2 GB|dds.shard.mid|N/A|800|
|2-core 4 GB|dds.shard.standard|1600|
|4-core 8 GB|dds.shard.large|3200|
|8-core 16 GB|dds.shard.xlarge|6400|
|8-core 32 GB|dds.shard.2xlarge|12800|
|16-core 64 GB|dds.shard.4xlarge|12,800|
|Configserver|General-purpose|1-core 2 GB|dds.cs.mid|800|

