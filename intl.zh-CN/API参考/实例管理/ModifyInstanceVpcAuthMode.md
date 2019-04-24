# ModifyInstanceVpcAuthMode {#doc_api_Dds_ModifyInstanceVpcAuthMode .reference}

调用ModifyInstanceVpcAuthMode接口开启或关闭MongoDB实例的专有网络免密访问功能。

调用本接口时，实例必须满足以下条件：

-   实例的类型为副本集实例或分片集群实例。
-   实例的数据库版本为4.0版本，数据库小版本为mongodb\_20190408\_3.0.11及以上版本，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)接口查看版本信息。如果版本过低请调用[UpgradeDBInstanceEngineVersion](~~67608~~)接口升级数据库版本。
-   实例的网络类型为专有网络。如果网络类型为经典网络，请调用[ModifyDBInstanceNetworkType](~~62138~~)接口将网络类型切换为专有网络。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=ModifyInstanceVpcAuthMode)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceVpcAuthMode|要执行的操作，取值**ModifyInstanceVpcAuthMode**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|VpcAuthMode|String|是|Open|设置专有网络免密访问功能，取值：

 -   **Open**：开启专有网络免密访问。
-   **Close**：关闭专有网络免密访问。

 |
|NodeId|String|否|s-bpxxxxxxxx|分片集群实例的Mongos节点ID。

 **说明：** 实例类型为分片集群实例时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyInstanceVpcAuthMode
&DBInstanceId=dds-bpxxxxxxxx
&VpcAuthMode=Open
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceVpcAuthModeResponse>
  <RequestId>BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C</RequestId>
</ModifyInstanceVpcAuthModeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

