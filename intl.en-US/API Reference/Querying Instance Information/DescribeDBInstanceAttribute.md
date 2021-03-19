# DescribeDBInstanceAttribute

You can call this operation to query the details of an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceAttribute&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceAttribute|The operation that you want to perform. Set the value to **DescribeDBInstanceAttribute**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|Engine|String|No|MongoDB|The database engine of the instance. Set the value to **MongoDB**. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C373EED9-5125-4DD9-89DB-FB1ECD2C2B4F|The ID of the request. |
|DBInstances|Array of DBInstance| |Details about the instances. |
|DBInstance| | | |
|ChargeType|String|PostPaid|The billing method of the instance.

 -   **PrePaid**: Subscription
-   **PostPaid**: pay-as-you-go |
|ConfigserverList|Array of ConfigserverAttribute| |Details about the Configserver nodes.

 **Note:** This parameter is returned if the instance is a sharded cluster instance. |
|ConfigserverAttribute| | | |
|ConnectString|String|mongodb://root:\*\*\*\*@dds-bpxxxxxxxxxxxxxx-cs1730-pub.mongodb.rds.aliyuncs.com:3717,|The connection string of the Configserver node. |
|MaxConnections|Integer|0|The maximum number of connections to the Configserver node. |
|MaxIOPS|Integer|1000|The maximum input/output operations per second \(IOPS\) on the Configserver node. |
|NodeClass|String|dds.cs.mid|The specfications of the Configserver node. |
|NodeDescription|String|testConfigserver|The name of the Configserver node. |
|NodeId|String|dds-bpxxxxxxxxxxxxxx-cs|The ID of the Configserver node. |
|NodeStorage|Integer|20|The storage capacity of the Configserver node. |
|Port|Integer|3717|The port number that is used to connect to the Configserver node. |
|CreationTime|String|2018-11-21T05:10:00Z|The time when the instance was created. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CurrentKernelVersion|String|mongodb\_20180914\_1.1.5|The minor version of the current database of the instance. |
|DBInstanceClass|String|dds.mongo.mid|The instance type |
|DBInstanceDescription|String|Test|The description of the instance. |
|DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|DBInstanceReleaseProtection|Boolean|true|Indicates whether release protection is enabled for the instance. Valid values:

 -   **true**: Release protection is enabled.
-   **false**: Release protection is disabled. |
|DBInstanceStatus|String|Running|The state of the instance. For more information, see [Instance states](~~63870~~). |
|DBInstanceStorage|Integer|10|The storage capacity of the instance. |
|DBInstanceType|String|replicate|The category of the instance.

 -   **replicate**: replica set instance
-   **sharding**: sharded cluster instance |
|Engine|String|MongoDB|The database engine of the instance. |
|EngineVersion|String|3.4|The version of the database engine. |
|ExpireTime|String|2019-04-08T16:00Z|The time when the subscription instance expires. The time is in the *yyyy-MM-dd*T*HH:mm*Z format. The time is displayed in UTC.

 **Note:** This parameter is returned if the instance is a subscription instance. |
|KindCode|String|1|The kind code of the instance. Valid values:

 -   **0**: physical machine
-   **1**: Elastic Compute Service \(ECS\) instance
-   **2**: Docker cluster
-   **18**: Kubernetes cluster |
|LastDowngradeTime|String|2019-03-08|The last time when the instance was downgraded. |
|LockMode|String|Unlock|Indicates whether the instance is locked.

 -   **Unlock**: The instance is not locked.
-   **ManualLock**: The instance is manually locked.
-   **LockByExpiration**: The instance is locked upon expiration.
-   **LockByRestoration**: The instance is locked for a rollback.
-   **LockByDiskQuota**: The instance is automatically locked because the storage space is exhausted.
-   **Released**: The instance is released. You cannot unlock an instance that has been released. After an instance is released, you can only use a backup to restore the data of the instance to a new instance. This process requires a long period of time. |
|MaintainEndTime|String|03:00Z|The end time of the maintenance window. The time is in the *HH:mm*Z format. The time is displayed in UTC. |
|MaintainStartTime|String|02:00Z|The start time of the maintenance window. The time is in the *HH:mm*Z format. The time is displayed in UTC. |
|MaxConnections|Integer|500|The maximum number of connections to the instance. |
|MaxIOPS|Integer|1000|The IOPS of the instance. |
|MongosList|Array of MongosAttribute| |Details about the mongos nodes.

 **Note:** This parameter is returned if the instance is a sharded cluster instance. |
|MongosAttribute| | | |
|ConnectSting|String|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The endpoint of the mongos node. |
|MaxConnections|Integer|1000|The maximum number of connections to the mongos node. |
|MaxIOPS|Integer|0|The maximum IOPS of the mongos node. |
|NodeClass|String|dds.mongos.mid|The specifications of the mongos node. |
|NodeDescription|String|mongos1|The name of the mongos node. |
|NodeId|String|s-bpxxxxxxxx|The ID of the mongos node. |
|Port|Integer|3717|The port number that is used to connect to the mongos node. |
|VPCId|String|vpc-bp1xxxxxxxxxxxxxxxxxx|The VPC ID of the mongos node. |
|VSwitchId|String|vsw-bp1xxxxxxxxxxxxxxxxxx|The vSwitch ID of the mongos node. |
|VpcCloudInstanceId|String|s-bp1xxxxxxxxxxxxx|The ID of the VPC-type mongos node. |
|NetworkType|String|VPC|The network type of the instance. Valid values:

 -   **Classic**
-   **VPC** |
|ProtocolType|String|mongodb|The access protocol type of the instance. Valid values:

 -   **mongodb**: the MongoDB protocol
-   **dynamodb**: the DynamoDB protocol |
|ReadonlyReplicas|String|0|The number of read-only nodes in the instance. |
|RegionId|String|cn-hangzhou|The region ID of the instance. |
|ReplacateId|String|bls-mxxxxxxxx|The ID of the BLS channel. |
|ReplicaSetName|String|mgset-10xxxxxxxx|The replica set name of the instance.

 **Note:** This parameter is returned if the instance is a replica set instance. |
|ReplicaSets|Array of ReplicaSet| |Details about the replica set instances.

 **Note:** This parameter is returned if the instance is a replica set instance. |
|ReplicaSet| | | |
|ConnectionDomain|String|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The endpoint of the node. |
|ConnectionPort|String|ConnectionPort|The port number that is used to connect to the node. |
|NetworkType|String|VPC|The network type of the node. Valid values:

 -   **Classic**
-   **VPC** |
|ReplicaSetRole|String|Primary|The role of the node.

 -   **Primary**
-   **Secondary** |
|VPCCloudInstanceId|String|vpc-xxxxxxxx|The ID of the VPC-type instance. |
|VPCId|String|vpc-bpxxxxxxxx|The VPC ID of the node. |
|VSwitchId|String|vsw-bpxxxxxxxx|The vSwitch ID of the node. |
|ReplicationFactor|String|3|The number of nodes in the instance.

 **Note:** This parameter is returned if the instance is a replica set instance. |
|ResourceGroupId|String|rg-axxxxxxxx|The ID of the resource group. |
|ShardList|Array of ShardAttribute| |Details about the shard nodes.

 **Note:** This parameter is returned if the instance is a sharded cluster instance. |
|ShardAttribute| | | |
|ConnectString|String|d-bpxxxxxxxxxxxxxxxxxx.mongodb.rds.aliyuncs.com|The endpoint of the shard node. |
|MaxConnections|Integer|8000|The maximum number of connections to the shard node. |
|MaxIOPS|Integer|8000|The maximum IOPS of the shard node. |
|NodeClass|String|dds.shard.mid|The specifications of the shard node. |
|NodeDescription|String|testshard|The name of the shard node. |
|NodeId|String|d-bpxxxxxxxx|The ID of the shard node. |
|NodeStorage|Integer|10|The storage capacity of the shard node. |
|Port|Integer|3717|The port that is used to connect to the shard node. |
|ReadonlyReplicas|Integer|1|The number of read-only nodes in the shard node. Valid values: **0** to **5**.

 **Note:** This parameter is available only for ApsaraDB for MongoDB instances that are purchased on the China site \(aliyun.com\). |
|StorageEngine|String|WiredTiger|The storage engine of the instance. |
|Tags|Array of Tag| |Details about the instance tags. |
|Tag| | | |
|Key|String|test|The tag key of the instance. |
|Value|String|api|The tag value of the instance. |
|VPCCloudInstanceIds|String|s-bp1xxxxxxxxxxxxx|The ID of the VPC-type instance. |
|VPCId|String|vpc-bpxxxxxxxx|The VPC ID of the instance. |
|VSwitchId|String|vsw-bpxxxxxxxx|The vSwitch ID of the instance. |
|VpcAuthMode|String|Open|Indicates whether to enable authentication to allow access within a VPC. Valid values:

 -   **Open**: Password-free access is enabled.
-   **Close**: Password-free access is disabled.
-   **NotSupport**: Authentication is not supported. |
|ZoneId|String|cn-hangzhou-b|The zone ID of the instance. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeDBInstanceAttribute
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBInstanceAttributeResponse>
	  <RequestId>9E7B90E1-AD90-4DD9-B1FB-E3BE2E0FDD48</RequestId>
	  <DBInstances>
		    <DBInstance>
			      <CurrentKernelVersion>mongodb_20190408_3.0.12</CurrentKernelVersion>
			      <ZoneId>cn-hangzhou-b</ZoneId>
			      <MongosList></MongosList>
			      <VSwitchId>vsw-bpxxxxxxxx</VSwitchId>
			      <Engine>MongoDB</Engine>
			      <ReplicationFactor>3</ReplicationFactor>
			      <NetworkType>VPC</NetworkType>
			      <VPCId>vpc-bpxxxxxxxx</VPCId>
			      <MaintainStartTime>18:00Z</MaintainStartTime>
			      <MaxConnections>500</MaxConnections>
			      <ReplicaSets>
				        <ReplicaSet>
					          <NetworkType>VPC</NetworkType>
					          <VPCId>vpc-bpxxxxxxxx</VPCId>
					          <ConnectionPort>3717</ConnectionPort>
					          <ReplicaSetRole>Primary</ReplicaSetRole>
					          <ConnectionDomain>dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com</ConnectionDomain>
					          <VSwitchId>vsw-bpxxxxxxxx</VSwitchId>
					          <VPCCloudInstanceId>dds-bpxxxxxxxx</VPCCloudInstanceId>
				        </ReplicaSet>
				        <ReplicaSet>
					          <NetworkType>VPC</NetworkType>
					          <VPCId>vpc-bpxxxxxxxx</VPCId>
					          <ConnectionPort>3717</ConnectionPort>
					          <ReplicaSetRole>Secondary</ReplicaSetRole>
					          <ConnectionDomain>dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com</ConnectionDomain>
					          <VSwitchId>vsw-bpxxxxxxxx</VSwitchId>
					          <VPCCloudInstanceId>dds-bpxxxxxxxx</VPCCloudInstanceId>
				        </ReplicaSet>
			      </ReplicaSets>
			      <DBInstanceType>replicate</DBInstanceType>
			      <VpcAuthMode>Open</VpcAuthMode>
			      <EngineVersion>4.0</EngineVersion>
			      <DBInstanceStatus>Running</DBInstanceStatus>
			      <ChargeType>PostPaid</ChargeType>
			      <LockMode>Unlock</LockMode>
			      <MaxIOPS>1000</MaxIOPS>
			      <MaintainEndTime>22:00Z</MaintainEndTime>
			      <DBInstanceClass>dds.mongo.mid</DBInstanceClass>
			      <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
			      <ResourceGroupId>rg-xxxxxxxx</ResourceGroupId>
			      <DBInstanceDescription>Test database</DBInstanceDescription>
			      <DBInstanceStorage>10</DBInstanceStorage>
			      <CreationTime>2019-04-23T03:52:01Z</CreationTime>
			      <Tags></Tags>
			      <RegionId>cn-hangzhou</RegionId>
			      <StorageEngine>WiredTiger</StorageEngine>
			      <ShardList></ShardList>
			      <ReplicaSetName>mgset-xxxxxxxx</ReplicaSetName>
		    </DBInstance>
	  </DBInstances>
</DescribeDBInstanceAttributeResponse>
```

`JSON` format

```
{
	"RequestId": "9E7B90E1-AD90-4DD9-B1FB-E3BE2E0FDD48",
	"DBInstances": {
		"DBInstance": [
			{
				"CurrentKernelVersion": "mongodb_20190408_3.0.12",
				"ZoneId": "cn-hangzhou-b",
				"MongosList": {
					"MongosAttribute": []
				},
				"VSwitchId": "vsw-bpxxxxxxxx",
				"Engine": "MongoDB",
				"ReplicationFactor": "3",
				"NetworkType": "VPC",
				"VPCId": "vpc-bpxxxxxxxx",
				"MaintainStartTime": "18:00Z",
				"MaxConnections": 500,
				"ReplicaSets": {
					"ReplicaSet": [
						{
							"NetworkType": "VPC",
							"VPCId": "vpc-bpxxxxxxxx",
							"ConnectionPort": "3717",
							"ReplicaSetRole": "Primary",
							"ConnectionDomain": "dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
							"VSwitchId": "vsw-bpxxxxxxxx",
							"VPCCloudInstanceId": "dds-bpxxxxxxxx"
						},
						{
							"NetworkType": "VPC",
							"VPCId": "vpc-bpxxxxxxxx",
							"ConnectionPort": "3717",
							"ReplicaSetRole": "Secondary",
							"ConnectionDomain": "dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
							"VSwitchId": "vsw-bpxxxxxxxx",
							"VPCCloudInstanceId": "dds-bpxxxxxxxx"
						}
					]
				},
				"DBInstanceType": "replicate",
				"VpcAuthMode": "Open",
				"EngineVersion": "4.0",
				"DBInstanceStatus": "Running",
				"ChargeType": "PostPaid",
				"LockMode": "Unlock",
				"MaxIOPS": 1000,
				"MaintainEndTime": "22:00Z",
				"DBInstanceClass": "dds.mongo.mid",
				"DBInstanceId": "dds-bpxxxxxxxx",
				"ResourceGroupId": "rg-xxxxxxxx",
				"DBInstanceDescription": "Testdatabase",
				"DBInstanceStorage": 10,
				"CreationTime": "2019-04-23T03:52:01Z",
				"Tags": {
					"Tag": []
				},
				"RegionId": "cn-hangzhou",
				"StorageEngine": "WiredTiger",
				"ShardList": {
					"ShardAttribute": []
				},
				"ReplicaSetName": "mgset-xxxxxxxx"
			}
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

