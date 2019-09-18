# ModifyParameters {#doc_api_Dds_ModifyParameters .reference}

调用ModifyParameters接口修改MongoDB实例的参数。

调用本接口时，要求实例状态为运行中。

**警告：** 如果提交的修改参数中包含需要重启才能生效的参数，则提交后实例将自动重启。您可以通过调用[DescribeParameterTemplates](intl.zh-CN/API参考/参数管理/DescribeParameterTemplates.md#)接口查询哪些是修改后需要重启才能生效的参数。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyParameters&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyParameters|要执行的操作，取值：**ModifyParameters**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|Parameters|String|是|\{"operationProfiling.slowOpThresholdMs":"300"\}|需要修改的参数及参数的取值，格式为JSON串，例如：\{“name”:”value”,”name”:”value2”\}。

 **说明：** 您可以通过调用[DescribeParameterTemplates](~~67618~~)接口查询默认的参数模板列表。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中的Mongos节点ID或Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|36923CC2-DDAB-4B48-A144-DA92C1E19537|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyParameters
&DBInstanceId=dds-bpxxxxxxxx
&Parameters={"operationProfiling.slowOpThresholdMs":"300"}
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyParametersResponse>
	  <RequestId>36923CC2-DDAB-4B48-A144-DA92C1E19537</RequestId>
</ModifyParametersResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"36923CC2-DDAB-4B48-A144-DA92C1E19537"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

