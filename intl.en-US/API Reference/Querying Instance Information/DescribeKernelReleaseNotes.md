# DescribeKernelReleaseNotes

You can call this operation to query the release notes of the minor database versions of a MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeKernelReleaseNotes&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeKernelReleaseNotes|The operation that you want to perform. Set the value to **DescribeKernelReleaseNotes**. |
|KernelVersion|String|No|mongodb\_20180522\_0.4.8|The number of the minor database version. For example: **mongodb\_20180522\_0.4.8**.

 -   If you specify this parameter, a list of version numbers later than the version specified is returned.
-   If you do not specify this parameter, a list of all the version numbers is returned. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query available regions. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ReleaseNotes|Array| |The list of version release notes. |
|ReleaseNote| | | |
|KernelVersion|String|mongodb\_20180619\_0.4.9|The version number. |
|ReleaseNote|String|Released the balancer switch limit for a sharded set|Publishes the log. |
|RequestId|String|F01D4DDA-CB72-4083-B399-AF4642294FE6|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeKernelReleaseNotes
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<DescribeKernelReleaseNotesResponse>
	  <RequestId>F01D4DDA-CB72-4083-B399-AF4642294FE6</RequestId>
	  <ReleaseNotes>
		    <ReleaseNote>
			      <KernelVersion>mongodb_20180619_0.4.9</KernelVersion>
			      <ReleaseNote>Released the balancer switch limit for a sharded set</ReleaseNote>
		    </ReleaseNote>
	  </ReleaseNotes>
</DescribeKernelReleaseNotesResponse>
```

`JSON` format

```
{
	"RequestId": "F01D4DDA-CB72-4083-B399-AF4642294FE6",
	"ReleaseNotes": {
		"ReleaseNote": [
			{
				"KernelVersion": "mongodb_20180619_0.4.9",
				"ReleaseNote":"Released the balancer limit for a sharded set"
			}
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

