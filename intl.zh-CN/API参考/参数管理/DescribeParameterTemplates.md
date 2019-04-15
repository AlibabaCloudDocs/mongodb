# DescribeParameterTemplates {#doc_api_Dds_DescribeParameterTemplates .reference}

调用DescribeParameterTemplates接口查询MongoDB实例默认的参数模板列表。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeParameterTemplates)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeParameterTemplates|要执行的操作，取值：**DescribeParameterTemplates**。

 |
|Engine|String|是|mongodb|数据库引擎，取值：**mongodb**。

 |
|EngineVersion|String|是|4.0|数据库版本号，取值：**3.2**、**3.4**、**4.0**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Parameters| | |参数模板列表。

 |
|└CheckingCode|String|\[0-65536\]|参数取值范围。

 |
|└ForceModify|Boolean|true|参数是否处于可修改的状态。

 -   **false**：不可修改。
-   **true**：可修改。

 |
|└ForceRestart|Boolean|false|修改参数后是否需要重启生效。

 -   **false**：无需重启，提交后即生效。
-   **true**：需要重启生效。

 |
|└ParameterDescription|String|The threshold in milliseconds at which the database profiler considers a query slow, default is 100.|参数描述。

 |
|└ParameterName|String|operationProfiling.slowOpThresholdMs|参数名。

 |
|└ParameterValue|String|100|参数默认值。

 |
|RequestId|String|76B66D95-0670-4199-A8B1-E362286CD015|请求ID。

 |
|ParameterCount|String|5|参数个数。

 |
|EngineVersion|String|4.0|数据库版本号。

 |
|Engine|String|mongodb|数据库引擎。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeParameterTemplates
&Engine=mongodb
&EngineVersion=4.0
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeParameterTemplatesResponse>
  <Parameters>
    <TemplateRecord>
      <ForceModify>true</ForceModify>
      <ParameterDescription/>
      <ParameterValue>snappy</ParameterValue>
      <CheckingCode>snappy|zlib|disabled</CheckingCode>
      <ForceRestart>true</ForceRestart>
      <ParameterName>net.compression.compressors</ParameterName>
    </TemplateRecord>
    <TemplateRecord>
      <ForceModify>true</ForceModify>
      <ParameterDescription>The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'.</ParameterDescription>
      <ParameterValue>slowOp</ParameterValue>
      <CheckingCode>off|slowOp|all</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ParameterName>operationProfiling.mode</ParameterName>
    </TemplateRecord>
    <TemplateRecord>
      <ForceModify>true</ForceModify>
      <ParameterDescription>The threshold in milliseconds at which the database profiler considers a query slow, default is 100.</ParameterDescription>
      <ParameterValue>100</ParameterValue>
      <CheckingCode>[0-65536]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
    </TemplateRecord>
    <TemplateRecord>
      <ForceModify>true</ForceModify>
      <ParameterDescription>The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)</ParameterDescription>
      <ParameterValue>600000</ParameterValue>
      <CheckingCode>[1-2147483647]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ParameterName>setParameter.cursorTimeoutMillis</ParameterName>
    </TemplateRecord>
    <TemplateRecord>
      <ForceModify>true</ForceModify>
      <ParameterDescription>The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)</ParameterDescription>
      <ParameterValue>33554432</ParameterValue>
      <CheckingCode>[33554432-268435456]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ParameterName>setParameter.internalQueryExecMaxBlockingSortBytes</ParameterName>
    </TemplateRecord>
  </Parameters>
  <RequestId>76B66D95-0670-4199-A8B1-E362286CD015</RequestId>
  <ParameterCount>5</ParameterCount>
  <EngineVersion>4.0</EngineVersion>
  <Engine>mongodb</Engine>
</DescribeParameterTemplatesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Parameters":{
		"TemplateRecord":[
			{
				"ForceModify":true,
				"ParameterDescription":"",
				"ParameterValue":"snappy",
				"ForceRestart":true,
				"CheckingCode":"snappy|zlib|disabled",
				"ParameterName":"net.compression.compressors"
			},
			{
				"ForceModify":true,
				"ParameterDescription":"The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'.",
				"ParameterValue":"slowOp",
				"ForceRestart":false,
				"CheckingCode":"off|slowOp|all",
				"ParameterName":"operationProfiling.mode"
			},
			{
				"ForceModify":true,
				"ParameterDescription":"The threshold in milliseconds at which the database profiler considers a query slow, default is 100.",
				"ParameterValue":"100",
				"ForceRestart":false,
				"CheckingCode":"[0-65536]",
				"ParameterName":"operationProfiling.slowOpThresholdMs"
			},
			{
				"ForceModify":true,
				"ParameterDescription":"The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)",
				"ParameterValue":"600000",
				"ForceRestart":false,
				"CheckingCode":"[1-2147483647]",
				"ParameterName":"setParameter.cursorTimeoutMillis"
			},
			{
				"ForceModify":true,
				"ParameterDescription":"The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)",
				"ParameterValue":"33554432",
				"ForceRestart":false,
				"CheckingCode":"[33554432-268435456]",
				"ParameterName":"setParameter.internalQueryExecMaxBlockingSortBytes"
			}
		]
	},
	"RequestId":"76B66D95-0670-4199-A8B1-E362286CD015",
	"ParameterCount":"5",
	"EngineVersion":"4.0",
	"Engine":"mongodb"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

