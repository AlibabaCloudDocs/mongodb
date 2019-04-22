# Instance specifications {#concept_wrp_kg4_tdb .concept}

## Current instance specifications {#section_l1p_xlc_bfb .section}

Due to the iterative evolution of hardware resources, new specifications in the following tables are applied to instances that are purchased or whose specifications are changed as of July 10, 2017.

|Instance type|Specification type|Specifications|Code|Max number of connections|Max iops|Storage capacity|
|:------------|:-----------------|:-------------|:---|:------------------------|:-------|:---------------|
|Three-node replica set instance|General specifications|Single-core CPU and 2 GB memory|dds.mongo.mid|500|1,000|10 GB to 2,000 GB|
|Dual-core CPU and 4 GB memory|dds.mongo.standard|1,000|2,000|
|Quad-core CPU and 8 GB memory|dds.mongo.large|2,000|4,000|
|8-core CPU and 16 GB memory|dds.mongo.xlarge|4,000|8,000|
|8-core CPU and 32 GB memory|dds.mongo. 2xlarge|8,000|14,000|
|16-core CPU and 64 GB memory|dds.mongo. 4xlarge|16,000|16,000|
|Dedicated specifications|2-core, 16 GB|mongo.x8.medium|2,500|4,500|250 GB|
|Quad-core CPU and 32 GB memory|mongo.x8.large|5,000|9,000|500 GB|
|8-core CPU and 64 GB memory|mongo.x8.xlarge|10,000|18,000|1,000 GB|
|16-core CPU and 128 GB memory|mongo.x8.2xlarge|20,000|36000|2,000 GB|
|32-core CPU and 256 GB memory|mongo.x8.4xlarge|40,000|72,000|2,000 GB|
|Exclusive physical machine|60-core, 440 GB|dds.mongo. 2xmonopolize|100,000|100,000|3,000 GB|
|Standalone instance|General specifications|Single-core CPU and 2 GB memory|dds.n2.small. 1|2,000|min\{30 x Storage space, 20,000\}|20 GB to 2,000 GB|
|Dual-core CPU and 4 GB memory|dds.sn2.medium. 1|4,000|
|Dual-core CPU and 8 GB memory|dds.sn4.large. 1|6,000|
|Quad-core CPU and 8 GB memory|dds.sn2.large. 1|6,000|
|Quad-core CPU and 16 GB memory|dds.sn4.xlarge. 1|8,000|
|8-core CPU and 16 GB memory|dds.sn2.xlarge. 1|8,000|

|Node type|Specification type|Specifications|Specification code|Maximum number of connections|Maximum IOPS|
|:--------|:-----------------|:-------------|:-----------------|:----------------------------|:-----------|
|Mongos|General specifications|Single-core CPU and 2 GB memory|dds.mongos.mid|1,000|-|
|Dual-core CPU and 4 GB memory|dds.mongos.standard|2,000|
|Quad-core CPU and 8 GB memory|dds.mongos.large|4,000|
|8-core CPU and 16 GB memory|dds.mongos.xlarge|8,000|
|8-core CPU and 32 GB memory|dds.mongos. 2xlarge|16,000|
|16-core CPU and 64 GB memory|dds.mongos. 4xlarge|16,000|
|Shard|General specifications|Single-core CPU and 2 GB memory|dds.shard.mid|-|1,000|
|Dual-core CPU and 4 GB memory|dds.shard.standard|2,000|
|Quad-core CPU and 8 GB memory|dds.shard.large|4,000|
|8-core CPU and 16 GB memory|dds.shard.xlarge|8,000|
|8-core CPU and 32 GB memory|dds.shard. 2xlarge|14,000|
|16-core CPU and 64 GB memory|dds.shard. 4xlarge|16,000|
|Config server|General specifications|Single-core CPU and 2 GB memory|dds.cs.mid|1,000|

## Historical instance specifications {#section_hxm_lmc_bfb .section}

Specifications in the following tables are still applied to instances that were purchased before July 10, 2017 and whose specifications have never been changed.

|Specification type|Specifications|Specification code|Maximum number of connections|Maximum IOPS|
|:-----------------|:-------------|:-----------------|:----------------------------|:-----------|
|General specifications|Single-core CPU and 2 GB memory|dds.mongo.mid|200|800|
|Dual-core CPU and 4 GB memory|dds.mongo.standard|400|1,600|
|Quad-core CPU and 8 GB memory|dds.mongo.large|1,000|3,200|
|8-core CPU and 16 GB memory|dds.mongo.xlarge|2,000|6,400|
|8-core CPU and 32 GB memory|dds.mongo. 2xlarge|4,000|12,800|
|16-core CPU and 64 GB memory|dds.mongo. 4xlarge|8,000|12,800|
|Dedicated specifications|Dual-core CPU and 16 GB memory|mongo.x8.medium|2,000|4,500|
|Quad-core CPU and 32 GB memory|mongo.x8.large|4,000|9,000|
|8-core CPU and 64 GB memory|mongo.x8.xlarge|8,000|18,000|
|16-core CPU and 128 GB memory|mongo.x8.2xlarge|16,000|36,000|
|32-core CPU and 256 GB memory|mongo.x8.4xlarge|32,000|72,000|
|Exclusive physical machine|60-core CPU and 440 GB memory|dds.mongo. 2xmonopolize|36,000|40,000|

|Node type|Specification type|Specifications|Specification code|Maximum number of connections|Maximum IOPS|
|:--------|:-----------------|:-------------|:-----------------|:----------------------------|:-----------|
|Mongos|General specifications|Single-core CPU and 2 GB memory|dds.mongos.mid|200|-|
|Dual-core CPU and 4 GB memory|dds.mongos.standard|400|
|Quad-core CPU and 8 GB memory|dds.mongos.large|1,000|
|8-core CPU and 16 GB memory|dds.mongos.xlarge|2,000|
|8-core CPU and 32 GB memory|dds.mongos. 2xlarge|4,000|
|16-core CPU and 64 GB memory|dds.mongos. 4xlarge|8,000|
|Shard|General specifications|Single-core CPU and 2 GB memory|dds.shard.mid|-|800|
|Dual-core CPU and 4 GB memory|dds.shard.standard|1,600|
|Quad-core CPU and 8 GB memory|dds.shard.large|3,200|
|8-core CPU and 16 GB memory|dds.shard.xlarge|6,400|
|8-core CPU and 32 GB memory|dds.shard. 2xlarge|12,800|
|16-core CPU and 64 GB memory|dds.shard. 4xlarge|12,800|
|Config server|General specifications|Single-core CPU and 2 GB memory|dds.cs.mid|800|

