# ModifyDBInstanceDescription

You can call this operation to change the name of an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceDescription&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceDescription|The operation that you want to perform. Set the value to **ModifyDBInstanceDescription**. |
|DBInstanceDescription|String|Yes|testdata|The name of the instance.

 **Note:**

-   The name cannot start with http:// or https://.
-   The name must start with a letter.
-   The name must be 2 to 256 characters in length, and can contain letters, underscores \(\_\), hyphens \(-\), and digits. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** **NodeId** also needs to be specified if you need to modify the name of a shard or mongos node in a replica set instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard or mongos node in the sharded cluster instance.

 **Note:** This parameter is valid only if you set the **DBInstanceId** parameter to the ID of a sharded cluster instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|06F8F642-4009-4FFC-80C4-9D67DBF7B74E|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceDescription
&DBInstanceDescription=testdata
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceDescriptionResponse>
	  <RequestId>06F8F642-4009-4FFC-80C4-9D67DBF7B74E</RequestId>
</ModifyDBInstanceDescriptionResponse>
```

`JSON` format

```
{
	"RequestId": "06F8F642-4009-4FFC-80C4-9D67DBF7B74E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

