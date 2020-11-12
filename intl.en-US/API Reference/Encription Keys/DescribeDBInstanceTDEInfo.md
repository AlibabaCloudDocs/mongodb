# DescribeDBInstanceTDEInfo

You can call this operation to query whether TDE is enabled for an ApsaraDB for MongoDB instance.

**Note:** For more information about this function, see [~~131048~~](~~131048~~)Configure TDE.

Before you call this operation, make sure that the following requirements are met:

-   A replica set or sharded cluster instance is used.
-   The storage engine of the instance is WiredTiger.
-   The database engine version of the instance is 4.0 or 4.2. If the database engine version of your instance is earlier than 4.0, you can call [UpgradeDBInstanceEngineVersion](~~67608~~) to upgrade the database engine.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceTDEInfo&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceTDEInfo|The operation that you want to perform. Set the value to **DescribeDBInstanceTDEInfo**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the Message Queue for Apache Kafka instance to be deleted. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|F4DD0E29-361B-42F2-9301-B0048CCCE5D6|The ID of the request. |
|TDEStatus|String|enabled|The TDE status. Valid values:

-   **enabled**
-   **disabled** |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeDBInstanceTDEInfo
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBInstanceTDEInfoResponse>
      <TDEStatus>enabled</TDEStatus>
      <RequestId>F4DD0E29-361B-42F2-9301-B0048CCCE5D6</RequestId>
</DescribeDBInstanceTDEInfoResponse>
```

`JSON` format

```
{
    "TDEStatus": "enabled",
    "RequestId": "F4DD0E29-361B-42F2-9301-B0048CCCE5D6"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

