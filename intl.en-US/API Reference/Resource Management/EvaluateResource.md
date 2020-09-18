# EvaluateResource

You can call this operation to check whether sufficient resources are available in the region where you want to create or upgrade an ApsaraDB for MongoDB instance.

This operation applies to replica set instances and sharded cluster instances. You can call this operation to check whether resources are sufficient for creating an instance, upgrading an instance, or upgrading a single node of a sharded cluster instance.

**Note:** You can call this operation a maximum of 200 times per minute.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=EvaluateResource&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Location|Type|Required|Example|Description|
|---------|--------|----|--------|-------|-----------|
|Action|Query|String|Yes|EvaluateResource|The operation that you want to perform. Set the value to **EvaluateResource**. |
|Engine|Query|String|Yes|MongoDB|The database engine. Set the value to **MongoDB**. |
|EngineVersion|Query|String|Yes|4.0|The version of the database engine. Valid values:

-   **3.2**
-   **3.4**
-   **4.0**
-   **4.2** |
|RegionId|Query|String|Yes|cn-hangzhou|The ID of the region. You can call [DescribeRegions](~~61933~~) to query the region ID. |
|ZoneId|Query|String|Yes|cn-hangzhou-h|The ID of the zone. You can call [DescribeRegions](~~61933~~) to query the zone ID. |
|DBInstanceClass|Query|String|No|dds.mongo.mid|The instance type. This parameter is required when you check whether resources are sufficient for creating or upgrading a replica set instance. For more information, see [Instance types](~~57141~~). |
|ShardsInfo|Query|String|No|\{"NodeId": "d-xxx", "NodeClass": "dds.shard.standard"\}|The node information. This parameter is required when you check whether resources are sufficient for creating or upgrading a sharded cluster instance.

-   To check whether resources are sufficient for creating a sharded cluster instance, specify the configurations of each node in the instance. The value must be a JSON string. The following example shows how to specify the node configurations:

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

The following list describes the parameters:

    -   `ConfigSvrs` specifies the configurations of the config server. `Mongos` specifies the configurations of the mongos nodes.`Shards` specifies the configurations of the shards.
    -   `Storage`: the storage space of the node.
    -   `DBInstanceClass`: the instance type of the node. For more information, see [Instance types](~~57141~~).
-   To check whether resources are sufficient for upgrading a node of a sharded cluster instance, specify the information of the node to be upgraded only. The value must be a JSON string. The following example shows how to specify the information of a node:

```

    {
     "NodeId": "d-xxx", "NodeClass": "dds.shard.standard"
    } 
    
```

The following list describes the parameters:

    -   `NodeId`: the ID of the node. You can call [DescribeDBInstanceAttribute](~~62010~~) to query the node ID.
    -   `NodeClass`: the instance type of the node. For more information, see [Instance types](~~57141~~). |
|DBInstanceId|Query|String|No|dds-bpxxxxxxxx|The ID of the ApsaraDB for MongoDB instance. This parameter is required when you check whether resources are sufficient for upgrading an instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceAvailable|String|1|Indicates whether the resources are sufficient in the region. Valid values:

-   **1**: The resources are sufficient.
-   **0**: The resources are insufficient. |
|Engine|String|MongoDB|The database engine. The returned value is MongoDB. |
|EngineVersion|String|4.0|The version of the database engine. |
|RequestId|String|AE2DE465-E45F-481F-ABD8-37D641738660|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=EvaluateResource
&Engine=MongoDB
&EngineVersion=4.0
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-h
&DBInstanceClass=dds.mongo.mid
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DBInstanceAvailable>1</DBInstanceAvailable>
<EngineVersion>4.0</EngineVersion>
<RequestId>AE2DE465-E45F-481F-ABD8-37D641738660</RequestId>
<Engine>MongoDB</Engine>
```

`JSON` format

```
{
    "DBInstanceAvailable": 1,
    "EngineVersion": "4.0",
    "RequestId": "AE2DE465-E45F-481F-ABD8-37D641738660",
    "Engine": "MongoDB"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

