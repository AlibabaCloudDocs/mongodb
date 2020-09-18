# DescribeActiveOperationTaskType

You can call this operation to query the types of O&M tasks on an ApsaraDB for MongoDB instance and the number of each type of tasks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeActiveOperationTaskType&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeActiveOperationTaskType|The operation that you want to perform. Set the value to **DescribeActiveOperationTaskType**. |
|RegionId|String|No|cn-hangzhou|The ID of the region where the instance is deployed. You can call the [DescribeRegions](~~61933~~) operation to query the region ID. |
|IsHistory|Integer|No|0|Specifies whether to return all O&M tasks. Valid values:

-   **0**: Returns pending tasks only.
-   **1**: Returns all tasks.

Default value: **0**. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|339BFDFD-BBC0-40C1-93E0-EE691DE28B21|The ID of the request. |
|TypeList|Array| |The list of tasks. |
|Count|Integer|1|The number of pending tasks. |
|TaskType|String|rds\_apsaradb\_upgrade|The type of the task. Valid values:

-   **rds\_apsaradb\_transfer**: instance migration
-   **rds\_apsaradb\_upgrade**: minor version upgrade
-   **rds\_apsaradb\_network\_upgrade**: network upgrade |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeActiveOperationTaskType
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>CCB7F6B4-A7EA-48C0-963C-5647AC38B784</RequestId>
<TypeList>
    <Count>1</Count>
    <TaskType>rds_apsaradb_network_upgrade</TaskType>
</TypeList>
```

`JSON` format

```
{
    "RequestId": "CCB7F6B4-A7EA-48C0-963C-5647AC38B784",
    "TypeList": [{"Count": 1, "TaskType": "rds_apsaradb_network_upgrade"}]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

