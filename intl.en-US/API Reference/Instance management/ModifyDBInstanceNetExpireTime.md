# ModifyDBInstanceNetExpireTime

You can call this operation to extend the retention period of the classic network of a MongoDB instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance is in the running state.
-   The network of the instance is in hybrid access mode.

**Note:** This operation is applicable only to replica set and sharded cluster instances, but not to standalone instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceNetExpireTime&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceNetExpireTime|The operation that you want to perform. Set the value to **ModifyDBInstanceNetExpireTime**. |
|ClassicExpendExpiredDays|Integer|Yes|30|The retention period of the original classic network address. Valid values: **14**, **30**, **60**, and**120**. Unit: day. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|ConnectionString|String|No|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The connection string of the instance |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|459E7D5C-38DA-4E14-9C82-5B5AF693DBAB|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceNetExpireTime
&ClassicExpendExpiredDays=30
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<ModifyDBInstanceNetExpireTimeResponse>
	  <RequestId>459E7D5C-38DA-4E14-9C82-5B5AF693DBAB</RequestId>
</ModifyDBInstanceNetExpireTimeResponse>
```

`JSON` format

```
{
	"RequestId": "459E7D5C-38DA-4E14-9C82-5B5AF693DBAB"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

