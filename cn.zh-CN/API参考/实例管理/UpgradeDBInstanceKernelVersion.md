# UpgradeDBInstanceKernelVersion {#doc_api_Dds_UpgradeDBInstanceKernelVersion .reference}

调用UpgradeDBInstanceKernelVersion接口升级MongoDB实例的数据库小版本。

调用本接口时，要求实例状态为运行中。

**说明：** 

-   本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。
-   升级过程中，实例会被重启一次，请在业务低峰期执行该操作。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=UpgradeDBInstanceKernelVersion&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|UpgradeDBInstanceKernelVersion|要执行的操作，取值： **UpgradeDBInstanceKernelVersion**。

 |
|DBInstanceId|String|否|dds-bpxxxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|27B9A130-7C4B-40D9-84E8-2FC081097AAC|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=UpgradeDBInstanceKernelVersion
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpgradeDBInstanceKernelVersionResponse>
	  <RequestId>27B9A130-7C4B-40D9-84E8-2FC081097AAC</RequestId>
</UpgradeDBInstanceKernelVersionResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"27B9A130-7C4B-40D9-84E8-2FC081097AAC"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

