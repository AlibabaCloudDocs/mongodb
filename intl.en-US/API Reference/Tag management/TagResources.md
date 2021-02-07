# TagResources

You can call this operation to bind tags to one or more ApsaraDB for MongoDB instances.

You can create multiple tags and bind them to multiple instances. This allows you to classify and filter instances by tag.

-   A tag consists of a key and a value. Each key must be unique in a region for an Alibaba Cloud account. Different keys can have the same value.
-   If the tag you specify does not exist, this tag is automatically created and bound to the specified instance.
-   If a tag that has the same key is already bound to the instance, the new tag overwrites the existing tag.
-   You can bind up to 20 tags to each instance.
-   You can bind tags to up to 50 instances each time you call the operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=TagResources&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|TagResources|The operation that you want to perform. Set the value to **TagResources**. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|ResourceId.N|RepeatList|Yes|dds-bpxxxxxxxx|The ID of instance N.

**Note:**

N specifies the serial number of the instance. Examples:

-   **ResourceId.1** specifies the ID of the first instance.
-   **ResourceId.2** specifies the ID of the second instance. |
|ResourceType|String|Yes|INSTANCE|The resource type. Set the value to **INSTANCE**. |
|Tag.N.Key|String|Yes|Development team|The key of tag N.

**Note:**

N specifies the serial number of the tag. Examples:

-   **Tag.1.Key** specifies the key of the first tag.
-   **Tag.2.Key** specifies the key of the second tag. |
|Tag.N.Value|String|Yes|Environment 4.0|The value of tag N.

**Note:**

N specifies the serial number of the tag. Examples:

-   **Tag.1.Value** specifies the value of the first tag.
-   **Tag.2.Value** specifies the value of the second tag. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|0FDDC511-7252-4A4A-ADDA-5CB1BF63873D|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=TagResources
&RegionId=cn-hangzhou
&ResourceType=INSTANCE
&ResourceId.1=dds-bpxxxxxxxx
&ResourceId.2=dds-bpxxxxxxxx
&Tag.1.Key=Development team
&Tag1.Value=Environment 4.0
&Tag.2.Key=Service team
&Tag2.Value=Log Service
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>0FDDC511-7252-4A4A-ADDA-5CB1BF63873D</RequestId>
```

`JSON` format

```
{
    "RequestId":"0FDDC511-7252-4A4A-ADDA-5CB1BF63873D"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

