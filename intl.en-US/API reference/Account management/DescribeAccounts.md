# DescribeAccounts {#doc_api_Dds_DescribeAccounts .reference}

You can call this operation to query the information of the database account of a MongoDB instance.

**Note:** This operation can query only the information of the root account.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAccounts) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|Action|String|No|DescribeAccounts|The operation that you want to perform. Set the value to **DescribeAccounts**.

 |
|AccountName|String|No|root|The name of the account. Set the value to **root**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Accounts| | |The detailed list of database accounts.

 |
|└AccountDescription|String|Administrator|The description of the account.

 |
|└AccountName|String|root|The name of the account.

 |
|└AccountStatus|String|Available|The status of the account.

 -   Unavailable
-   Available

 |
|└DBInstanceId|String|dds-bpxxxxxxxx|The name of the instance to which the account belongs.

 |
|RequestId|String|B562A65B-39AB-4EE8-8635-5A222054FB35|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeAccounts
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeAccountsResponse>
  <Accounts>
    <Account>
      <AccountStatus>Available</AccountStatus>
      <AccountDescription>Administrator</AccountDescription>
      <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
      <AccountName>root</AccountName>
    </Account>
  </Accounts>
  <RequestId>A806B0FC-CFCC-48D8-8AEC-34C892806B40</RequestId>
</DescribeAccountsResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"Accounts":{
		"Account":[
			{
				"AccountStatus":"Available",
				"AccountDescription":"Administrator",
				"DBInstanceId":"dds-bpxxxxxxxx",
				"AccountName":"root"
			}
		]
	},
	"RequestId":"A806B0FC-CFCC-48D8-8AEC-34C892806B40"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

