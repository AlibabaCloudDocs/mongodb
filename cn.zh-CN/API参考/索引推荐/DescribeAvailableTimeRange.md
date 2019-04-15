# DescribeAvailableTimeRange {#doc_api_Dds_DescribeAvailableTimeRange .reference}

调用DescribeAvailableTimeRange接口查询MongoDB实例索引分析报告的分析时间段和生成状态。

调用本接口时，实例必须满足以下条件：

-   实例的地域为华东1、华东2、华南1、华北1或华北2。
-   实例类型为副本集实例或分片集群实例。
-   实例必须先开通审计日志功能。

**说明：** 您可以通过调用[CreateRecommendationTask](~~95527~~)接口创建7天内任意时间段（精确到小时）内的在线分析任务。分析完成后，自动将结果转换为可查询数据。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAvailableTimeRange)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAvailableTimeRange|要执行的操作，取值：**DescribeAvailableTimeRange**。

 |
|InstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|TimeRange| | |可用的时间范围内，索引报告生成状态。

 |
|└EndTime|String|2019-03-12T16Z|查询结束时间，格式为*yyyy-MM-dd*T*HH*Z。

 |
|└NodeId|String|d-bpxxxxxxxx|分片集群实例中Shard节点ID。

 **说明：** 当实例类型为分片集群实例时，返回本参数。

 |
|└StartTime|String|2019-03-11T16Z|查询开始时间，格式为*yyyy-MM-dd*T*HH*Z。

 |
|└Status|String|Success|索引推荐报告的生成状态。

 -   **Success**：生成成功。
-   **Creating**：生成中。
-   **Failure**：生成失败。

 |
|└TaskId|String|3223xxxx|任务ID。

 |
|RequestId|String|5C344679-EDD7-4BC1-964B-DDE01C507BE5|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeAvailableTimeRange
&InstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAvailableTimeRangeResponse>
  <TimeRange>
    <TimeRange>
      <Status>Success</Status>
      <EndTime>2019-03-12T16Z</EndTime>
      <TaskId>3223xxxx</TaskId>
      <StartTime>2019-03-11T16Z</StartTime>
    </TimeRange>
  </TimeRange>
  <RequestId>5C344679-EDD7-4BC1-964B-DDE01C507BE5</RequestId>
</DescribeAvailableTimeRangeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TimeRange":{
		"TimeRange":[
			{
				"Status":"Success",
				"EndTime":"2019-03-12T16Z",
				"StartTime":"2019-03-11T16Z",
				"TaskId":"3223xxxx"
			}
		]
	},
	"RequestId":"5C344679-EDD7-4BC1-964B-DDE01C507BE5"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

