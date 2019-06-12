# DeleteDBInstance {#doc_api_Dds_DeleteDBInstance .reference}

You can call this operation to release a MongoDB instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The instance is in the running state.
-   The billing method of the instance is Pay-As-You-Go.

**Note:** When an instance is released, all the data in the instance is lost and cannot be retrieved. Exercise caution when your release instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DeleteDBInstance) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteDBInstance|The operation that you want to perform. Set the value to **DeleteDBInstance**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters, and cannot exceed 64 characters in length.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|72651AF9-7897-41A7-8B67-6C15C7F26A0A|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DeleteDBInstance
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteDBInstanceResponse>
  <RequestId>72651AF9-7897-41A7-8B67-6C15C7F26A0A</RequestId> 
</DeleteDBInstanceResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"72651AF9-7897-41A7-8B67-6C15C7F26A0A"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

