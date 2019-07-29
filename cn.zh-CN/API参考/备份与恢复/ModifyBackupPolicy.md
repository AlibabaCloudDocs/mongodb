# ModifyBackupPolicy {#doc_api_Dds_ModifyBackupPolicy .reference}

调用ModifyBackupPolicy接口修改MongoDB实例的备份策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyBackupPolicy&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyBackupPolicy|要执行的操作，取值：**ModifyBackupPolicy**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|PreferredBackupPeriod|String|是|Monday,Wednesday,Friday,Sunday|备份周期，取值：

 -   **Monday**：周一。
-   **Tuesday**：周二。
-   **Wednesday**：周三。
-   **Thursday**：周四。
-   **Friday**：周五。
-   **Saturday**：周六。
-   **Sunday**：周日。

 **说明：** 如需传入多个值，多个值用英文逗号（,）隔开。

 |
|PreferredBackupTime|String|是|03:00Z-04:00Z|执行备份的时间，格式为*HH:mm*Z-*HH:mm*Z（UTC时间）。

 **说明：** 时间范围限制为1小时。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|644A359C-B871-4DD3-97B5-ED91EF5809C2|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyBackupPolicy
&DBInstanceId=dds-bpxxxxxxxx
&PreferredBackupPeriod=Monday,Wednesday,Friday,Sunday
&PreferredBackupTime=03:00Z-04:00Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyBackupPolicyResponse>
	  <RequestId>644A359C-B871-4DD3-97B5-ED91EF5809C2</RequestId>
</ModifyBackupPolicyResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"644A359C-B871-4DD3-97B5-ED91EF5809C2"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

