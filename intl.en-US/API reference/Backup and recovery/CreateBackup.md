# CreateBackup {#doc_api_Dds_CreateBackup .reference}

You can call this operation to manually back up MongoDB instances.

The instance must be running when you call this operation.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=CreateBackup) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateBackup|The operation that you want to perform. Set the value to **CreateBackup**.

 |
|DBInstanceId|String|Yes|d-bpxxxxxxxx|The ID of the instance.

 |
|BackupMethod|String|No|Logical|The backup method of the instance. Valid values:

 -   **Logical**
-   **Physical**: This is the default value.

 **Note:** Only replica set instances and sharded cluster instances support this parameter. You do not need to specify this parameter for standalone instances. All standalone instances use snapshot backup.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|BackupId|String|5664xxxx|The ID of the backup.

 |
|RequestId|String|7016B12F-7F64-40A4-BAFF-013F02AC82FC|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=CreateBackup
DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateBackupResponse>
  <RequestId>7016B12F-7F64-40A4-BAFF-013F02AC82FC</RequestId>
  <BackupId>5664xxxx</BackupId>
</CreateBackupResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"7016B12F-7F64-40A4-BAFF-013F02AC82FC",
	"BackupId":"5664xxxx"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

