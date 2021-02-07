# ModifyAuditLogFilter

You can call this operation to modify the type of audit logs to be collected from ApsaraDB for MongoDB instances.

-   The instance must be in the running state when you call this operation.
-   This operation is applicable to replica set instances, but cannot be performed on standalone instances and sharded cluster instances.
-   You can call this operation up to 30 times per minute. To call this operation at a higher frequency, use a Logstore. For more information, see [Manage a Logstore](~~48990~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyAuditLogFilter&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAuditLogFilter|The operation that you want to perform. Set the value to **ModifyAuditLogFilter**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|Filter|String|Yes|insert,query,update,delete|The type of the audit log entries to be collected. Valid values:

 -   **admin**: O&M and management operations
-   **slow**: slow query logs
-   **query**: query operations
-   **insert**: insert operations
-   **update**: update operations
-   **delete**: delete operations
-   **command**: protocol commands such as the aggregate method |
|RegionId|String|No|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~61933~~) operation to query the most recent region list. |
|RoleType|String|No|primary|The role of the node in the instance. Valid values:

 -   **primary**
-   **secondary** |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyAuditLogFilter
&Filter=insert,query,update,delete
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<ModifyAuditLogFilterResponse>
	  <RequestId>E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28</RequestId>
</ModifyAuditLogFilterResponse>
```

`JSON` format

```
{
	"RequestId": "E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

