# DescribeAuditLogFilter

You can call this operation to view the types of audit logs collected from ApsaraDB for MongoDB instances.

-   The instance must be in the running state when you call this operation.
-   This operation is applicable to replica set instances, but cannot be performed on standalone instances and sharded cluster instances.
-   You can call this operation up to 30 times per minute. To call this operation at a higher frequency, use a Logstore. For more information, see [Manage a Logstore](~~48990~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeAuditLogFilter&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAuditLogFilter|The operation that you want to perform. Set the value to **DescribeAuditLogFilter**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RoleType|String|No|primary|The role of the node in the instance. Valid values:

 -   **primary**
-   **secondary** |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to view the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Filter|String|admin,slow,insert,query,update,delete,command|The type of the audit log entries. Valid values:

 -   **admin**: O&M and management operations
-   **slow**: slow query logs
-   **query**: query operations
-   **insert**: insert operations
-   **update**: update operations
-   **delete**: delete operations
-   **command**: protocol commands such as the aggregate method |
|RequestId|String|D7C8BA0C-9350-487D-9B70-D69AF27FB1EB|The ID of the request. |
|RoleType|String|primary|The role of the node. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeAuditLogFilter
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<DescribeAuditLogFilterResponse>
	  <Filter>admin,slow,insert,query,update,delete,command</Filter>
	  <RoleType></RoleType>
	  <RequestId>D7C8BA0C-9350-487D-9B70-D69AF27FB1EB</RequestId>
</DescribeAuditLogFilterResponse>
```

`JSON` format

```
{
	"Filter": "admin,slow,insert,query,update,delete,command",
	"RoleType": "",
	"RequestId": "D7C8BA0C-9350-487D-9B70-D69AF27FB1EB"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

