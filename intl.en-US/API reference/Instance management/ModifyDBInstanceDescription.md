# ModifyDBInstanceDescription {#doc_api_Dds_ModifyDBInstanceDescription .reference}

You can call this operation to change the name of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceDescription) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceDescription|The operation that you want to perform. Set the value to **ModifyDBInstanceDescription**.

 |
|DBInstanceDescription|String|Yes|testdata|The name of the instance.

 **Note:** 

 

-   It cannot start with http:// or https://.

-   It must start with a letter.
-   It can contain letters, underscores \(\_\), hyphens \(-\), and digits. It must be 2 to 256 characters in length.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** **NodeId**also needs to be specified if you need to modify the name of a shard or mongos node in a replica set instance.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard or mongos in the sharded cluster instance.

 **Note:** This parameter is available only when **DBInstanceId** is the ID of the sharded cluster instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|06F8F642-4009-4FFC-80C4-9D67DBF7B74E|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceDescription
&DBInstanceDescription=testdata
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDBInstanceDescriptionResponse> 
  <RequestId>06F8F642-4009-4FFC-80C4-9D67DBF7B74E</RequestId> 
</ModifyDBInstanceDescriptionResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"06F8F642-4009-4FFC-80C4-9D67DBF7B74E"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

