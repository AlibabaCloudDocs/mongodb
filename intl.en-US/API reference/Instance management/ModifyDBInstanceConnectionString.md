# ModifyDBInstanceConnectionString {#doc_api_Dds_ModifyDBInstanceConnectionString .reference}

You can call this operation to modify the connection address of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceConnectionString) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceConnectionString|The operation that you want to perform. Set the value to **ModifyDBInstanceConnectionString**.

 |
|CurrentConnectionString|String|Yes|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The current connection address, which is to be modified.

 |
|NewConnectionString|String|Yes|aliyuntest111|The new connection address. It must be 8 to 64 characters in length and can contain letters and digits. It must start with a lowercase letter.

 **Note:** You only need to specify the prefix of the connection address. The content other than the prefix cannot be modified.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|NodeId|String|No|s-bpxxxxxxxx|The ID of the mongos in the specified sharded cluster instance. Only one mongos ID can be specified in each call.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|FF36A84C-0694-42D0-861D-C383E8E4FAAF|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceConnectionString
&CurrentConnectionString=s-bpxxxxxxxx.mongodb.rds.aliyuncs.com
&NewConnectionString=aliyuntest111
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDBInstanceConnectionStringResponse> 
  <RequestId>FF36A84C-0694-42D0-861D-C383E8E4FAAF</RequestId>
</ModifyDBInstanceConnectionStringResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"FF36A84C-0694-42D0-861D-C383E8E4FAAF"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

