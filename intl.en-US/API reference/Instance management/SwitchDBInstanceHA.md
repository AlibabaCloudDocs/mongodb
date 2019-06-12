# SwitchDBInstanceHA {#doc_api_Dds_SwitchDBInstanceHA .reference}

You can call this operation to switch between the primary and secondary nodes in a MongoDB instance.

The instance must be in the running state when you call this operation.

**Note:** 

 

-   This operation is applicable to replica set instances and sharded cluster instances. SwitchDBInstanceHA cannot be performed on standalone instances.

-   On replica set instances, the switch is performed between instances. On sharded cluster instances, the switch is performed between shards.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=SwitchDBInstanceHA) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SwitchDBInstanceHA|The operation that you want to perform. Set the value to **SwitchDBInstanceHA**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard in the sharded cluster instance.

 **Note:** You must specify this parameter when the value specified for **DBInstanceId** is the ID of a sharded cluster instance. Otherwise, ignore this parameter.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|26BD4E5F-BDB4-47BA-B232-413AA78CFA8F|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=SwitchDBInstanceHA
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<SwitchDBInstanceHAResponse>
  <RequestId>26BD4E5F-BDB4-47BA-B232-413AA78CFA8F</RequestId>
</SwitchDBInstanceHAResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"26BD4E5F-BDB4-47BA-B232-413AA78CFA8F"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

