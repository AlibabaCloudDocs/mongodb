# DescribeKernelReleaseNotes {#doc_api_Dds_DescribeKernelReleaseNotes .reference}

You can call this operation to query the release notes of the minor database versions of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeKernelReleaseNotes) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeKernelReleaseNotes|The operation that you want to perform. Set the value to **DescribeKernelReleaseNotes**.

 |
|KernelVersion|String|No|Mongodb\_20180522\_0.4.8|The number of the minor database version. For example: **mongodb\_20180522\_0.4.8**.

 -   If you specify this parameter, a list of version numbers later than the version specified is returned.
-   If you do not specify this parameter, a list of all the version numbers is returned.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ReleaseNotes| | |The list of version release notes.

 |
|└KernelVersion|String|mongodb\_20180619\_0.4.9|The version number.

 |
|└ReleaseNote|String|Released the balancer switch limit for a sharded set.|The release notes.

 |
|RequestId|String|F01D4DDA-CB72-4083-B399-AF4642294FE6|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeKernelReleaseNotes
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
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

``` {#json_return_success_demo}
{
	"RequestId":"F01D4DDA-CB72-4083-B399-AF4642294FE6",
	"ReleaseNotes":{
		"ReleaseNote":[
			{
				"KernelVersion":"mongodb_20180619_0.4.9",
				"ReleaseNote":"Released the balancer limit for a sharded set"
			}
		]
	}
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

