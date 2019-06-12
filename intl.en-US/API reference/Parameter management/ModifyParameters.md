# ModifyParameters {#doc_api_Dds_ModifyParameters .reference}

You can call this operation to modify the parameters of an AsparaDB for MongoDB instance.

The instance must be in the running state when you call this operation.

**Warning:** If some of the modified parameters require the instance to be restarted to take effect, the instance will be automatically restarted after the operation is complete. You can call the [DescribeParameterTemplates](intl.en-US/API reference/Parameter management/DescribeParameterTemplates.md#) operation to query which parameters require the instance to be restarted to take effect.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyParameters) simplifies API usage. You can use OpenAPI explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyParameters|The operation that you want to perform. Set the value to **ModifyParameters**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|Parameters|String|Yes|\{"operationProfiling.slowOpThresholdMs":"300"\}|The parameters for which to modify and their new values. This parameter is a JSON string in the \{“name”:”value”,”name”:”value2”\} format.

 **Note:** You can call the [DescribeParameterTemplates](~~67618~~) operation to query a list of default parameter templates.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in the specified sharded cluster instance.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|36923CC2-DDAB-4B48-A144-DA92C1E19537|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyParameters
&DBInstanceId=dds-bpxxxxxxxx
&Parameters={"operationProfiling.slowOpThresholdMs":"300"}
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyParametersResponse>
  <RequestId>36923CC2-DDAB-4B48-A144-DA92C1E19537</RequestId>
</ModifyParametersResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"36923CC2-DDAB-4B48-A144-DA92C1E19537"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

