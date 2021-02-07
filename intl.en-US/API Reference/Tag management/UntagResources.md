# UntagResources

You can call this operation to unbind tags from an instance. If an unbound tag is not bound to another instance, the tag is deleted.

**Note:**

-   You can unbind up to 20 tags at a time.
-   When a tag is unbound from all instances, the tag is automatically deleted.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=UntagResources&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UntagResources|The operation that you want to perform. Set the value to **UntagResources**. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|ResourceId.N|RepeatList|Yes|dds-bpxxxxxxxx|The ID of instance N.

 **Note:** **N** specifies the serial number of the instance. For example, **ResourceId.1** specifies the ID of the first instance and **ResourceId.2** specifies the ID of the second instance. |
|ResourceType|String|Yes|INSTANCE|The resource type. Set the value to **INSTANCE**. |
|TagKey.N|RepeatList|No|Development team|The key of tag N.

 **Note:** **N** specifies the serial number of the tag. For example, **TagKey.1** specifies the key of the first tag and **TagKey.2** specifies the key of the second tag. |
|All|Boolean|No|false|Specifies whether to unbind all tags from the instance. Valid values:

 -   **true**
-   **false**

 **Note:**

-   Default value: **false**.
-   If you specify both this parameter and **TagKey.N**, this parameter is invalid. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|FA3A7F36-DB57-4281-8935-4B9DF61554EB|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=UntagResources
&RegionId=cn-hangzhou
&ResourceType=INSTANCE
&ResourceId.1=dds-bpxxxxxxxx
&TagKey.1=Development team
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>FA3A7F36-DB57-4281-8935-4B9DF61554EB</RequestId>
```

`JSON` format

```
{
	"RequestId": "FA3A7F36-DB57-4281-8935-4B9DF61554EB"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

