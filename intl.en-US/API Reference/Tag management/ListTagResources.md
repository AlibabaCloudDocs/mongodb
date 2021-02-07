# ListTagResources

You can call this operation to query the binding relationship between ApsaraDB for MongoDB instances and tags.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ListTagResources&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagResources|The operation that you want to perform. Set the value to **ListTagResources**. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|ResourceType|String|Yes|INSTANCE|The type of resource. Set the value to **INSTANCE**. |
|ResourceId.N|RepeatList|No|dds-bpxxxxxxxx|The ID of the instance.

 **Note:**

-   **N** specifies the nth instance. For example, **ResourceId.1** indicates the ID of the first instance and **ResourceId.2** indicates the ID of the second instance.
-   You must specify either this parameter or **Tag.N.Key**. |
|NextToken|String|No|212db86xxxxxxxx|The start Token for the next query. It is used to return more results.

 **Note:** This parameter is not required in the first query. If not all results are returned in one query, you can input the **NextToken** returned in the previous query to query again. |
|Tag.N.Key|String|No|Development team|The key of the tag.

 **Note:**

-   **N** specifies the serial number of the tag. For example, **Tag.1.Key** indicates the key of the first tag. **Tag.2.Key** indicates the key of the second tag.
-   You must specify either this parameter or **ResourceId.N**. |
|Tag.N.Value|String|No|Environment 4.0|The value of the tag.

 **Note:** **N** specifies the serial number of the tag. For example, **Tag.1.Value** indicates the value of the first tag. **Tag.2.Value** indicates the value of the second tag. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|212db86xxxxxxxx|The start Token for the next query.

 **Note:** If not all results are returned in the first query, this parameter is returned. You can input the returned value of this parameter in the next query. |
|TagResources|Array| |An array that consists of the information of the tags of the instance. |
|TagResource| | | |
|ResourceId|String|dds-bpxxxxxxxx|The ID of the resource. It is the ID of the ApsaraDB for MongoDB instance. |
|ResourceType|String|ALIYUN::DDS::INSTANCE|The type of resource. The return value is fixed to **ALIYUN: KVSTORE: INSTANCE**, indicating an ApsaraDB for MongoDB instance. |
|TagKey|String|Development team|The key of the tag. |
|TagValue|String|Environment 4.0|The value of the tag. |
|RequestId|String|96017AF2-9AB1-4BC9-88D2-7966B3CD068F|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=TagResources
&RegionId=cn-hangzhou
&ResourceType=INSTANCE
&Tag.1.Key=Development team
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TagResources>
    <TagResource>
        <ResourceType>ALIYUN::DDS::INSTANCE</ResourceType>
        <TagValue>Environment 4.0</TagValue>
        <ResourceId>dds-bpxxxxxxxx</ResourceId>
        <TagKey>Development team</TagKey>
    </TagResource>
    <TagResource>
        <ResourceType>ALIYUN::DDS::INSTANCE</ResourceType>
        <TagValue>Environment 3.4</TagValue>
        <ResourceId>dds-bpxxxxxxxx</ResourceId>
        <TagKey>Development team</TagKey>
    </TagResource>
</TagResources>
<RequestId>96017AF2-9AB1-4BC9-88D2-7966B3CD068F</RequestId>
```

`JSON` format

```
{
	"TagResources": {
		"TagResource": [
			{
				"ResourceType": "ALIYUN::DDS::INSTANCE",
				"TagValue":"Environment 4.0",
				"ResourceId": "dds-bpxxxxxxxx",
				"TagKey": "Development team",
			},
			{
				"ResourceType": "ALIYUN::DDS::INSTANCE",
				"TagValue":"Environment 3.4",
				"ResourceId": "dds-bpxxxxxxxx",
				"TagKey": "Development team",
			}
		]
	},
	"RequestId": "96017AF2-9AB1-4BC9-88D2-7966B3CD068F"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

