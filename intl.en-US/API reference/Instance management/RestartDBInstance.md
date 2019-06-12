# RestartDBInstance {#doc_api_Dds_RestartDBInstance .reference}

You can call this operation to restart a MongoDB instance.

This operation can also be used to restart a shard or mongos node in a replica set instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=RestartDBInstance) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RestartDBInstance|The operation that you want to perform. Set the value to **RestartDBInstance**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard or mongos in the sharded cluster instance.

 **Note:** The sharded cluster instance will be restarted if this parameter is not specified.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|149C517D-B586-47BE-A107-8673E0ED77C6|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=RestartDBInstance
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<RestartDBInstanceResponse> 
  <RequestId>149C517D-B586-47BE-A107-8673E0ED77C6</RequestId>
</RestartDBInstanceResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"149C517D-B586-47BE-A107-8673E0ED77C6"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

