# CheckCloudResourceAuthorized

调用CheckCloudResourceAuthorized接口查询KMS密钥是否已授权给MongoDB实例。

在调用[ModifyDBInstanceTDE](~~131267~~)接口开启透明数据加密TDE前，请调用本接口查询KMS密钥是否已授权给MongoDB实例。

如果未授权则无法开启MongoDB实例的透明数据加密TDE功能，您可以[提交工单](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex)修改授权信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=CheckCloudResourceAuthorized&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CheckCloudResourceAuthorized|要执行的操作，取值：**CheckCloudResourceAuthorized**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。 |
|TargetRegionId|String|是|cn-hangzhou|实例所属地域，您可以调用[DescribeDBInstanceAttribute](~~62010~~)查询。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A0181AC4-F186-46ED-87CA-100C70B86729|请求ID。 |
|AuthorizationState|Integer|1|授权状态，返回值为：

 -   **0**：未授权。
-   **1**：已授权。
-   **2**：用户未开启KMS。 |
|RoleArn|String|acs:ram::140xxxxxxxx:role/aliyunrdsinstanceencryptiondefaultrole|已授权阿里云资源的角色信息。

 **说明：** 当**AuthorizationState**返回值为**1**时，才会返回本参数。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=CheckCloudResourceAuthorized
&DBInstanceId=dds-bpxxxxxxxx
&TargetRegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>A0181AC4-F186-46ED-87CA-100C70B86729</RequestId>
<AuthorizationState>1</AuthorizationState>
<RoleArn>acs:ram::140xxxxxxxx:role/aliyunrdsinstanceencryptiondefaultrole</RoleArn>
```

`JSON` 格式

```
{
	"RequestId": "A0181AC4-F186-46ED-87CA-100C70B86729",
	"AuthorizationState": 1,
	"RoleArn": "acs:ram::140xxxxxxxx:role/aliyunrdsinstanceencryptiondefaultrole"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

