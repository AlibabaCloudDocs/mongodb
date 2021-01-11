# CreateDBInstance

You can call this operation to create and clone ApsaraDB for MongoDB instances.

Make sure that you fully understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB before calling this operation.

For more information about the instance types in ApsaraDB for MongoDB, see [Instance types](~~57141~~).

To create sharded cluster instances, you can call the [CreateShardingDBInstance](~~61884~~) operation.

This operation is only available on the partner site.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=CreateDBInstance&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDBInstance|The operation that you want to perform. Set the value to **CreateDBInstance**. |
|ClientToken|String|Yes|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotency of requests. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|Engine|String|Yes|MongoDB|The database engine. Set the value to **MongoDB**. |
|EngineVersion|String|Yes|4.0|The database version of the instance. Valid values: 3.2, 3.4, 4.0, and 4.2.

**Note:** To call this operation to clone an instance, set this value to the engine version of the source instance. |
|DBInstanceClass|String|Yes|dds.mongo.standard|The type of the instance. For more information about valid values, see [Instance types](~~57141~~). |
|DBInstanceStorage|Integer|Yes|10|The storage space of the instance.

-   Valid values:**10**to**3000**. Unit: GB.
-   The value must be a multiple of 10 GB.

**Note:** The values that can be specified for this parameter are subject to the instance specifications. For more information, see [Instance types](~~57141~~). |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the regions where the instance can be created. |
|ZoneId|String|No|cn-hangzhou-b|The zone ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the zones where the instance can be created. |
|DBInstanceDescription|String|No|Test database 1|The name of the instance. It must be 2 to 256 characters in length. The name must start with a letter, and can contain digits, letters, underscores \(\_\), and hyphens \(-\). |
|SecurityIPList|String|No|10.23.12.24/24|-   The whitelist that contains the IP addresses that are allowed to access the instance. Separate multiple IP addresses with commas \(,\). Each IP address must be unique. A maximum of 1,000 IP addresses can be added.
-   You can enter IP addresses such as 10.23.12.24 and Classless Inter-Domain Routing \(CIDR\) blocks such as 10.23.12.24/24. /24 indicates the length of the CIDR block prefix. The prefix can be 1 to 32 bits in length. You can also enter the percent sign \(%\) or 0.0.0.0/0.

**Note:** If you enter the percent sign \(%\) or 0.0.0.0/0, all IP addresses can access the instance. This may introduce security risks to the instance. |
|AccountPassword|String|No|Alitest! 159|The password of the root account.

-   The password must contain at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! @ # $ % ^ & * ( ) _ + - =`.
-   The password must be 8 to 32 characters in length. |
|ChargeType|String|No|PrePaid|The billing method of the instance. Valid values:

-   **Postpaid**: pay-as-you-go
-   **Prepaid**: subscription

Default value: pay-as-you-go

**Note:** If you specify this parameter to **PrePaid**, you must also specify the **Period** parameter. |
|Period|Integer|No|1|The subscription period of the instance. Unit: months. Valid values:**1**to**9**,**12**,**24**, and**36**.

**Note:** This parameter is valid and required only if you set the **ChargeType** parameter to **PrePaid**. |
|NetworkType|String|No|VPC|The network type of the new instance. Valid values:

-   **CLASSIC**
-   **VPC**

Default value: CLASSIC.

**Note:** If you specify this parameter to **VPC**, you must also specify the **VpcId** parameter and the **VSwitchId** parameter. |
|VpcId|String|No|vpc-bpxxxxxxxx|The ID of the VPC.

**Note:** This parameter is valid only if you set the **NetworkType** parameter to **VPC**. |
|VSwitchId|String|No|vsw-bpxxxxxxxx|The ID of the VSwitch.

**Note:** This parameter is valid only if you set the **NetworkType** parameter to **VPC**. |
|SrcDBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the source instance. This parameter can only be specified when this operation is called to clone instances. You must also specify the **BackupId** parameter or **RestoreTime** parameter. |
|BackupId|String|No|32994xxxx|The ID of the specific backup set. This parameter can only be specified when this operation is called to clone instances. You must also specify the **SrcDBInstanceId** parameter.

**Note:** You can call [DescribeBackups](~~62172~~) to query the backup ID. |
|RestoreTime|String|No|2019-03-13T12:11:14Z|The target time point of the clone operation. After you set this parameter, the data of the source instance at the specified time point is used to create an instance. Specify the time in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

**Note:**

-   This parameter can only be specified when this operation is called to clone instances. You must also specify the **SrcDBInstanceId** parameter and the **BackupId** parameter.
-   You can set this parameter to any time point in the last seven days. |
|BusinessInfo|String|No|\{“ActivityId":"000000000"\}|The business information. It is an additional parameter. |
|DatabaseNames|String|No|mongodbtest|The name of the database.

**Note:** When calling this operation to clone instances, you can set the database that is specified by this parameter for cloning. Otherwise, all the databases of the instances will be cloned. |
|AutoRenew|String|No|true|Indicates whether automatic renewal is enabled for the instance. Valid values:

-   **true**: enables automatic renewal.
-   **false**: disables automatic renewal. You must renew the instance manually.

Default value: false.

**Note:** This parameter is valid only if you set the **ChargeType** parameter to **PrePaid**. |
|CouponNo|String|No|youhuiquan\_promotion\_option\_id\_for\_blank|The coupon code. Default value:**youhuiquan\_promotion\_option\_id\_for\_blank**. |
|StorageEngine|String|No|WiredTiger|The storage engine used by the instance. Valid values: **WiredTiger**, **RocksDB**, and **TerarkDB**. Default value: **WiredTiger**. For more information about the limits on database versions and storage engines, see [MongoDB versions and storage engines](~~61906~~).

**Note:** To call this operation to clone an instance, set this value to the engine version of the source instance. |
|ReplicationFactor|String|No|3|The number of nodes in the replica set instance. Valid values:**3**,**5**, and**7**. Default value:**3**. |
|ReadonlyReplicas|String|No|1|The number of read-only nodes. Valid values: **1** to **5**.

**Note:** By default, this parameter is not specified and no read-only node is created. |
|ResourceGroupId|String|No|rg-axxxxxxxx|The ID of the resource group. |
|ClusterId|String|No|dhg-2x7\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the MyBase for MongoDB cluster. To create a MyBase for MongoDB instance, you must log on to the [ApsaraDB for MyBase console](https://cddc.console.aliyun.com/) and create a MyBase for MongoDB cluster and three hosts in the cluster first. For more information, see [Create a cluster](~~141766~).

**Note:** This operation is only available on the China site \(aliyun.com\). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|OrderId|String|2033xxxxxxxxxxxx|The ID of the order. |
|RequestId|String|D8F1D721-6439-4257-A89C-F1E8E9C9624D|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=CreateDBInstance
&ClientToken=ETnLKlblzczshOTUbOCzxxxxxxxxxx
&Engine=MongoDB
&EngineVersion=4.0
&DBInstanceClass=dds.mongo.standard
&DBInstanceStorage=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDBInstanceResponse>
      <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
      <OrderId>2033xxxxxxxxxxxx</OrderId>
      <RequestId>D8F1D721-6439-4257-A89C-F1E8E9C9624D</RequestId>
</CreateDBInstanceResponse>
```

`JSON` format

```
{
    "DBInstanceId": "dds-bpxxxxxxxx",
    "OrderId": "2033xxxxxxxxxxxx",
    "RequestId": "D8F1D721-6439-4257-A89C-F1E8E9C9624D"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|InsufficientBalance|Your account does not have enough balance.|The error message returned when your account does not have sufficient balance. Top up and try again.|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|The error message returned when the specified user has not performed real-name authentication. Perform real-name authentication and try again.|
|400|InvalidCapacity.NotFound|The Capacity provided does not exist in our records.|The error message returned when the configured capacity is invalid. Check the specified parameter.|
|400|IdempotentParameterMismatch|Request uses a client token in a previous request but is not identical to that request.|The error message returned because the two specified requests use the same ClientToken.|
|403|IncorrectBackupSetState|Current backup set state does not support operations.|The error message returned because the backup set is in a state that does not support the current operation.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

