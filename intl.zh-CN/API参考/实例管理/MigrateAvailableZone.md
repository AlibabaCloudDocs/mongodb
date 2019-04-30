# MigrateAvailableZone {#doc_api_Dds_MigrateAvailableZone .reference}

调用MigrateAvailableZone接口迁移MongoDB实例的可用区。

本接口适用于副本集实例，暂不支持单节点实例和分片集群实例。

**说明：** 如果实例申请了公网连接地址，需要先调用[ReleasePublicNetworkAddress](~~67604~~)接口释放公网连接地址。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=MigrateAvailableZone)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|MigrateAvailableZone|要执行的操作，取值**MigrateAvailableZone**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 如果实例的网络类型为专有网络，您还需要传入**Vswitch**参数。

 |
|ZoneId|String|是|cn-hangzhou-b|迁移的目标可用区ID。

 **说明：** 

-   迁移的目标可用区和当前实例的可用区处于同一地域。
-   您可以通过调用[DescribeRegions](~~61933~~)接口查询可用区ID。

 |
|EffectiveTime|String|是|Immediately|迁移可用区的生效时间，取值：

 -   **Immediately**：立即生效。
-   **MaintainTime**：在实例的可运维时间段内生效。

 默认为**Immediately**。

 |
|Vswitch|String|否|1|迁移的目标可用区虚拟交换机ID。

 **说明：** 当实例的网络类型为专有网络时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0FDDC511-7252-4A4A-ADDA-5CB1BF63873D|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=MigrateAvailableZone
&DBInstanceId=dds-bpxxxxxxxx
&ZoneId=cn-hangzhou-b
&EffectiveTime=Immediately
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<MigrateAvailableZoneResponse>
  <RequestId>0FDDC511-7252-4A4A-ADDA-5CB1BF63873D</RequestId>
</MigrateAvailableZoneResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"0FDDC511-7252-4A4A-ADDA-5CB1BF63873D"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

