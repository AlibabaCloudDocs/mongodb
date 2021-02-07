# CreateBackup

You can call this operation to manually back up an ApsaraDB for MongoDB instance.

The instance must be in the running state when you call this operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=CreateBackup&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateBackup|The operation that you want to perform. Set the value to **CreateBackup**. |
|DBInstanceId|String|Yes|d-bpxxxxxxxx|The ID of the instance. |
|BackupMethod|String|No|Logical|The backup method of the instance. Default value: Physical. Valid values:

 -   **Logical**
-   **Physical**

 **Note:** Only replica set instances and sharded cluster instances support this parameter. You do not need to specify this parameter for standalone instances. All standalone instances use snapshot backup. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BackupId|String|5664xxxx|The ID of the backup set. |
|RequestId|String|7016B12F-7F64-40A4-BAFF-013F02AC82FC|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=CreateBackup
DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateBackupResponse>
	  <RequestId>7016B12F-7F64-40A4-BAFF-013F02AC82FC</RequestId>
	  <BackupId>5664xxxx</BackupId>
</CreateBackupResponse>
```

`JSON` format

```
{
    "RequestId": "7016B12F-7F64-40A4-BAFF-013F02AC82FC",
    "BackupId": "5664xxxx"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

