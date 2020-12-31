# EvaluateResource

在新购实例或对实例进行变配之前调用EvaluateResource接口评估是否有足够的资源。

本接口适用于MongoDB副本集、分片集群资源的评估。支持评估新购资源以及副本集、分片集群或单个分片的变配。

**说明：** 本接口每分钟调用不得超过200次，超出会被限制流量。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=EvaluateResource&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|EvaluateResource|要执行的操作，取值：**EvaluateResource**。 |
|Engine|String|是|MongoDB|数据库引擎，取值：**MongoDB**。 |
|EngineVersion|String|是|4.0|数据库版本号。取值：**3.4**、**4.0**或**4.2**。 |
|RegionId|String|是|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |
|ZoneId|String|是|cn-hangzhou-h|可用区ID，您可以调用[DescribeRegions](~~61933~~)查询。 |
|DBInstanceClass|String|否|dds.mongo.mid|实例规格，评估副本集资源时必须指定。规格详情请参见[实例规格表](~~57141~~)。 |
|ShardsInfo|String|否|\{"NodeId": "d-xxx", "NodeClass": "dds.shard.standard"\}|分片集群的分片信息，评估分片集群资源时必须指定。

 -   评估新购分片集群资源时，需指定每个分片的规格，格式为JSON格式字符串。示例如下：

```

    {
     "ConfigSvrs":
         [{"Storage":20,"DBInstanceClass":"dds.cs.mid"}],
     "Mongos":
         [{"DBInstanceClass":"dds.mongos.standard"},{"DBInstanceClass":"dds.mongos.standard"}],
     "Shards":
         [{"Storage":50,"DBInstanceClass":"dds.shard.standard"},{"Storage":50,"DBInstanceClass":"dds.shard.standard"},   {"Storage":50,"DBInstanceClass":"dds.shard.standard"}]
    }
    
```

各参数说明如下：

    -   `ConfigSvrs`、`Mongos`、`Shards`分别对应Configserver、Mongos、Shards节点。
    -   `Storage`：指定目标分片的存储空间。
    -   `DBInstanceClass`：指定目标分片的规格，规格详情请参见[实例规格表](~~57141~~)。
-   评估分片集群变配资源时，仅需指定节点信息即可，格式为JSON格式字符串。示例如下：

```

    {
     "NodeId": "d-xxx", "NodeClass": "dds.shard.standard"
    } 
    
```

各参数说明如下：

    -   `NodeId`：指定目标节点ID。您可以调用[DescribeDBInstanceAttribute](~~62010~~)查询。
    -   `NodeClass`：指定目标节点的规格。规格详情请参见[实例规格表](~~57141~~)。 |
|DBInstanceId|String|否|dds-bpxxxxxxxx|实例ID，评估变配资源时必须指定。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceAvailable|String|1|展示当前区域是否有可用的资源。返回值：

 -   **1**：资源足够。
-   **0**：资源不足。 |
|Engine|String|MongoDB|数据库引擎，固定为MongoDB。 |
|EngineVersion|String|4.0|数据库版本号。 |
|RequestId|String|AE2DE465-E45F-481F-ABD8-37D641738660|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=EvaluateResource
&Engine=MongoDB
&EngineVersion=4.0
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-h
&DBInstanceClass=dds.mongo.mid
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DBInstanceAvailable>1</DBInstanceAvailable>
<EngineVersion>4.0</EngineVersion>
<RequestId>AE2DE465-E45F-481F-ABD8-37D641738660</RequestId>
<Engine>MongoDB</Engine>
```

`JSON` 格式

```
{
	"DBInstanceAvailable": 1,
	"EngineVersion": "4.0",
	"RequestId": "AE2DE465-E45F-481F-ABD8-37D641738660",
	"Engine": "MongoDB"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

