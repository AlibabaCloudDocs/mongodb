# DescribeActiveOperationTaskCount

You can call this operation to query the number of O&M tasks on an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeActiveOperationTaskCount&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeActiveOperationTaskCount|The operation that you want to perform. Set the value to **DescribeActiveOperationTaskCount**. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NeedPop|Integer|0|Indicates whether any O&M tasks need pop-up windows to notify users actions. Valid values:

-   **0**: No O&M tasks need pop-up windows to notify users actions.
-   **1**: Some O&M tasks need pop-up windows to notify users actions. |
|RequestId|String|770D7F11-21A2-402B-9DF6-D1A620570EF9|The ID of the request. |
|TaskCount|Integer|0|The number of pending O&M tasks. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeActiveOperationTaskCount
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>770D7F11-21A2-402B-9DF6-D1A620570EF9</RequestId>
<NeedPop>0</NeedPop>
<TaskCount>0</TaskCount>
```

`JSON` format

```
{
    "RequestId": "770D7F11-21A2-402B-9DF6-D1A620570EF9",
    "NeedPop": 0,
    "TaskCount": 0
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

