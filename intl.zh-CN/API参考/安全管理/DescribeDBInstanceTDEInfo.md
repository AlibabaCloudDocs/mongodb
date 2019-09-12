# DescribeDBInstanceTDEInfo {#doc_api_Dds_DescribeDBInstanceTDEInfo .reference}

调用DescribeDBInstanceTDEInfo接口查询MongoDB实例的透明数据加密TDE（Transparent Data Encryption）是否开启。

**说明：** 关于该功能的详细介绍，请参见[设置透明数据加密TDE](~~131048~~)。

调用本接口时，实例必须满足以下条件：

-   实例为副本集实例或分片集群实例。
-   实例的存储引擎为WiredTiger。
-   实例的数据库版本为4.0，如果实例数据库版本过低，您可以调用[UpgradeDBInstanceEngineVersion](~~67608~~)接口升级数据库版本。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceTDEInfo&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|DescribeDBInstanceTDEInfo|要执行的操作，取值：**DescribeDBInstanceTDEInfo**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|F4DD0E29-361B-42F2-9301-B0048CCCE5D6|请求ID。

 |
|TDEStatus|String|enabled|TDE状态，返回值为：

 -   **enabled**：开启状态。
-   **disabled**：关闭状态。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeDBInstanceTDEInfo
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceTDEInfoResponse>
	  <TDEStatus>enabled</TDEStatus>
	  <RequestId>F4DD0E29-361B-42F2-9301-B0048CCCE5D6</RequestId>
</DescribeDBInstanceTDEInfoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TDEStatus":"enabled",
	"RequestId":"F4DD0E29-361B-42F2-9301-B0048CCCE5D6"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

