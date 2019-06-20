# DescribeBackupPolicy {#doc_api_Dds_DescribeBackupPolicy .reference}

You can call this operation to query the backup policy of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeBackupPolicy) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeBackupPolicy|The operation that you want to perform. Set the value to **DescribeBackupPolicy**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BackupRetentionPeriod|String|7|The backup retention period. Unit: days.

 |
|PreferredBackupPeriod|String|Monday,Wednesday,Friday,Sunday|The period of backup. Valid values:

 -   **Monday** 
-   **Tuesday** 
-   **Thursday** 
-   **Friday** 
-   **Saturday** 
-   **Sunday** 

 |
|PreferredBackupTime|String|20:00Z-21:00Z|The period when the backup is performed. The format is *HH:mm*Z-*HH:mm*Z.

 |
|RequestId|String|C2C283A1-1CC4-4DD9-B985-3811E0244A45|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeBackupPolicy
DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeBackupPolicyResponse>
  <PreferredBackupPeriod>Monday,Wednesday,Friday,Sunday</PreferredBackupPeriod>
  <RequestId>C2C283A1-1CC4-4DD9-B985-3811E0244A45</RequestId>
  <PreferredBackupTime>20:00Z-21:00Z</PreferredBackupTime>
  <BackupRetentionPeriod>7</BackupRetentionPeriod>
</DescribeBackupPolicyResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"PreferredBackupPeriod":"Monday,Wednesday,Friday,Sunday",
	"RequestId":"C2C283A1-1CC4-4DD9-B985-3811E0244A45",
	"BackupRetentionPeriod":"7",
	"PreferredBackupTime":"20:00Z-21:00Z"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

