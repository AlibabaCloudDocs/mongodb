# DescribeActiveOperationTaskCount

调用DescribeActiveOperationTaskCount接口查询MongoDB实例的运维任务数量。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeActiveOperationTaskCount&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeActiveOperationTaskCount|要执行的操作，取值：**DescribeActiveOperationTaskCount**。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |
|ResourceGroupId|String|否|sg-bpxxxxxxxxxxxxxxxxxx|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NeedPop|Integer|0|是否有需要弹窗通知用户操作的运维任务。返回值：

 -   **0**：无弹窗
-   **1**：有弹窗 |
|RequestId|String|770D7F11-21A2-402B-9DF6-D1A620570EF9|请求ID。 |
|TaskCount|Integer|0|待处理的运维任务数。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeActiveOperationTaskCount
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>770D7F11-21A2-402B-9DF6-D1A620570EF9</RequestId>
<NeedPop>0</NeedPop>
<TaskCount>0</TaskCount>
```

`JSON` 格式

```
{
	"RequestId": "770D7F11-21A2-402B-9DF6-D1A620570EF9",
	"NeedPop": 0,
	"TaskCount": 0
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

