# ModifyBackupPolicy {#doc_api_Dds_ModifyBackupPolicy .reference}

You can call this operation to modify the backup policy of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyBackupPolicy) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyBackupPolicy|The operation that you want to perform. Set the value to **ModifyBackupPolicy**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|PreferredBackupPeriod|String|Yes|Monday,Wednesday,Friday,Sunday|The period of backup. Valid values:

 -   **Monday** 
-   **Tuesday** 
-   **Wednesday** 
-   **Thursday** 
-   **Friday** 
-   **Saturday** 
-   **Sunday** 

 **Note:** Separate multiple values with commas \(,\).

 |
|PreferredBackupTime|String|Yes|03:00Z-04:00Z|The period when the backup is performed. The format is *HH:mm*Z-*HH:mm*Z.

 **Note:** The maximum period is 1 hour.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|644A359C-B871-4DD3-97B5-ED91EF5809C2|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyBackupPolicy
&DBInstanceId=dds-bpxxxxxxxx
&PreferredBackupPeriod=Monday,Wednesday,Friday,Sunday
&PreferredBackupTime=03:00Z-04:00Z
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyBackupPolicyResponse>
  <RequestId>644A359C-B871-4DD3-97B5-ED91EF5809C2</RequestId> 
</ModifyBackupPolicyResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"644A359C-B871-4DD3-97B5-ED91EF5809C2"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

