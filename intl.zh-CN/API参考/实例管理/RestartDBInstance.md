# RestartDBInstance {#doc_api_Dds_RestartDBInstance .reference}

调用RestartDBInstance接口重启MongoDB实例。

调用本接口可用于重启实例，也可用于重启分片集群实例中的某个Shard节点或Mongos节点。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=RestartDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RestartDBInstance|要执行的操作，取值：**RestartDBInstance**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Shard节点ID或Mongos节点ID。

 **说明：** 当实例类型为分片集群实例时，如不传入本参数，则重启分片集群实例。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|149C517D-B586-47BE-A107-8673E0ED77C6|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=RestartDBInstance
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RestartDBInstanceResponse>
  <RequestId>149C517D-B586-47BE-A107-8673E0ED77C6</RequestId>
</RestartDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"149C517D-B586-47BE-A107-8673E0ED77C6"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

