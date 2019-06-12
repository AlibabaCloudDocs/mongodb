# CreateShardingDBInstance {#doc_api_Dds_CreateShardingDBInstance .reference}

You can call this operation to create or clone ApsaraDB for MongoDB sharded cluster instances.

**Make sure that you fully understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB before using this API.** 

For more information about the specifications of ApsaraDB for MongoDB instances, see[Instance specifications](~~57141~~).

To create replica set instances, you can call [CreateDBInstance](~~61763~~).

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=CreateShardingDBInstance) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateShardingDBInstance| The operation that you want to perform. Set the value to**CreateShardingDBInstance**.

 |
|Engine|String|Yes|MongoDB| The database engine. Valid value:**MongoDB**.

 |
|EngineVersion|String|Yes|4.0| The version number of the database. Valid values:**3.4**and**4.0**.

 **Note:** 

 -   For more information about the limits on database versions and storage engines, see[Versions and storage engines](~~61906~~).
-   When calling this operation to clone instances, ensure that this value is the same as the engine version number of its source instances.

 |
|AccountPassword|String|Yes|Alitest! 159| The password of the root account.

 -   The password must contain at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters. Special characters include ! \#$%^&\*\(\)\_+-=
-   The password must be 8 to 32 characters in length.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call the[DescribeRegions](~~61933~~)operation to query available regions.

 |
|ZoneId|String|No|cn-hangzhou-b| The ID of the zone. You can call the[DescribeRegions](~~61933~~)operation to query available zones.

 |
|DBInstanceDescription|String|No|Test database 1| The name of the instance. It must be 2 to 256 characters in length. The name must start with a letter, and can contain digits, letters, underscores \(\_\), and hyphens \(-\).

 |
|SecurityIPList|String|No|10.23.12.24/24| -   The whitelist that contains the IP addresses that are allowed to access the instance. Separate multiple IP addresses with commas \(,\). Each IP address must be unique. A maximum of 1,000 IP addresses can be set.
-   Supported formats of IP addresses are IP addresses such as %, 0.0.0.0/0, 10.23.12.24 or Classless Inter-Domain Routing \(CIDR\) blocks such as 10.23.12.24/24. /24 indicates the length of the IP address prefix. The IP address prefix can consists of 1 to 32 bits.

 **Note:** % and 0.0.0.0/0 indicate that any IP address can access the database. We do not recommend including these values in your whitelist as they expose your database to security risks.

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
|NetworkType|String|No|VPC| The network type of the instance. The classic network is specified by default when you create the instance.

 -   **CLASSIC**
-   **VPC**

 **Note:** If you specify this parameter to**VPC**, you must also specify the**VpcId**parameter and the**VSwitchId**parameter.

 |
|VpcId|String|No|vpc-bpxxxxxxxx| The ID of the VPC.

 **Note:** This parameter is only valid when you specify the**NetworkType**parameter to**VPC**.

 |
|Mongos.N.Class|String|No|dds.mongos.standard| The specification of mongos N. For more information, see[Instance specifications](~~57141~~).

 **N**indicates the sequence of the mongos for which a specification is specified. For example,

 -   **Mongos. 1.Class**specifies the specification of the first mongs.
-   **Mongos. 2.Class**specifies the specification of the second mongos.

 **Note:** You can specify 2 to 32 mongos.

 |
|ReplicaSet.N.Class|String|No|dds.shard.standard| The specification of shard N. For more information about the value, see[Instance specifications](~~57141~~).

 **N**indicates the sequence of the shard for which a specification is specified. For example,

 -   **ReplicaSet. 1.Class**specifies the specification of the first shard.
-   **ReplicaSet. 2.Class**specifies the specification of the second shard.

 **Note:** You can specify 2 to 32 shards.

 |
|ReplicaSet.N.Storage|Integer|No|20| The storage space of shard N.

 -   Valid values:**10**to**2000**. Unit: GB.
-   You can only specify this value in 10 GB increments.

 **Note:** The values that can be specified for this parameter are dependent on the instance specifications. For more information, see[Instance specifications](~~57141~~).

 **N**indicates the sequence of the shard for which storage space is specified. For example,

 -   **ReplicaSet. 1.Storage**specifies the storage space of the first shard.
-   **ReplicaSet. 2.Storage**specifies the storage space of the second shard.

 |
|ConfigServer.N.Class|String|No|dds.cs.mid| The specification of config server N. Valid value:**dds.cs.mid**.

 **Note:** The specifications of the config server are fixed at 1 core and 2 GB memory. The value of N is fixed at 1. For example, set the value of**ConfigServer.1.Class**parameter to**dds.cs.mid**.

 |
|ConfigServer.N.Storage|Integer|No|20| The storage space of config server N. Valid value:**20**.

 **Note:** This parameter can be specified to only 20 GB. For example, set the value of**ConfigServer.1.Storage**to**20**.

 |
|VSwitchId|String|No|vsw-bpxxxxxxxx| The ID of the VSwitch.

 **Note:** This parameter is only valid when you specify the**NetworkType**parameter to**VPC**.

 |
|SrcDBInstanceId|String|No|dds-bpxxxxxxxx| The ID of the source instance. This parameter can only be specified when this operation is called to clone instances. You must also specify the**RestoreTime**parameter.

 |
|RestoreTime|String|No|2019-03-08T02:30:25Z| The time to restore the cloned instance to. The format is *yyyy-MM-dd*T*HH:mm:ss*Z.

 This parameter can only be specified when this operation is called to clone instances. You must also specify the**SrcDBInstanceId**parameter.

 **Note:** You can clone instances to any restore time in the past seven days.

 |
|StorageEngine|String|No|WiredTiger| The storage engine used by instances. Valid values:**WiredTiger**,**RocksDB**, and**TerarkDB**. Default value: WiredTiger. For more information about the limits on database versions and storage engines, see[Versions and storage engines](~~61906~~).

 **Note:** When calling this operation to clone instances, ensure that this value is the same as the engine version number of its source instances.

 |
|AutoRenew|String|No|true| Indicates whether automatic renewal is enabled for the instance. Valid values:

 -   **true**: Automatic renewal is enabled.
-   **false**: Automatic renewal is not enabled. You must renew the instance manually.

 Default value: false.

 **Note:** This parameter is only valid when you specify the**ChargeType**parameter to**PrePaid**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx| The AccessKey ID provided to you by Alibaba Cloud.

 |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx| The client token that is used to ensure idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters, and cannot exceed 64 characters in length.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|dds-bpxxxxxxxx| The ID of the instance.

 |
|OrderId|String|2033xxxxxxxxxxxx| The ID of the order.

 |
|RequestId|String|D8F1D721-6439-4257-A89C-F1E8E9C9623D| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=CreateShardingDBInstance
&Engine=MongoDB
&EngineVersion=4.0
&AccountPassword=Alitest! 159
&ZoneId=cn-hangzhou-b 
&ClientToken=ETnLKlblzczshOTUbOCzxxxxxxxxxx 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateDBInstanceResponse>
  <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
  <OrderId>2033xxxxxxxxxxxx</OrderId>
  <RequestId>D8F1D721-6439-4257-A89C-F1E8E9C9623D</RequestId> 
</CreateDBInstanceResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"D8F1D721-6439-4257-A89C-F1E8E9C9623D",
	"OrderId":"2033xxxxxxxxxxxx",
	"DBInstanceId":"dds-bpxxxxxxxx"
}
```

## Error codes {#section_qfv_w7k_00q .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

