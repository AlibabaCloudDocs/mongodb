# ModifyDBInstanceDescription {#doc_api_Dds_ModifyDBInstanceDescription .reference}

调用ModifyDBInstanceDescription接口修改MongoDB实例名称。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceDescription&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceDescription|String|是|testdata|实例名称。

 **说明：** 

-   不能 http:// 或者 https:// 开头
-   以中文、英文字母开头。
-   可以包含中文、英文字符、下划线（\_）、连接号（-）和数字，字符长度2~256个字符。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 如需修改分片集群实例中的Shard节点或Mongos节点的名称，还需要传入**NodeId**参数。

 |
|Action|String|否|ModifyDBInstanceDescription|要执行的操作，取值：**ModifyDBInstanceDescription**。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Shard节点ID或Mongos节点ID。

 **说明：** 当**DBInstanceId**传入的是分片集群实例ID时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|06F8F642-4009-4FFC-80C4-9D67DBF7B74E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyDBInstanceDescription
&DBInstanceDescription=testdata
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceDescriptionResponse>
	  <RequestId>06F8F642-4009-4FFC-80C4-9D67DBF7B74E</RequestId>
</ModifyDBInstanceDescriptionResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"06F8F642-4009-4FFC-80C4-9D67DBF7B74E"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

