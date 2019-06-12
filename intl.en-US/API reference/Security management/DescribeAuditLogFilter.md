# DescribeAuditLogFilter {#doc_api_Dds_DescribeAuditLogFilter .reference}

You can call this operation to query the types of audit logs collected from MongoDB instances.

The instance must be in the running state when you call this operation.

**Note:** This operation is applicable to replica set instances. DescribeAuditLogFilter cannot be performed on standalone instances and sharded cluster instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAuditLogFilter) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAuditLogFilter|The operation that you want to perform. Set the value to **DescribeAuditLogFilter**.

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
|Filter|String|admin,slow,insert,query,update,delete,command|The operation log types of the database. The types are as follows:

 -   **admin**: O&M and management operations
-   **slow**: slow operations
-   **query**: query operations
-   **insert**: insert operations
-   **update**: update operations
-   **delete**: delete operations
-   **command**: protocol commands such as the aggregate method

 |
|RequestId|String|D7C8BA0C-9350-487D-9B70-D69AF27FB1EB|The ID of the request.

 |
|RoleType|String|primary|The role of the node.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeAuditLogFilter
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeAuditLogFilterResponse>
  <Filter>admin,slow,insert,query,update,delete,command</Filter>
  <RoleType/>
  <RequestId>D7C8BA0C-9350-487D-9B70-D69AF27FB1EB</RequestId>
</DescribeAuditLogFilterResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"Filter":"admin,slow,insert,query,update,delete,command",
	"RequestId":"D7C8BA0C-9350-487D-9B70-D69AF27FB1EB",
	"RoleType":""
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

