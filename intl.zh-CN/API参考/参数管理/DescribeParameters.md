# DescribeParameters {#doc_api_Dds_DescribeParameters .reference}

调用DescribeParameters接口查询MongoDB实例的参数配置信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeParameters)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeParameters|要执行的操作，取值：**DescribeParameters**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中的Mongos节点ID或Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ConfigParameters| | |配置中的的参数配置信息列表。

 |
|└CheckingCode|String|\[0-65536\]|参数取值范围。

 |
|└ForceRestart|Boolean|true|修改参数后是否需要重启生效。

 -   **flase**：无需重启，提交后即生效。
-   **true**：需要重启生效。

 |
|└ModifiableStatus|Boolean|true|参数是否处于可修改的状态。

 -   **flase**：不可修改。
-   **true**：可修改。

 |
|└ParameterDescription|String|The threshold in milliseconds at which the database profiler considers a query slow, default is 100.|参数描述。

 |
|└ParameterName|String|operationProfiling.slowOpThresholdMs|参数名。

 |
|└ParameterValue|String|200|参数值。

 |
|RequestId|String|3ADD0C7D-2D2A-4F15-88FF-E7AC9B9FDCC8|请求ID。

 |
|RunningParameters| | |当前运行的参数配置信息列表。

 |
|└CheckingCode|String|\[33554432-268435456\]|参数取值范围。

 |
|└ForceRestart|Boolean|false|修改参数后是否需要重启生效。

 -   **flase**：无需重启，提交后即生效。
-   **true**：需要重启生效。

 |
|└ModifiableStatus|Boolean|true|参数是否处于可修改的状态。

 -   **flase**：不可修改。
-   **true**：可修改。

 |
|└ParameterDescription|String|The maximum memory bytes that sort stage may use, default is 33554432\(i.e. 32MB\)|参数描述。

 |
|└ParameterName|String|setParameter.internalQueryExecMaxBlockingSortBytes|参数名。

 |
|└ParameterValue|String|33554432|参数值。

 |
|EngineVersion|String|4.0|数据库版本号。

 |
|Engine|String|mongodb|数据库引擎，默认返回**mongodb**。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeParameters
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeParametersResponse>
  <ConfigParameters>
    <Parameter>
      <ParameterDescription>The threshold in milliseconds at which the database profiler considers a query slow, default is 100.</ParameterDescription>
      <ParameterValue>200</ParameterValue>
      <CheckingCode>[0-65536]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
    </Parameter>
  </ConfigParameters>
  <RequestId>3ADD0C7D-2D2A-4F15-88FF-E7AC9B9FDCC8</RequestId>
  <RunningParameters>
    <Parameter>
      <ParameterDescription/>
      <ParameterValue>zlib</ParameterValue>
      <CheckingCode>snappy|zlib|disabled</CheckingCode>
      <ForceRestart>true</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>net.compression.compressors</ParameterName>
    </Parameter>
    <Parameter>
      <ParameterDescription>The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'.</ParameterDescription>
      <ParameterValue>slowOp</ParameterValue>
      <CheckingCode>off|slowOp|all</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>operationProfiling.mode</ParameterName>
    </Parameter>
    <Parameter>
      <ParameterDescription>The threshold in milliseconds at which the database profiler considers a query slow, default is 100.</ParameterDescription>
      <ParameterValue>220</ParameterValue>
      <CheckingCode>[0-65536]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
    </Parameter>
    <Parameter>
      <ParameterDescription>The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)</ParameterDescription>
      <ParameterValue>600000</ParameterValue>
      <CheckingCode>[1-2147483647]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>setParameter.cursorTimeoutMillis</ParameterName>
    </Parameter>
    <Parameter>
      <ParameterDescription>The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)</ParameterDescription>
      <ParameterValue>33554432</ParameterValue>
      <CheckingCode>[33554432-268435456]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>setParameter.internalQueryExecMaxBlockingSortBytes</ParameterName>
    </Parameter>
  </RunningParameters>
  <EngineVersion>4.0</EngineVersion>
  <Engine>mongodb</Engine>
</DescribeParametersResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ConfigParameters":{
		"Parameter":[
			{
				"ParameterDescription":"The threshold in milliseconds at which the database profiler considers a query slow, default is 100.",
				"ParameterValue":"200",
				"ForceRestart":false,
				"CheckingCode":"[0-65536]",
				"ModifiableStatus":true,
				"ParameterName":"operationProfiling.slowOpThresholdMs"
			}
		]
	},
	"RequestId":"3ADD0C7D-2D2A-4F15-88FF-E7AC9B9FDCC8",
	"RunningParameters":{
		"Parameter":[
			{
				"ParameterDescription":"",
				"ParameterValue":"zlib",
				"ForceRestart":"true",
				"CheckingCode":"snappy|zlib|disabled",
				"ModifiableStatus":"true",
				"ParameterName":"net.compression.compressors"
			},
			{
				"ParameterDescription":"The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'.",
				"ParameterValue":"slowOp",
				"ForceRestart":"false",
				"CheckingCode":"off|slowOp|all",
				"ModifiableStatus":"true",
				"ParameterName":"operationProfiling.mode"
			},
			{
				"ParameterDescription":"The threshold in milliseconds at which the database profiler considers a query slow, default is 100.",
				"ParameterValue":"220",
				"ForceRestart":"false",
				"CheckingCode":"[0-65536]",
				"ModifiableStatus":"true",
				"ParameterName":"operationProfiling.slowOpThresholdMs"
			},
			{
				"ParameterDescription":"The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)",
				"ParameterValue":"600000",
				"ForceRestart":"false",
				"CheckingCode":"[1-2147483647]",
				"ModifiableStatus":"true",
				"ParameterName":"setParameter.cursorTimeoutMillis"
			},
			{
				"ParameterDescription":"The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)",
				"ParameterValue":"33554432",
				"ForceRestart":"false",
				"CheckingCode":"[33554432-268435456]",
				"ModifiableStatus":"true",
				"ParameterName":"setParameter.internalQueryExecMaxBlockingSortBytes"
			}
		]
	},
	"EngineVersion":"4.0",
	"Engine":"mongodb"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDBInstanceClass.NotFound|Specified DB instance class is not found.|该实例规格不存在，请您检查输入的参数是否正确。|
|403|IncorrectDBInstanceType|Current DB instance type does not support this operation.|当前的实例类型不支持此操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

