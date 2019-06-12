# ModifyDBInstanceNetExpireTime {#doc_api_Dds_ModifyDBInstanceNetExpireTime .reference}

You can call this operation to extend the retention period of the classic network of a MongoDB instance.

Ensure that the instance meet the following conditions when you call this operation:

-   The instance must be running.
-   The network of the instance is in hybrid access mode.

**Note:** This operation is applicable to replica set instances and sharded cluster instances. ModifyDBInstanceNetExpireTime cannot be performed on standalone instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceNetExpireTime) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceNetExpireTime|The operation that you want to perform. Set the value to **ModifyDBInstanceNetExpireTime**.

 |
|ClassicExpendExpiredDays|Integer|Yes|30|The retention period of the original classic network address. Valid values: **14**, **30**, **60**, and**120**. Unit: day.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|ConnectionString|String|No|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The connection address of the instance

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|459E7D5C-38DA-4E14-9C82-5B5AF693DBAB|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceNetExpireTime
&ClassicExpendExpiredDays=30
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDBInstanceNetExpireTimeResponse>
  <RequestId>459E7D5C-38DA-4E14-9C82-5B5AF693DBAB</RequestId> 
</ModifyDBInstanceNetExpireTimeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"459E7D5C-38DA-4E14-9C82-5B5AF693DBAB"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

