# ModifySecurityGroupConfiguration

调用ModifySecurityGroupConfiguration更改MongoDB实例已绑定的ECS安全组。

**说明：** 如果是分片集群实例，绑定的ECS安全组仅对Mongos节点生效。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifySecurityGroupConfiguration&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifySecurityGroupConfiguration|要执行的操作，取值：**ModifySecurityGroupConfiguration**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。 |
|SecurityGroupId|String|是|sg-bpxxxxxxxx|ECS安全组ID。

 **说明：**

-   1个实例最多可以绑定10个ECS安全组。
-   您可以通过调用ECS的[DescribeSecurityGroup](~~25556~~)接口查询目标地域的安全组ID。 |
|RegionId|String|否|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|E062C482-1A4B-469E-938C-96D28CFAE42E|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=ModifySecurityGroupConfiguration
&DBInstanceId=dds-bpxxxxxxxx
&SecurityGroupId=sg-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>E062C482-1A4B-469E-938C-96D28CFAE42E</RequestId>
```

`JSON` 格式

```
{
	"RequestId": "E062C482-1A4B-469E-938C-96D28CFAE42E"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

