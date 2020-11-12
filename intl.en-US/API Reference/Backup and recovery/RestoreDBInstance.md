# RestoreDBInstance

You can call this operation to restore data to the current ApsaraDB for MongoDB instance.

This operation is applicable to replica set instances, but cannot be called on standalone instances or sharded cluster instances. You can use the following methods to clone an instance: [Create an instance from a backup](~~55013~~) to clone a standalone instance. Call the [CreateShardingDBInstance](~~61884~~) operation to clone a sharded cluster instance.

**Note:** This operation overwrites the data of the current instance, and the data cannot be recovered. Exercise caution when performing this operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=RestoreDBInstance&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RestoreDBInstance|The operation that you want to perform. Set the value to **RestoreDBInstance**. |
|BackupId|Integer|Yes|11111111|The ID of the backup.

**Note:** You can call the [DescribeBackups](~~62172~~) operation to query the backup ID. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of an instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|973DCB8F-56B3-4102-8777-3A90495927F7|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=RestoreDBInstance
&BackupId=11111111
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RestoreDBInstanceResponse>
      <RequestId>973DCB8F-56B3-4102-8777-3A90495927F7</RequestId>
</RestoreDBInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "973DCB8F-56B3-4102-8777-3A90495927F7"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

