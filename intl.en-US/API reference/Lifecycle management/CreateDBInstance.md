# CreateDBInstance {#doc_api_Dds_CreateDBInstance .reference}

You can call this operation to create and clone ApsaraDB for MongoDB instances.

**Make sure that you fully understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB before using this API.** 

For more information about the specifications of ApsaraDB for MongoDB instances, see[Instance specifications](~~57141~~).

To create sharded cluster instances, you can call[CreateShardingDBInstance](~~61884~~).

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=CreateDBInstance) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDBInstance| The operation that you want to perform. Set the value to**CreateDBInstance**.

 |
|ClientToken|String|Yes|ETnLKlblzczshOTUbOCzxxxxxxxxxx| The client token that is used to ensure idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters, and cannot exceed 64 characters in length.

 |
|Engine|String|Yes|MongoDB| The database engine. Set the value to**MongoDB**.

 |
|EngineVersion|String|Yes|4.0| The version number of the database. Valid value:**3.2**,**3.4**or**4.0**.

 **Note:** When calling this operation to clone instances, ensure that this value is the same as the engine version number of its source instances.

 |
|DBInstanceClass|String|Yes|dds.mongo.standard| The specification of the instance. For more information about the value, see[Instance specifications](~~57141~~).

 |
|DBInstanceStorage|Integer|Yes|10| The storage space of the instance.

 -   Valid values:**10**to**3000**. Unit: GB.
-   You can only specify this value in 10 GB increments.

 **Note:** The values that can be specified for this parameter are dependent on the instance specification. For more information, see[Instance specifications](~~57141~~).

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call the[DescribeRegions](~~61933~~)operation to query regions.

 |
|ZoneId|String|No|cn-hangzhou-b| The ID of the zone. You can call the[DescribeRegions](~~61933~~)operation to query zones.

 |
|DBInstanceDescription|String|No|Test database 1| The name of the instance. It must be 2 to 256 characters in length. The name must start with a letter, and can contain digits, letters, underscores \(\_\), and hyphens \(-\).

 |
|SecurityIPList|String|No|10.23.12.24/24| -   The whitelist that contains the IP addresses that are allowed to access the instance. Separate multiple IP addresses with commas \(,\). Each IP address must be unique. A maximum of 1,000 IP addresses can be set.
-   Supported formats of IP addresses are IP addresses such as %, 0.0.0.0/0, 10.23.12.24 or Classless Inter-Domain Routing \(CIDR\) blocks such as 10.23.12.24/24. /24 indicates the length of the IP address prefix. The IP address prefix can consists of 1 to 32 bits.

 **Note:** % and 0.0.0.0/0 indicate that any IP address can access the database. We do not recommend including these values in your whitelist as they expose your database to security risks.

 |
|AccountPassword|String|No|Alitest! 159| The password of the root account.

 -   The password must contain at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters. Special characters include ! \#$%^&\*\(\)\_+-=
-   The password must be 8 to 32 characters in length.

 |
|ChargeType|String|No|PrePaid| The billing method of the instance. Valid values:

 -   PostPaid: Pay-As-You-Go.
-   PrePaid: Subscription.

 Default value: Pay-As-You-Go.

 **Note:** If you specify this parameter to**PrePaid**, you must also specify the**Period**parameter.

 |
|Period|Integer|No|1| The subscription period of the instance. Unit: months. Valid values:**1**to**9**,**12**,**24**, and**36**.

 **Note:** This parameter is only valid when you specify the**ChargeType**parameter to**PrePaid**.

 |
|NetworkType|String|No|VPC| The network type of the instance. Valid values:

 -   **CLASSIC**
-   **VPC**

 Default value: classic.

 **Note:** If you specify this parameter to**VPC**, you must also specify the**VpcId**parameter and the**VSwitchId**parameter.

 |
|VpcId|String|No|vpc-bpxxxxxxxx| The ID of the VPC.

 **Note:** This parameter is only valid when you specify the**NetworkType**parameter to**VPC**.

 |
|VSwitchId|String|No|vsw-bpxxxxxxxx| The ID of the VSwitch.

 **Note:** This parameter is only valid when you specify the**NetworkType**parameter to**VPC**.

 |
|SrcDBInstanceId|String|No|dds-bpxxxxxxxx| The ID of the source instance. This parameter can only be specified when this operation is called to clone instances. You must also specify the**BackupId**parameter or**RestoreTime**parameter.

 |
|BackupId|String|No|32994xxxx| The ID of the specific backup set. This parameter can only be specified when this operation is called to clone instances. You must also specify the**SrcDBInstanceId** parameter.

 **Note:** You can call the [DescribeBackups](62172) operation to query the ID of the backup set.

 |
|RestoreTime|String|No|2019-03-13T12:11:14Z| The time to restore the cloned instance to. The format is *yyyy-MM-dd*T*HH:mm:ss*Z.

 **Note:** 

 -   This parameter can only be specified when this operation is called to clone instances. You must also specify the**SrcDBInstanceId**parameter and the**BackupId**parameter.
-   You can clone instances to any restore time in the past seven days.

 |
|BusinessInfo|String|No|\{“ActivityId":"000000000"\}| The business information. It is an additional parameter.

 |
|DatabaseNames|String|No|mongodbtest| The name of the database.

 **Note:** When calling this operation to clone instances, you can set the database that is specified by this parameter for cloning. Otherwise, all the databases of the instances will be cloned.

 |
|AutoRenew|String|No|true| Indicates whether automatic renewal is enabled for the instance. Valid values:

 -   **true**: Automatic renewal is enabled.
-   **false**: Automatic renewal is not enabled. You must renew the instance manually.

 Default value: false.

 **Note:** This parameter is only valid when you specify the**ChargeType**parameter to**PrePaid**.

 |
|CouponNo|String|No|youhuiquan\_promotion\_option\_id\_for\_blank| The coupon code. Default value:**youhuiquan\_promotion\_option\_id\_for\_blank**.

 |
|StorageEngine|String|No|WiredTiger| The storage engine used by instances. Valid values:**WiredTiger**,**RocksDB**, and**TerarkDB**. Default value: WiredTiger. For more information about the limits on database versions and storage engines, see[Versions and storage engines](~~61906~~).

 **Note:** When calling this operation to clone instances, ensure that this value is the same as the engine version number of its source instances.

 |
|ReplicationFactor|String|No|3| The number of nodes in the replica set instance. Valid values:**3**,**5**, and**7**. Default value:**3**.

 |
|ResourceGroupId|String|No|rg-axxxxxxxx| The ID of the resource group.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx| The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|dds-bpxxxxxxxx| The ID of the instance.

 |
|OrderId|String|2033xxxxxxxxxxxx| The ID of the order.

 |
|RequestId|String|D8F1D721-6439-4257-A89C-F1E8E9C9624D| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=CreateDBInstance
&ClientToken=ETnLKlblzczshOTUbOCzxxxxxxxxxx 
&Engine=MongoDB
&EngineVersion=4.0
&DBInstanceClass=dds.mongo.standard
&DBInstanceStorage=10
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateDBInstanceResponse>
  <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
  <OrderId>2033xxxxxxxxxxxx</OrderId>
  <RequestId>D8F1D721-6439-4257-A89C-F1E8E9C9624D</RequestId>
</CreateDBInstanceResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"D8F1D721-6439-4257-A89C-F1E8E9C9624D",
	"OrderId":"2033xxxxxxxxxxxx",
	"DBInstanceId":"dds-bpxxxxxxxx"
}
```

## Error codes {#section_olq_yii_kxf .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InsufficientBalance|Your account does not have enough balance.|The error message returned when your account does not have sufficient balance. Top up and try again.|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|The error message returned when the specified user has not performed real-name authentication. Perform real-name authentication and try again.|
|400|InvalidCapacity.NotFound|The Capacity provided does not exist in our records.|The error message returned when the configured capacity is invalid. Check the specified parameter.|
|400|IdempotentParameterMismatch|Request uses a client token in a previous request but is not identical to that request.|The error message returned when a different request uses a client token that was used for a previous request.|

[View error codes](https://error-center.aliyun.com/status/product/Dds)

