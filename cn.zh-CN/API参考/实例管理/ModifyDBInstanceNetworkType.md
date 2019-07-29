# ModifyDBInstanceNetworkType {#doc_api_Dds_ModifyDBInstanceNetworkType .reference}

调用ModifyDBInstanceNetworkType接口切换MongoDB实例的网络类型。

该接口适用于副本集实例和分片集群实例，暂不支持单节点实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceNetworkType&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceNetworkType|要执行的操作，取值：**ModifyDBInstanceNetworkType**。

 |
|NetworkType|String|是|VPC|实例要切换的目标网络类型，取值：

 -   **VPC**：将网络类型切换为专有网络。
-   **Classic**：将网络类型切换为经典网络。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|VpcId|String|否|vpc-bpxxxxxxxx|专有网络ID。

 **说明：** 当**NetworkType**参数取值为**VPC**时，本参数必须传入。

 |
|VSwitchId|String|否|vsw-bpxxxxxxxx|专有网络中的交换机ID。

 **说明：** 当**NetworkType**参数取值为**VPC**时，本参数必须传入。

 |
|RetainClassic|String|否|True|切换网络类型为VPC时，设置是否保留原经典网络地址，取值：

 -   **True**：保留原经典网络地址。
-   **False**：不保留原经典网络地址。

 **说明：** 

-   当**NetworkType**参数取值为**VPC**时，才可以传入本参数。
-   当本参数取值为**True**时，还需要传入**ClassicExpiredDays**参数。

 |
|ClassicExpiredDays|Integer|否|30|切换网络类型为VPC时，设置保留原经典网络地址的时长。 取值：**14**、**30**、**60**、**120**，单位为天。

 **说明：** 

-   当**NetworkType**参数取值为**VPC**时，才可以传入本参数。
-   当**RetainClassic**参数取值为**True**时，本参数必须传入。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|7A9807F0-1301-4154-9849-6497E94A04DB|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyDBInstanceNetworkType
&NetworkType=VPC
&DBInstanceId=dds-bpxxxxxxxx
&VpcId=vpc-bpxxxxxxxx
&VSwitchId=vsw-bpxxxxxxxx
&RetainClassic=True
&ClassicExpiredDays=30
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceNetworkTypeResponse>
	  <RequestId>7A9807F0-1301-4154-9849-6497E94A04DB</RequestId>
</ModifyDBInstanceNetworkTypeResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"7A9807F0-1301-4154-9849-6497E94A04DB"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

