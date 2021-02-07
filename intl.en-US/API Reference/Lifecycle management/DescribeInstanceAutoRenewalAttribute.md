# DescribeInstanceAutoRenewalAttribute

You can call this operation to query whether auto-renewal is enabled for an ApsaraDB for MongoDB instance.

This operation is applicable to subscription instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeInstanceAutoRenewalAttribute&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstanceAutoRenewalAttribute|The operation that you want to perform. Set the value to **DescribeInstanceAutoRenewalAttribute**. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|DBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the instance. |
|DBInstanceType|String|No|replicate|The category of the instance. Valid values:

 -   **replicate**: the standalone or replica set instance
-   **sharding**: the sharded cluster instance

 Default value: **replicate**. |
|PageSize|String|No|30|The number of entries to return on each page. Valid values: **30**, **50**, and **100**.

 **Note:** Default value: **30**. |
|PageNumber|String|No|1|The number of the page to return. The value must be a positive integer that does not exceed the maximum value of the Integer parameter. Default value: **1**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items|Array| |Details about returned entries. |
|Item| | | |
|AutoRenew|String|true|Indicates whether auto-renewal is enabled for the instance. Valid values:

 -   **true**: Auto-renewal is enabled for the instance.
-   **false**: Auto-renewal is disabled for the instance. |
|DBInstanceType|String|replicate|The category of the instance. Valid values:

 -   **replicate**: the standalone or replica set instance
-   **sharding**: the sharded cluster instance |
|DbInstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|Duration|String|1|The auto-renewal period. Unit: months.

 **Note:**

-   This parameter is ruturned only when the returned value of the **AutoRenew** parameter is **true**.
-   You can call the [ModifyInstanceAutoRenewalAttribute](~~145979~~) operation to modify the auto-renewal period. |
|RegionId|String|cn-hangzhou|The region ID of the instance. |
|ItemsNumbers|Integer|2|The total number of entries returned. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|2|The number of entries that were returned on the current page. |
|RequestId|String|FAB5CB3B-DB9D-473A-9DF1-F57B6B9CB949|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeInstanceAutoRenewalAttribute
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstanceAutoRenewalAttributeResponse>
	  <Items>
		    <Item>
			      <DBInstanceType>replicate</DBInstanceType>
			      <RegionId>cn-hangzhou</RegionId>
			      <DbInstanceId>dds-bpxxxxxxxx</DbInstanceId>
			      <AutoRenew>false</AutoRenew>
		    </Item>
		    <Item>
			      <DBInstanceType>replicate</DBInstanceType>
			      <Duration>1</Duration>
			      <RegionId>cn-hangzhou</RegionId>
			      <DbInstanceId>dds-bpxxxxxxxx</DbInstanceId>
			      <AutoRenew>true</AutoRenew>
		    </Item>
	  </Items>
	  <PageNumber>1</PageNumber>
	  <RequestId>FAB5CB3B-DB9D-473A-9DF1-F57B6B9CB949</RequestId>
	  <ItemsNumbers>2</ItemsNumbers>
	  <PageRecordCount>2</PageRecordCount>
</DescribeInstanceAutoRenewalAttributeResponse>
```

`JSON` format

```
{
	"Items": {
		"Item": [
			{
				"DBInstanceType": "replicate",
				"RegionId": "cn-hangzhou",
				"DbInstanceId": "dds-bpxxxxxxxx",
				"AutoRenew": "false"
			},
			{
				"DBInstanceType": "replicate",
				"Duration": 1,
				"RegionId": "cn-hangzhou",
				"DbInstanceId": "dds-bpxxxxxxxx",
				"AutoRenew": "true"
			}
		]
	},
	"PageNumber": 1,
	"RequestId": "FAB5CB3B-DB9D-473A-9DF1-F57B6B9CB949",
	"ItemsNumbers": 2,
	"PageRecordCount": 2
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

