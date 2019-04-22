# DescribeAccounts {#doc_api_Dds_DescribeAccounts .reference}

调用DescribeAccounts接口查询MongoDB实例的数据库账号信息。

**说明：** 本接口目前仅可查询root账号的信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAccounts)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|DescribeAccounts|要执行的操作，取值：**DescribeAccounts**。

 |
|AccountName|String|否|root|账号名，取值：**root**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Accounts| | |账号信息列表。

 |
|└AccountDescription|String|管理员|账号备注信息。

 |
|└AccountName|String|root|账号名。

 |
|└AccountStatus|String|Available|帐号状态。

 -   Unavailable：不可用。
-   Available：可用。

 |
|└DBInstanceId|String|dds-bpxxxxxxxx|帐号所属实例名称。

 |
|RequestId|String|B562A65B-39AB-4EE8-8635-5A222054FB35|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeAccounts
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAccountsResponse>
  <Accounts>
    <Account>
      <AccountStatus>Available</AccountStatus>
      <AccountDescription>管理员</AccountDescription>
      <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
      <AccountName>root</AccountName>
    </Account>
  </Accounts>
  <RequestId>A806B0FC-CFCC-48D8-8AEC-34C892806B40</RequestId>
</DescribeAccountsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Accounts":{
		"Account":[
			{
				"AccountStatus":"Available",
				"AccountDescription":"管理员",
				"DBInstanceId":"dds-bpxxxxxxxx",
				"AccountName":"root"
			}
		]
	},
	"RequestId":"A806B0FC-CFCC-48D8-8AEC-34C892806B40"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

