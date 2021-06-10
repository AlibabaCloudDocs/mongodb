# MigrateAvailableZone

调用MigrateAvailableZone接口迁移MongoDB实例的可用区。

本接口适用于MongoDB 4.2及以下版本的副本集实例，分片集群实例，暂不支持单节点实例。

**说明：** 如果实例申请了公网连接地址，需要先调用[ReleasePublicNetworkAddress](~~67604~~)接口释放公网连接地址。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=MigrateAvailableZone&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|MigrateAvailableZone|要执行的操作，取值**MigrateAvailableZone**。 |
|DBInstanceId|String|是|dds-bp1ece71ff2f\*\*\*\*|实例ID。

 **说明：** 如果实例的网络类型为专有网络，您还需要传入**Vswitch**参数。 |
|ZoneId|String|是|cn-hangzhou-b|迁移的目标可用区ID。

 **说明：**

-   迁移的目标可用区和当前实例的可用区处于同一地域。
-   您可以通过调用[DescribeRegions](~~61933~~)接口查询可用区ID。 |
|Vswitch|String|否|vsw-bp1buy0h9myt5i9e7\*\*\*\*|迁移的目标可用区虚拟交换机ID。

 **说明：** 当实例的网络类型为专有网络时，需要配置该参数。 |
|EffectiveTime|String|否|Immediately|迁移可用区的生效时间，取值：

 -   **Immediately**：立即生效。
-   **MaintainTime**：在实例的可运维时间段内生效。

 默认为**Immediately**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0FDDC511-7252-4A4A-ADDA-5CB1BF63\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=MigrateAvailableZone
&DBInstanceId=dds-bp1ece71ff2f****
&ZoneId=cn-hangzhou-b
&EffectiveTime=Immediately
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<MigrateAvailableZoneResponse>
        <RequestId>0FDDC511-7252-4A4A-ADDA-5CB1BF63****</RequestId>
</MigrateAvailableZoneResponse>
```

`JSON`格式

```
{
        "RequestId": "0FDDC511-7252-4A4A-ADDA-5CB1BF63****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

