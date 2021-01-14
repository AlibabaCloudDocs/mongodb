# DescribeInstanceAutoRenewalAttribute

调用DescribeInstanceAutoRenewalAttribute接口查询MongoDB实例是否为自动付费。

本接口适用于包年包月付费类型的实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeInstanceAutoRenewalAttribute&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInstanceAutoRenewalAttribute|要执行的操作，取值：**DescribeInstanceAutoRenewalAttribute**。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。 |
|DBInstanceId|String|否|dds-bpxxxxxxxx|实例ID。 |
|DBInstanceType|String|否|replicate|实例类型，取值：

 -   **replicate**：单节点或副本集实例。
-   **sharding**：分片集群实例。

 默认值为**replicate**。 |
|PageSize|String|否|30|每页记录数，取值：**30**、**50**或**100**。

 **说明：** 默认值为**30**。 |
|PageNumber|String|否|1|页码，取值为大于0且不超过Integer数据类型的最大值，默认值为**1**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Items|Array| |查询结果列表。 |
|Item| | | |
|AutoRenew|String|true|自动续费状态，返回值为：

 -   **true**：已开启自动续费。
-   **false**：未开启自动续费。 |
|DBInstanceType|String|replicate|实例类型，返回值为：

 -   **replicate**：单节点或副本集实例。
-   **sharding**：分片集群实例。 |
|DbInstanceId|String|dds-bpxxxxxxxx|实例ID。 |
|Duration|String|1|自动续费的续费周期，单位为月。

 **说明：**

-   当**AutoRenew**参数的返回值为**true**时，才会返回本参数。
-   您可以调用[ModifyInstanceAutoRenewalAttribute](~~145979~~)接口，修改自动续费的周期。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|ItemsNumbers|Integer|2|查询结果总数。 |
|PageNumber|Integer|1|页码。 |
|PageRecordCount|Integer|2|当前页显示的记录数。 |
|RequestId|String|FAB5CB3B-DB9D-473A-9DF1-F57B6B9CB949|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeInstanceAutoRenewalAttribute
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

