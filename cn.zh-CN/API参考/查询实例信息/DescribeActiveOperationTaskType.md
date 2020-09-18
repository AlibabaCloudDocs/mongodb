# DescribeActiveOperationTaskType

调用DescribeActiveOperationTaskType接口查询MongoDB实例的运维任务类型以及各类型的任务数量。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeActiveOperationTaskType&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeActiveOperationTaskType|要执行的操作，取值：**DescribeActiveOperationTaskType**。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |
|IsHistory|Integer|否|0|是否返回历史运维任务。取值：

 -   **0**：仅返回当前待处理的运维任务。
-   **1**：返回历史运维任务。

 默认值：**0**。 |
|ResourceGroupId|String|否|sg-bpxxxxxxxxxxxxxxxxxx|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|339BFDFD-BBC0-40C1-93E0-EE691DE28B21|请求ID。 |
|TypeList|Array of Items| |任务列表。 |
|Count|Integer|1|待处理的任务数量。 |
|TaskType|String|rds\_apsaradb\_upgrade|任务的类型。返回值：

 -   **rds\_apsaradb\_transfer**：实例迁移
-   **rds\_apsaradb\_upgrade**：小版本升级
-   **rds\_apsaradb\_network\_upgrade**：网络升级 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeActiveOperationTaskType
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>CCB7F6B4-A7EA-48C0-963C-5647AC38B784</RequestId>
<TypeList>
    <Count>1</Count>
    <TaskType>rds_apsaradb_network_upgrade</TaskType>
</TypeList>
```

`JSON` 格式

```
{
    "RequestId": "CCB7F6B4-A7EA-48C0-963C-5647AC38B784",
    "TypeList": [{"Count": 1, "TaskType": "rds_apsaradb_network_upgrade"}]
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

