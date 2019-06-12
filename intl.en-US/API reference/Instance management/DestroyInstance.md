# DestroyInstance {#doc_api_Dds_DestroyInstance .reference}

You can call this operation to release a MongoDB instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The billing method of the instance is subscription.
-   The instance has expired and is in the **Locking** state.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DestroyInstance) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DestroyInstance|The operation that you want to perform. Set the value to **DestroyInstance**.

 |
|InstanceId|String|No|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** **InstanceId** and **DBInstanceId** serve the same function. You only need to specify one of them.

 |
|DBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** **InstanceId** and **DBInstanceId** serve the same function. You only need to specify one of them.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters, and cannot exceed 64 characters in length.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DestroyInstance
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DestroyInstanceResponse>
  <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId> 
</DestroyInstanceResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

