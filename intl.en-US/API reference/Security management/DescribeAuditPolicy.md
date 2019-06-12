# DescribeAuditPolicy {#doc_api_Dds_DescribeAuditPolicy .reference}

You can call this operation to query whether the log audit function is enabled for a MongoDB instance.

The instance must be in the running state when you call this operation.

**Note:** This operation is applicable to replica set instances and sharded cluster instances. DescribeAuditPolicy cannot be performed on standalone instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAuditPolicy) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAuditPolicy|The operation that you want to perform. Set the value to **DescribeAuditPolicy**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LogAuditStatus|String|Enable|The status of the log audit function. Valid values:

 -   Enable
-   Disabled

 Default value: Disabled.

 |
|RequestId|String|111E7B16-0A87-4CBA-B271-F34AD61E099F|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeAuditPolicy
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeAuditPolicyResponse>
  <LogAuditStatus>Enable</LogAuditStatus>
  <RequestId>111E7B16-0A87-4CBA-B271-F34AD61E099F</RequestId>
</DescribeAuditPolicyResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"LogAuditStatus":"Enable",
	"RequestId":"111E7B16-0A87-4CBA-B271-F34AD61E099F"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

