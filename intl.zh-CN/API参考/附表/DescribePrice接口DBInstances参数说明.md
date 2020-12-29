# DescribePrice接口DBInstances参数说明

本文对DescribePrice接口中的DBInstances参数进行详细说明。该接口用于查询创建MongoDB实例、升级配置或续费操作产生的费用。

|参数名称|类型|是否必须|说明|示例|
|----|--|----|--|--|
|DBInstanceId|String|否|实例ID。您可以调用[DescribeDBInstances](~~61939~~)查询实例列表。当**OrderType**为**UPGRADE**或**RENEW**时必传。|dds-bp1xxxxxxxxxxxxx|
|RegionId|String|是|区域ID。您可以通过[DescribeRegions](~~61933~~)查看可用的区域。|cn-hangzhou|
|ZoneId|String|是|可用区ID。您可以通过[DescribeRegions](~~61933~~)查看可用的可用区。|cn-hangzhou-h|
|Engine|String|是|数据库类型。固定为**MongoDB**。|MongoDB|
|EngineVersion|String|是|数据库版本。取值：-   **3.4**
-   **4.0**
-   **4.2**

|4.2|
|DBInstanceClass|String|否|实例规格。详情请参见[实例规格表](~~57141~~)。|dds.mongo.mid|
|DBInstanceStorage|String|是|存储空间。单位：GB。|20|
|ReplicationFactor|String|否|节点数。取值：-   **1**
-   **3**
-   **5**
-   **7**

|3|
|NetworkType|String|否|网络类型。取值：-   **VPC**：专有网络。
-   **Classic**：经典网络。

默认为：**Classic**。

|VPC|
|VPCId|String|否|VPC的ID。当**NetworkType**为**VPC**时必传。|vpc-bp1xxxxxxxxxxxxxx|
|VSwitchId|String|否|VSwitch的ID。当**NetworkType**为**VPC**时必传。|vsw-bp1xxxxxxxxxxxxxx|
|ChargeType|String|否|付费类型。取值：-   **PostPaid**：按量付费。
-   **PrePaid**：包年包月。

|PostPaid|
|AutoPay|String|否|自动付费。取值：-   **True**：是。
-   **False**：否。

|True|
|Period|String|否|包年包月的购买时长，单位为月。当**ChargeType**为**PrePaid**时必填。|1|
|configServers|JSON|否|分片集群configserver节点规格。子参数：-   **nodeClass**：ConfigServers的规格。
-   **nodeStorage**：ConfigServers的存储容量。

本参数的值固定为：`[{"nodeClass":"dds.cs.mid","nodeStorage":"20"}]`|\[\{"nodeClass":"dds.cs.mid","nodeStorage":"20"\}\]|
|mongos|JSON|否|分片集群mongos节点规格。详情请参见[实例规格表](~~57141~~)子参数：-   **nodeClass**：mongos的规格。

|\[\{"nodeClass":"dds.mongos.mid"\},\{"nodeClass":"dds.mongos.mid"\}\]|
|shards|JSON|否|分片集群shard节点规格。详情请参见[实例规格表](~~57141~~)子参数：-   **nodeClass**：shards的规格。
-   **nodeStorage**：shards的存储容量。
-   **ReadonlyReplicas**：只读节点的数量。取值：**0**、**1**、**2**、**3**、**4**、**5**。

|\[\{"nodeClass":"dds.shard.mid","ReadonlyReplicas":"1","nodeStorage":"10"\},\{"nodeClass":"dds.shard.mid","ReadonlyReplicas":"1","nodeStorage":"10"\}\]|

