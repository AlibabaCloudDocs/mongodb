# RestartDBInstance

You can call this operation to restart an ApsaraDB for MongoDB instance.

This operation can also be used to restart a shard or mongos node in a sharded cluster instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=RestartDBInstance&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RestartDBInstance|The operation that you want to perform. Set the value to **RestartDBInstance**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard or mongos node in the sharded cluster instance.

 **Note:** The sharded cluster instance is restarted if you do not specify this parameter. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|149C517D-B586-47BE-A107-8673E0ED77C6|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=RestartDBInstance
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RestartDBInstanceResponse>
	  <RequestId>149C517D-B586-47BE-A107-8673E0ED77C6</RequestId>
</RestartDBInstanceResponse>
```

`JSON` format

```
{
	"RequestId": "149C517D-B586-47BE-A107-8673E0ED77C6"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

