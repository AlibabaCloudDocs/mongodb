# UpgradeDBInstanceEngineVersion {#doc_api_Dds_UpgradeDBInstanceEngineVersion .reference}

调用UpgradeDBInstanceEngineVersion接口升级数据库版本。

本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。

调用本接口时，要求实例状态为运行中。

**说明：** 

 

-   实例的存储引擎对数据库版本的选择有约束性，详情请参考[版本与存储引擎](~~61906~~)。

-   升级数据库版本后不支持降级数据库版本。
-   升级过程中会自动对实例进行2-3次重启，请确保在业务低峰执行。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=UpgradeDBInstanceEngineVersion)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpgradeDBInstanceEngineVersion|要执行的操作，取值：**UpgradeDBInstanceEngineVersion**。

 |
|EngineVersion|String|是|4.0|升级的目标数据库版本，取值：**3.4**、**4.0**。

 **说明：** 升级的目标数据库版本必须大于实例当前的数据库版本。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C4907B00-A208-4E0C-A636-AA85140E406C|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=UpgradeDBInstanceEngineVersion
&EngineVersion=4.0
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpgradeDBInstanceEngineVersionResponse>
  <RequestId>C4907B00-A208-4E0C-A636-AA85140E406C</RequestId>
</UpgradeDBInstanceEngineVersionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C4907B00-A208-4E0C-A636-AA85140E406C"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

