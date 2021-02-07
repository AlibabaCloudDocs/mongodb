# DescribeAccounts

You can call this operation to query the database accounts of an ApsaraDB for MongoDB instance.

**Note:** This operation can query only the information of the root account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeAccounts&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAccounts|The operation that you want to perform. Set the value to **DescribeAccounts**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID. |
|AccountName|String|No|root|The name of the account. Set the value to **root**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Accounts|Array| |Details about the accounts. |
|Account| | | |
|AccountDescription|String|Administrator|The description of the account. |
|AccountName|String|root|The name of the account. |
|AccountStatus|String|Available|The status of the account.

-   Unavailable
-   Available |
|CharacterType|String|mongos|The role of the account. Valid values:

-   db: shard
-   cs: Configserver
-   mongos: mongos
-   logic: sharded cluster instance
-   normal: replica set instance |
|DBInstanceId|String|dds-bpxxxxxxxx|The name of the instance to which the account belongs. |
|RequestId|String|B562A65B-39AB-4EE8-8635-5A222054FB35|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeAccounts
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
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

```
{
    "Accounts": {
        "Account": [
            {
                "AccountStatus": "Available",
                "AccountDescription": "Administrator",
                "DBInstanceId": "dds-bpxxxxxxxx",
                "AccountName": "root"
            }
        ]
    },
    "RequestId": "A806B0FC-CFCC-48D8-8AEC-34C892806B40"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

