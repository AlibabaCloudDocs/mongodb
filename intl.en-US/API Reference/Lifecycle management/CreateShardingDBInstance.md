# CreateShardingDBInstance

You can call this operation to create or clone an ApsaraDB for MongoDB sharded cluster instance.

Before you call this operation, make sure that you understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB.

For more information about the specifications of ApsaraDB for MongoDB instances, see [Instance specifications](~~57141~~).

To create replica set instances, you can call the [CreateDBInstance](~~61763~~) operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=CreateShardingDBInstance&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateShardingDBInstance|The operation that you want to perform. Set the value to **CreateShardingDBInstance**. |
|EngineVersion|String|Yes|4.0|The version of the database engine. Valid values:

-   **3.4**
-   **4.0**
-   **4.2**

**Note:**

-   For more information about the limits on database versions and storage engines, see [MongoDB versions and storage engines](~~61906~~).
-   If you call this operation to clone an instance, set the value to the engine version of the source instance. |
|Engine|String|Yes|MongoDB|The database engine of the instance. Set the value to **MongoDB**. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query available regions where the instance can be created. |
|AccountPassword|String|No|Alitest! 159|The password of the root account.

-   The password must contain at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! # $ % ^ & * ( ) _ + - =`
-   The password must be 8 to 32 characters in length. |
|ZoneId|String|No|cn-hangzhou-b|The zone ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query available zones where the instance can be created. |
|Mongos.N.Class|String|No|dds.mongos.standard|The specifications of mongos node N. For more information, see [Instance types](~~57141~~). Valid values: **2** to **32**.

**Note:** **N** specifies the serial number of the mongos node for which the specification is specified. For example,

-   **Mongos.1.Class** specifies the specifications of the first mongos node.
-   **Mongos.2.Class** specifies the specifications of the second mongos node. |
|ReplicaSet.N.Class|String|No|dds.shard.standard|The specifications of shard node N. For more information about the valid values, see [Instance types](~~57141~~). Valid values: **2** to **32**.

**Note:** **N** specifies the serial number of the shard node for which the specification is specified. For example,

-   **ReplicaSet.1.Class** specifies the specifications of the first shard node.
-   **ReplicaSet.2.Class** specifies the specifications of the second shard node. |
|ReplicaSet.N.Storage|Integer|No|20|The storage capacity of shard node N. The values that can be specified for this parameter are subject to the instance specifications. For more information, see [Instance types](~~57141~~).

-   Valid values: **10** to **2000**. Unit: GB.
-   The value must be a multiple of 10 GB.

**Note:** **N** specifies the serial number of the shard node for which storage capacity is specified.

-   **ReplicaSet.1.Storage** specifies the storage capacity of the first shard node.
-   **ReplicaSet.2.Storage** specifies the storage capacity of the second shard node. |
|ConfigServer.N.Class|String|No|dds.cs.mid|The specifications of Configserver node N. Set the value to **dds.cs.mid**.

**Note:** The specifications of a Configserver node is 1 vCPU and 2 GiB memory. The number of Configserver nodes is 1. Set the **ConfigServer.1.Class** parameter to **dds.cs.mid**. |
|ConfigServer.N.Storage|Integer|No|20|The storage capacity of a Configserver node. Set the value to **20**.

**Note:** The storage capacity is fixed as 20 GB. Set the **ConfigServer.1.Storage** parameter to **20**. |
|DBInstanceDescription|String|No|Testdatabase1|The description of the instance. The description must be 2 to 256 characters in length, and can contain digits, letters, underscores \(\_\), and hyphens \(-\). The name must start with a letter. |
|SecurityIPList|String|No|10.23.12.24/24|-   The whitelist that contains the IP addresses that are allowed to access the instance. Separate multiple IP addresses with commas \(,\). Each IP address must be unique. A maximum of 1,000 IP addresses can be added.
-   You can enter IP addresses such as 10.23.12.24 and Classless Inter-Domain Routing \(CIDR\) blocks such as 10.23.12.24/24. /24 indicates that the prefix of the CIDR block is 24-bit long. You can replace 24 with a value within the range of 1 to 32. You can also enter the percent sign \(%\) or 0.0.0.0/0.

**Note:** If you enter the percent sign \(%\) or 0.0.0.0/0, all IP addresses can access the instance. This may introduce security risks to the instance. Proceed with caution. |
|ChargeType|String|No|PrePaid|The billing method of the instance. Valid values:

-   **Postpaid**: pay-as-you-go
-   **Prepaid**: subscription

Default value: pay-as-you-go

**Note:** If you specify this parameter to **PrePaid**, you must also specify the **Period** parameter. |
|Period|Integer|No|1|The subscription period of the instance. Unit: months. Valid values: **1** to **9**, **12**, **24**, and **36**.

**Note:** This parameter is valid and required only if you set the **ChargeType** parameter to **PrePaid**. |
|NetworkType|String|No|VPC|The network type of the instance. Default value: CLASSIC. Valid values:

-   **Classic**
-   **VPC**

**Note:** If you set the value to **VPC**, you must specify the **VpcId** and **VSwitchId** parameters. |
|VpcId|String|No|vpc-bpxxxxxxxx|The ID of the VPC.

**Note:** This parameter is valid only if you set the **NetworkType** parameter to **VPC**. |
|VSwitchId|String|No|vsw-bpxxxxxxxx|The ID of the vSwitch.

**Note:** This parameter is valid only if you set the **NetworkType** parameter to **VPC**. |
|SrcDBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the source instance. You can specify this parameter only when this operation is called to clone instances. If you specify this parameter, you must also specify the **RestoreTime** parameter. |
|RestoreTime|String|No|2019-03-08T02:30:25Z|The point in time to clone the instance. Specify the time in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

You can specify this parameter only when you call this operation to clone an instance. You must also specify the **SrcDBInstanceId** parameter.

**Note:** You can set this parameter to any point in time in the last seven days. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. |
|StorageEngine|String|No|WiredTiger|The storage engine of the instance. Valid values: **WiredTiger**, **RocksDB**, and **TerarkDB**. Default value: **WiredTiger**. For more information about the limits on database versions and storage engines, see [MongoDB versions and storage engines](~~61906~~).

**Note:** If you call this operation to clone an instance, set the value to the database engine of the source instance. |
|AutoRenew|String|No|true|Specifies whether to enable automatic renewal for the instance. Valid values:

-   **true**: enables automatic renewal.
-   **false**: disables automatic renewal. You must manually renew the instance.

Default value: false.

**Note:** This parameter takes effect only when you set the **ChargeType** parameter to **PrePaid**. |
|ProtocolType|String|No|mongodb|The type of the access protocol. Valid values:

-   mongodb: the MongoDB protocol
-   dynamodb: the DynamoDB protocol |
|ReplicaSet.N.ReadonlyReplicas|Integer|No|5|The number of read-only nodes in shard node N. Valid values: **0** to **5**. Default value: **0**.

**Note:** **N** specifies the serial number of the mongos node for which you want to set the read-only nodes. For example,

-   **ReplicaSet.1.ReadonlyReplicas** specifies the specifications of the first mongos node.
-   **ReplicaSet.2.ReadonlyReplicas** specifies the specifications of the second mongos node. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|OrderId|String|2033xxxxxxxxxxxx|The order ID of the instance. |
|RequestId|String|D8F1D721-6439-4257-A89C-F1E8E9C9623D|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=CreateShardingDBInstance
&Engine=MongoDB
&EngineVersion=4.0
&AccountPassword=Alitest! 159
&ZoneId=cn-hangzhou-b
&ClientToken=ETnLKlblzczshOTUbOCzxxxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDBInstanceResponse>
      <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
      <OrderId>2033xxxxxxxxxxxx</OrderId>
      <RequestId>D8F1D721-6439-4257-A89C-F1E8E9C9623D</RequestId>
</CreateDBInstanceResponse>
```

`JSON` format

```
{
    "DBInstanceId": "dds-bpxxxxxxxx",
    "OrderId": "2033xxxxxxxxxxxx",
    "RequestId": "D8F1D721-6439-4257-A89C-F1E8E9C9623D"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

