# DeleteDBInstance

调用DeleteDBInstance接口释放MongoDB实例。

调用该接口时，实例必须满足以下条件。

-   实例状态为运行中；
-   实例付费类型为按量付费。

**说明：** 实例释放后数据将无法找回，请谨慎操作。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DeleteDBInstance&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteDBInstance|要执行的操作，取值**DeleteDBInstance**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|72651AF9-7897-41A7-8B67-6C15C7F26A0A|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DeleteDBInstance
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteDBInstanceResponse>
	  <RequestId>72651AF9-7897-41A7-8B67-6C15C7F26A0A</RequestId>
</DeleteDBInstanceResponse>
```

`JSON` 格式

```
{
	"RequestId": "72651AF9-7897-41A7-8B67-6C15C7F26A0A"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

