# ModifyAuditLogFilter {#doc_api_Dds_ModifyAuditLogFilter .reference}

You can call this operation to modify the type of audit logs to be collected for MongoDB instances.

The instance must be in the running state when you call this operation.

This operation is applicable to replica set instances. ModifyAuditLogFilter cannot be performed on standalone instances and sharded cluster instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyAuditLogFilter) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAuditLogFilter|The operation that you want to perform. Set the value to **ModifyAuditLogFilter**.

 |
|Filter|String|Yes|insert,query,update,delete|The type of the audit logs to be collected.

 -   **admin**: O&M and management operations
-   **slow**: slow operations
-   **query**: query operations
-   **insert**: insert operations
-   **update**: update operations
-   **delete**: delete operations
-   **command**: protocol commands such as the aggregate method

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|RoleType|String|No|primary|The role of the node in the instance. Valid values:

 -   **primary**
-   **secondary**

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyAuditLogFilter
&Filter=insert,query,update,delete
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyAuditLogFilterResponse>
  <RequestId>E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28</RequestId>
</ModifyAuditLogFilterResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

