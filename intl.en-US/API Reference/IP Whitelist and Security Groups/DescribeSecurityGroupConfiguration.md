# DescribeSecurityGroupConfiguration

You can call this operation to query ECS security groups that are bound to an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeSecurityGroupConfiguration&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSecurityGroupConfiguration|The operation that you want to perform. Set the value to **DescribeSecurityGroupConfiguration**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items|Array| |Details about the ECS security groups. |
|RdsEcsSecurityGroupRel| | | |
|NetType|String|vpc|The network type of the ECS security group. Valid values:

 -   **vpc**
-   **classic** |
|RegionId|String|cn-hangzhou|The region ID of the ECS security group. |
|SecurityGroupId|String|sg-bpxxxxxxxx|The ID of the ECS security group. |
|RequestId|String|3C4A2494-85C4-45C5-93CF-548DB3375193|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeSecurityGroupConfiguration
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<Items>
    <RdsEcsSecurityGroupRel>
        <SecurityGroupId>sg-bpxxxxxxxx</SecurityGroupId>
        <RegionId>cn-hangzhou</RegionId>
        <NetType>classic</NetType>
    </RdsEcsSecurityGroupRel>
</Items>
<RequestId>D18F5B88-ACA6-470E-9493-384412EDD902</RequestId>
```

`JSON` format

```
{
	"Items": {
		"RdsEcsSecurityGroupRel": [
			{
				"SecurityGroupId": "sg-bpxxxxxxxx",
				"RegionId": "cn-hangzhou",
				"NetType": "classic"
			}
		]
	},
	"RequestId": "D18F5B88-ACA6-470E-9493-384412EDD902"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

