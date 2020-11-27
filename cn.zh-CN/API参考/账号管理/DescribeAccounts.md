# DescribeAccounts

调用DescribeAccounts接口查询MongoDB实例的数据库账号信息。

**说明：** 本接口目前仅可查询root账号的信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeAccounts&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAccounts|要执行的操作，取值：**DescribeAccounts**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。 |
|RegionId|String|否|cn-hangzhou|地域ID，可调用[DescribeRegions](~~61933~~)查询。 |
|AccountName|String|否|root|账号名，取值：**root**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Accounts|Array| |账号信息列表。 |
|Account| | | |
|AccountDescription|String|管理员|账号备注信息。 |
|AccountName|String|root|账号名。 |
|AccountStatus|String|Available|帐号状态。

-   Unavailable：不可用。
-   Available：可用。 |
|CharacterType|String|mongos|账号的角色类型，返回值：

-   db：shard角色
-   cs：config server角色
-   mongos：mongos角色
-   logic：分片集群实例
-   normal：副本集实例 |
|DBInstanceId|String|dds-bpxxxxxxxx|帐号所属实例名称。 |
|RequestId|String|B562A65B-39AB-4EE8-8635-5A222054FB35|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeAccounts
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
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

```
{
    "Accounts": {
        "Account": [
            {
                "AccountStatus": "Available",
                "AccountDescription": "管理员",
                "DBInstanceId": "dds-bpxxxxxxxx",
                "AccountName": "root"
            }
        ]
    },
    "RequestId": "A806B0FC-CFCC-48D8-8AEC-34C892806B40"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

