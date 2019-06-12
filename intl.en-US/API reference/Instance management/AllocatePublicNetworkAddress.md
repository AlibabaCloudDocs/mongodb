# AllocatePublicNetworkAddress {#doc_api_Dds_AllocatePublicNetworkAddress .reference}

You can call this operation to assign a public IP address to a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=AllocatePublicNetworkAddress) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|Action|String|No|AllocatePublicNetworkAddress|The operation that you want to perform. Set the value to **AllocatePublicNetworkAddress**.

 |
|NodeId|String|No|s-bpxxxxxxxx|The ID of the mongos in the sharded cluster instance.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B6D17591-B48B-4D31-9CD6-9B9796B2270A|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=AllocatePublicNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AllocatePublicNetworkAddressResponse> 
  <RequestId>B6D17591-B48B-4D31-9CD6-9B9796B2270A</RequestId>
</AllocatePublicNetworkAddressResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"B6D17591-B48B-4D31-9CD6-9B9796B2270A"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

