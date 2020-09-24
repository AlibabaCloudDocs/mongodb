# DescribeAvailableEngineVersion

You can call this operation to query the engine versions that an ApsaraDB for MongoDB instance can be upgraded to.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeAvailableEngineVersion&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAvailableEngineVersion|The operation that you want to perform. Set the value to **DescribeAvailableEngineVersion**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~61933~~) to query. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|52507B6B-003B-47A3-A0A3-9FE992C7A243|The ID of the request. |
|EngineVersions|List|\{"EngineVersion": \["4.0" \]\}|The engine versions that the ApsaraDB for MongoDB instance can be upgraded to.

**Note:** An empty string is returned if the latest version is being used. |

## Examples

Sample requests

```

http(s)://mongodb.aliyuncs.com/? Action=DescribeAvailableEngineVersion
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DescribeAvailableEngineVersionResponse>
	  <EngineVersions>
		    <EngineVersion>4.0</EngineVersion>
	  </EngineVersions>
	  <RequestId>52507B6B-003B-47A3-A0A3-9FE992C7A243</RequestId>
</DescribeAvailableEngineVersionResponse>
```

`JSON` format

```
{
	"RequestId":"52507B6B-003B-47A3-A0A3-9FE992C7A243",
	"EngineVersions":{
		"EngineVersion":[
			"4.0"
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

