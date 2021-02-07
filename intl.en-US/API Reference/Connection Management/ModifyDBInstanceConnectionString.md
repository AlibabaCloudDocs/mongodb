# ModifyDBInstanceConnectionString

You can call this operation to modify the connection string of a MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceConnectionString&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceConnectionString|The operation that you want to perform. Set the value to **ModifyDBInstanceConnectionString**. |
|CurrentConnectionString|String|Yes|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The current connection string, which is to be modified. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you set this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter. |
|NewConnectionString|String|Yes|aliyuntest111|The new connection string. It must be 8 to 64 characters in length and can contain letters and digits. It must start with a lowercase letter.

 **Note:** You need only to specify the prefix of the connection string. The content other than the prefix cannot be modified. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the most recent region list. |
|NodeId|String|No|s-bpxxxxxxxx|The ID of the mongos in the specified sharded cluster instance. Only one mongos ID can be specified in each call.

 **Note:** This parameter is valid only if you set the **DBInstanceId** parameter to the ID of a sharded cluster instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|FF36A84C-0694-42D0-861D-C383E8E4FAAF|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceConnectionString
&CurrentConnectionString=s-bpxxxxxxxx.mongodb.rds.aliyuncs.com
&NewConnectionString=aliyuntest111
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<ModifyDBInstanceConnectionStringResponse>
	  <RequestId>FF36A84C-0694-42D0-861D-C383E8E4FAAF</RequestId>
</ModifyDBInstanceConnectionStringResponse>
```

`JSON` format

```
{
	"RequestId": "FF36A84C-0694-42D0-861D-C383E8E4FAAF"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

