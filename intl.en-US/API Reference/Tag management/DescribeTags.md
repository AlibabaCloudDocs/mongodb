# DescribeTags

You can call this operation to query all tags in a specified region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeTags&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeTags|The operation that you want to perform. Set the value to **DescribeTags**. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|ResourceType|String|No|INSTANCE|The resource type. Set the value to **INSTANCE**. |
|NextToken|String|No|212db86xxxxxxxx|The start token for the next query, which is used to return more results.

**Note:** This parameter is not required in the first query. If not all results are returned in one query, you can pass in the **NextToken** value returned in the previous query to perform query again. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|212db86xxxxxxxx|The token that was returned for the next query.

**Note:** If not all results are returned in the first query, this parameter is returned. You can pass in the returned value of this parameter in the next query. |
|Tags|Array of Tag| |Details about the tags. |
|TagKey|String|Development team|The key of the tag. |
|TagValues|List|Environment 4.0|The value of the tag. |
|RequestId|String|EEDBE38F-5CF5-4316-AAC2-35817BA60D68|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeTags
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<Tags>
    <TagKey>Development team</TagKey>
    <TagValues>Environment 3.4</TagValues>
    <TagValues>Environment 4.0</TagValues>
</Tags>
<Tags>
    <TagKey>Service team</TagKey>
    <TagValues>Log Service</TagValues>
</Tags>
<RequestId>EEDBE38F-5CF5-4316-AAC2-35817BA60D68</RequestId>
```

`JSON` format

```
{
    "Tags": [
        {
            "TagKey": "Development team",
            "TagValues": [
                "Environment 3.4",
                "Environment 4.0"
            ]
        },
        {
            "TagKey": "Service team",
            "TagValues": [
                "Log Service"
            ]
        }
    ],
    "RequestId": "EEDBE38F-5CF5-4316-AAC2-35817BA60D68"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

