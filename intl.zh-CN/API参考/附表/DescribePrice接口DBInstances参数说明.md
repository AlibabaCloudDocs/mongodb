# DescribePrice接口DBInstances参数说明

本文对DescribePrice接口中的DBInstances参数进行详细说明。该接口用于查询创建MongoDB实例、升级配置或续费操作产生的费用。

|参数名称|类型|是否必须|说明|示例|
|----|--|----|--|--|
|DBInstanceId|String|否|实例ID。您可以调用[DescribeDBInstances](~~61939~~)查询实例列表。**说明：** 当订单类型为变更配置或续费实例时，需要配置该参数。

|dds-bp13bbf2407f\*\*\*\*|
|RegionId|String|是|区域ID。您可以通过[DescribeRegions](~~61933~~)查看可用的区域。|cn-hangzhou|
|ZoneId|String|是|可用区ID。您可以通过[DescribeRegions](~~61933~~)查看可用的可用区。|cn-hangzhou-h|
|Engine|String|是|数据库类型。固定为**MongoDB**。|MongoDB|
|EngineVersion|String|是|数据库版本。取值：-   **3.4**
-   **4.0**
-   **4.2**

|4.2|
|DBInstanceClass|String|否|实例规格。详情请参见[实例规格表](~~57141~~)。|dds.mongo.mid|
|DBInstanceStorage|String|是|存储空间。单位：GB。|20|
|ReplicationFactor|String|否|节点数。取值为1、3、5、7。|3|
|NetworkType|String|否|网络类型。取值：-   VPC：专有网络。
-   Classic：经典网络。

默认为经典网络。

|VPC|
|VPCId|String|否|专有网络的ID。**说明：** 当网络类型为专有网络时，需要配置该参数。

|vpc-bp1q2qqm4vxo6e6zl\*\*\*\*|
|VSwitchId|String|否|虚拟交换机的ID。**说明：** 当网络类型为专有网络时，需要配置该参数。

|vsw-bp1lb40helio22b6d\*\*\*\*|
|ChargeType|String|否|付费类型。取值：-   PostPaid：按量付费。
-   PrePaid：包年包月。

|PostPaid|
|AutoPay|String|否|自动付费。取值：-   True：是。
-   False：否。

|True|
|Period|String|否|包年包月的购买时长，单位为月。**说明：** 当付费类型为包年包月时，需要配置该参数。

|1|
|configServers|JSON|否|分片集群ConfigServer节点规格。包含如下参数：-   nodeClass：ConfigServer节点的规格。
-   nodeStorage：ConfigServer节点的存储容量。

默认值为`[{"nodeClass":"dds.cs.mid","nodeStorage":"20"}]`|`[{"nodeClass":"dds.cs.mid","nodeStorage":"20"}]`|
|mongos|JSON|否|分片集群Mongos节点规格。包含参数：nodeClass：Mongos节点的规格。

Mongos节点支持的规格信息请参见[实例规格表](~~57141~~)。

|`[{"nodeClass":"dds.mongos.mid"},{"nodeClass":"dds.mongos.mid"}]`|
|shards|JSON|否|分片集群Shard节点规格。包含如下参数：-   nodeClass：Shard节点的规格。
-   nodeStorage：Shard节点的存储容量。
-   ReadonlyReplicas：只读节点的数量。取值为0~5的整数。

Shard节点支持的规格信息请参见[实例规格表](~~57141~~)。

|`[{"nodeClass":"dds.shard.mid","ReadonlyReplicas":"1","nodeStorage":"10"},{"nodeClass":"dds.shard.mid","ReadonlyReplicas":"1","nodeStorage":"10"}]`|

