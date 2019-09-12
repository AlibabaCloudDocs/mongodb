# ModifyDBInstanceTDE {#doc_api_Dds_ModifyDBInstanceTDE .reference}

调用ModifyDBInstanceTDE接口修改MongoDB实例的透明数据加密TDE（Transparent Data Encryption）状态。

透明数据加密TDE（Transparent Data Encryption）可对数据文件执行实时I/O加密和解密，数据在写入磁盘之前进行加密，从磁盘读入内存时进行解密，更多详情请参见[设置透明数据加密TDE](~~131048~~)。

**说明：** TDE功能开通后无法关闭。

调用本接口时，实例必须满足以下条件：

-   实例为副本集实例或分片集群实例。
-   实例的存储引擎为WiredTiger。
-   实例的数据库版本为4.0，如果实例数据库版本过低，您可以调用[UpgradeDBInstanceEngineVersion](~~67608~~)接口升级数据库版本。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceTDE&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|TDEStatus|String|是|enabled|TDE状态，取值： **enabled**，即开启TDE功能。

 **说明：** TDE功能开启后不支持关闭，请谨慎开启。

 |
|Action|String|否|ModifyDBInstanceTDE|要执行的操作，取值：**ModifyDBInstanceTDE**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|EncryptorName|String|否|AES-256-CBC|加密方式，取值：**AES-256-CBC**。

 **说明：** 当**TEDStatus**参数取值为**enabled**时，本参数才可用。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|434D7127-6229-4355-BA50-7A3685A725DF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyDBInstanceTDE
&DBInstanceId=dds-bpxxxxxxxx
&TDEStatus=enabled
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceTDEResponse>
	  <RequestId>434D7127-6229-4355-BA50-7A3685A725DF</RequestId>
</ModifyDBInstanceTDEResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"434D7127-6229-4355-BA50-7A3685A725DF"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|IncorrectDBInstanceState|Current DB instance state does not support this operation.|实例状态不支持此操作，请您检查输入的参数是否正确。|
|403|IncorrectDBInstanceLockMode|Current DB instance lock mode does not support this operation.|实例已经被锁定。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

