# CreateRecommendationTask {#doc_api_Dds_CreateRecommendationTask .reference}

调用CreateRecommendationTask接口为MongoDB实例创建索引分析任务。

调用该接口时，实例必须满足以下条件：

-   实例的地域为华东1、华东2、华南1、华北1或华北2。
-   实例类型为副本集实例或分片集群实例。
-   实例已开通审计日志功能。

**说明：** 

-   调用本接口创建索引分析任务后，可以通过调用[DescribeAvailableTimeRange](~~95534~~)查询对应的任务及状态。
-   每个实例每日最多可执行10次。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=CreateRecommendationTask)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateRecommendationTask|要执行的操作，取值：**CreateRecommendationTask**。

 |
|StartTime|String|是|2019-01-01T12Z|查询开始时间，格式为*yyyy-MM-dd*T*HH*Z（UTC时间）。

 **说明：** **StartTime**参数取值必须晚于审计日志的开启时间。

 |
|EndTime|String|是|2019-01-01T18Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH*Z（UTC时间）。

 **说明：** 查询的时间范围为7天内。

 |
|InstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|009D2572-6839-43C0-8D89-44DB46CBA2EA|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=CreateRecommendationTask
&StartTime=2019-01-01T12Z
&EndTime=2019-01-01T18Z
&InstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateRecommendationTaskResponse>
  <RequestId>009D2572-6839-43C0-8D89-44DB46CBA2EA</RequestId>
</CreateRecommendationTaskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"009D2572-6839-43C0-8D89-44DB46CBA2EA"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidEndTime.Format|Specified end time is not valid.|输入的结束时间无效，请您检查输入的时间格式是否正确。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

