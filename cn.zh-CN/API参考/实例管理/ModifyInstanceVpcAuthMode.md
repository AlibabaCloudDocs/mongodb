# ModifyInstanceVpcAuthMode {#doc_api_Dds_ModifyInstanceVpcAuthMode .reference}

调用ModifyInstanceVpcAuthMode接口开启或关闭MongoDB实例的专有网络免密访问功能。

调用本接口时，实例必须满足以下条件：

-   实例的类型为副本集实例或分片集群实例。
-   实例的数据库版本为4.0版本，数据库小版本为mongodb\_20190408\_3.0.11及以上版本，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)接口查看版本信息。如果版本过低请调用[UpgradeDBInstanceEngineVersion](~~67608~~)接口升级数据库版本。
-   实例的网络类型为专有网络。如果网络类型为经典网络，请调用[ModifyDBInstanceNetworkType](~~62138~~)接口将网络类型切换为专有网络。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyInstanceVpcAuthMode&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|ModifyInstanceVpcAuthMode|要执行的操作，取值**ModifyInstanceVpcAuthMode**。

 |
|NodeId|String|否|s-bpxxxxxxxx|分片集群实例的Mongos节点ID。

 **说明：** 实例类型为分片集群实例时，本参数才可用。

 |
|VpcAuthMode|String|否|Open|设置专有网络免密访问功能，取值：

 -   **Open**：开启专有网络免密访问。
-   **Close**：关闭专有网络免密访问。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

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

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

