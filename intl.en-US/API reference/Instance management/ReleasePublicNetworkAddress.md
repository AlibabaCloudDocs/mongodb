# ReleasePublicNetworkAddress {#doc_api_Dds_ReleasePublicNetworkAddress .reference}

You can call this operation to release the public IP address of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ReleasePublicNetworkAddress) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReleasePublicNetworkAddress|The operation that you want to perform. Set the value to **ReleasePublicNetworkAddress**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|NodeId|String|No|s-bpxxxxxxxx|The ID of the mongos in the sharded cluster instance.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1D6AFE36-1AF5-4DE4-A954-672159D4CC69|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ReleasePublicNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&s-bpxxxxxxxx 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ReleasePublicNetworkAddressResponse> 
  <RequestId>B6D17591-B48B-4D31-9CD6-9B9796B2270A</RequestId>
</ReleasePublicNetworkAddressResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"1D6AFE36-1AF5-4DE4-A954-672159D4CC69"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

