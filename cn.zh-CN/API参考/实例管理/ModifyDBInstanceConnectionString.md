# ModifyDBInstanceConnectionString {#doc_api_Dds_ModifyDBInstanceConnectionString .reference}

调用ModifyDBInstanceConnectionString接口修改MongoDB实例的连接地址。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceConnectionString&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|CurrentConnectionString|String|是|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|当前连接地址，即待修改的连接地址。

 |
|NewConnectionString|String|是|aliyuntest111|新的连接地址，以小写字母开头，由字母、数字组成，长度为8~64个字符。

 **说明：** 仅需传入连接地址的前缀部分，前缀以外的部分不可修改。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|Action|String|否|ModifyDBInstanceConnectionString|要执行的操作，取值： **ModifyDBInstanceConnectionString**。

 |
|NodeId|String|否|s-bpxxxxxxxx|分片集群实例中的Mongos节点ID，每次调用仅能传入一个Mongos节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FF36A84C-0694-42D0-861D-C383E8E4FAAF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyDBInstanceConnectionString
&CurrentConnectionString=s-bpxxxxxxxx.mongodb.rds.aliyuncs.com
&NewConnectionString=aliyuntest111
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceConnectionStringResponse>
	  <RequestId>FF36A84C-0694-42D0-861D-C383E8E4FAAF</RequestId>
</ModifyDBInstanceConnectionStringResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"FF36A84C-0694-42D0-861D-C383E8E4FAAF"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

