# AllocatePublicNetworkAddress {#doc_api_Dds_AllocatePublicNetworkAddress .reference}

调用AllocatePublicNetworkAddress接口为MongoDB实例申请公网连接地址。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=AllocatePublicNetworkAddress&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|Action|String|否|AllocatePublicNetworkAddress|要执行的操作，取值：**AllocatePublicNetworkAddress**。

 |
|NodeId|String|否|s-bpxxxxxxxx|分片集群实例中Mongos节点ID。

 **说明：** 当**DBInstanceId**传入的是分片集群实例ID时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B6D17591-B48B-4D31-9CD6-9B9796B2270A|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=AllocatePublicNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AllocatePublicNetworkAddressResponse>
	  <RequestId>B6D17591-B48B-4D31-9CD6-9B9796B2270A</RequestId>
</AllocatePublicNetworkAddressResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B6D17591-B48B-4D31-9CD6-9B9796B2270A"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

