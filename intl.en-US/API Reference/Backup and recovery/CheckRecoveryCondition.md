# CheckRecoveryCondition

You can call this operation to check whether an ApsaraDB for MongoDB instance meets the data recovery conditions.

This operation is applicable to replica set instances or sharded cluster instances.

**Note:** After you confirm that the data recovery conditions are met by calling this operation, you can call the [CreateDBInstance](~~61763~~) operation to restore data to a new instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=CheckRecoveryCondition&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CheckRecoveryCondition|The operation that you want to perform. Set the value to **CheckRecoveryCondition**. |
|SourceDBInstance|String|Yes|dds-bpxxxxxxxx|The ID of the source instance. |
|DatabaseNames|String|No|\["db1","db2"\]|The name of the source database. The value is a JSON array.

**Note:** If you do not specify this parameter, all databases are restored. |
|RestoreTime|String|No|2019-08-22T08:00:00Z|The point in time to which the instance is restored. Specify the time in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

**Note:**

-   The value can be any time within the past seven days. The time must be earlier than the current time, but later than the time when the instance was created.
-   You must specify one of the RestoreTime and **BackupId** parameters. |
|BackupId|String|No|5664xxxx|The ID of the backup.

**Note:**

-   You can call the [DescribeBackups](~~62172~~) operation to query the ID of the backup.
-   You must specify one of the **RestoreTime** and BackupId parameters.
-   This parameter is not applicable to sharded cluster instances. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsValid|Boolean|true|Indicates whether the recovery conditions are met. Valid values:

-   **true**: The recovery conditions are met.
-   **false**: The recovery conditions are not met. |
|RequestId|String|D563A3E7-6010-45FE-A0CD-9283414C9657|The ID of the request. |
|DBInstanceName|String|dds-bpxxxxxxxx|The ID of the instance. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=CheckRecoveryCondition
&SourceDBInstance=dds-bpxxxxxxxx
&RestoreTime=2019-08-22T08:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CheckRecoveryConditionResponse>
      <IsValid>true</IsValid>
      <RequestId>D563A3E7-6010-45FE-A0CD-9283414C9657</RequestId>
      <DBInstanceName>dds-bpxxxxxxxx</DBInstanceName>
</CheckRecoveryConditionResponse>
```

`JSON` format

```
{
    "IsValid": true,
    "RequestId": "D563A3E7-6010-45FE-A0CD-9283414C9657",
    "DBInstanceName": "dds-bpxxxxxxxx"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectDBInstanceType|Current DB instance type does not support this operation.|The error message returned because the operation is not supported by the current instance type.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

