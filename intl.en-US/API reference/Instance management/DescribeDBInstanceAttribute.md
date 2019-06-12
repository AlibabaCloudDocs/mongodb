# DescribeDBInstanceAttribute {#doc_api_Dds_DescribeDBInstanceAttribute .reference}

You can call this operation to query the details of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceAttribute) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceAttribute|The operation that you want to perform. Set the value to **DescribeDBInstanceAttribute**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |
|Engine|String|No|MongoDB|The database engine. Set the value to **MongoDB**.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C373EED9-5125-4DD9-89DB-FB1ECD2C2B4F|The ID of the request.

 |
|DBInstances| | |A detailed list of instances.

 |
|└ChargeType|String|PostPaid|The billing method of the instance.

 -   **PrePaid**: Subscription
-   **PostPaid**: Pay-As-You-Go

 |
|└CreationTime|String|2018-11-21T05:10:00Z|The time when the instance was created. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|└CurrentKernelVersion|String|mongodb\_20180914\_1.1.5|The minor version number of the current database of the instance.

 |
|└DBInstanceClass|String|dds.mongo.mid|The type of the instance.

 |
|└DBInstanceDescription|String|test|The name of the instance.

 |
|└DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance.

 |
|└DBInstanceStatus|String|Running|The state of the instance. For more information, see [Instance states](~~63870~~).

 |
|└DBInstanceStorage|Integer|10|The storage space of the instance.

 |
|└DBInstanceType|String|replicate|The type of the instance.

 -   **replicate**: replica set instance
-   **sharding**: sharded cluster instance

 |
|└Engine|String|MongoDB|The engine of the database.

 |
|└EngineVersion|String|3.4|The version of the database.

 |
|└ExpireTime|String|2019-04-08T16:00Z|The expiration time of the Subscription instance.

 **Note:** This parameter is returned when the instance billing method is Subscription.

 |
|└LastDowngradeTime|String|2019-03-08|The last time when the instance was downgraded.

 |
|└LockMode|String|Unlock|The lock status of the instance.

 -   **Unlock**: The instance is not locked.
-   **ManualLock**: The instance has been manually locked.
-   **LockByExpiration**: The instance has been locked because it has expired.
-   **LockByRestoration**: The instance has been locked before the rollback of the instance.
-   **LockByDiskQuota**: The instance has been locked because its capacity is full.
-   **Released**: The instance is released. When the instance is in the released state, it cannot be unlocked. You must use backup data to create a new instance. Creating a new instance may take a long time.

 |
|└MaintainEndTime|String|03:00Z|The end time of the instance maintenance period.

 |
|└MaintainStartTime|String|02:00Z|The start time of the instance maintenance period.

 |
|└MaxConnections|Integer|500|The maximum connections to the instance.

 |
|└MaxIOPS|Integer|1000|The maximum IOPS of the instance.

 |
|└MongosList| | |A detailed list of mongos.

 **Note:** This parameter is returned when the instance type is sharded cluster.

 |
|└ConnectSting|String|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The connection address of the mongos.

 |
|└NodeClass|String|dds.mongos.mid|The instance type of the mongos.

 |
|└NodeDescription|String|mongos1|The name of the mongos.

 |
|└NodeId|String|s-bpxxxxxxxx|The ID of the mongos.

 |
|└Port|Integer|3717|The connection port of the mongos.

 |
|└NetworkType|String|VPC|The network type of the instance. Valid values:

 -   **Classic**
-   **VPC**

 |
|└RegionId|String|cn-hangzhou|The ID of the region to which the instance belongs.

 |
|└ReplacateId|String|bls-mxxxxxxxx|The ID of the BLS channel.

 |
|└ReplicaSetName|String|mgset-10xxxxxxxx|The name of the instance replica set.

 **Note:** This parameter is returned when the instance type is replica set.

 |
|└ReplicaSets| | |The information of the replica set.

 **Note:** This parameter is returned when the instance type is replica set.

 |
|└ConnectionDomain|String|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The connection address of the node.

 |
|└ConnectionPort|String|ConnectionPort|The connection port of the node.

 |
|└NetworkType|String|VPC|The network type of the node. Valid values:

 -   **Classic**
-   **VPC**

 |
|└ReplicaSetRole|String|Primary|The role of the node.

 -   **Primary**
-   **Secondary**

 |
|└VPCCloudInstanceId|String|vpc-xxxxxxxx|The ID of the VPC instance.

 |
|└VPCId|String|vpc-bpxxxxxxxx|The ID of the VPC to which the instance belongs.

 |
|└VSwitchId|String|vsw-bpxxxxxxxx|The VSwitch ID of the VPC to which the node belongs.

 |
|└ReplicationFactor|String|3|The number of nodes in the instance.

 **Note:** This parameter is returned when the instance is replica set.

 |
|└ResourceGroupId|String|rg-axxxxxxxx|The ID of the resource group to which the instance belongs.

 |
|└ShardList| | |A list of shard information.

 **Note:** This parameter is returned when the instance type is sharded cluster.

 |
|└NodeClass|String|dds.shard.mid|The instance type of the shard.

 |
|└NodeDescription|String|testshard|The name of the shard.

 |
|└NodeId|String|d-bpxxxxxxxx|The ID of the shard.

 |
|└NodeStorage|Integer|10|The storage space of the shard.

 |
|└Tags| | |A list of instance tags.

 |
|└Key|String|test|The key of the instance tag.

 |
|└Value|String|api|The value of the instance tag.

 |
|└VPCId|String|vpc-bpxxxxxxxx|The ID of the VPC.

 |
|└VSwitchId|String|vsw-bpxxxxxxxx|The VSwitch ID of the VPC.

 |
|└VpcAuthMode|String|Open|Indicates whether to enable authentication to allow access within a VPC. Valid values:

 -   **Open**: Authentication is enabled.
-   **Close**: Authentication is disabled.
-   **NotSupport**: Authentication is not supported.

 |
|└ZoneId|String|cn-hangzhou-b|The ID of the zone to which the instance belongs.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeDBInstanceAttribute
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeDBInstanceAttributeResponse>
  <RequestId>9E7B90E1-AD90-4DD9-B1FB-E3BE2E0FDD48</RequestId>
  <DBInstances>
    <DBInstance>
      <CurrentKernelVersion>mongodb_20190408_3.0.12</CurrentKernelVersion>
      <ZoneId>cn-hangzhou-b</ZoneId>
      <MongosList/>
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
      <Tags/>
      <RegionId>cn-hangzhou</RegionId>
      <StorageEngine>WiredTiger</StorageEngine>
      <ShardList/>
      <ReplicaSetName>mgset-xxxxxxxx</ReplicaSetName>
    </DBInstance>
  </DBInstances>
</DescribeDBInstanceAttributeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"9E7B90E1-AD90-4DD9-B1FB-E3BE2E0FDD48",
	"DBInstances":{
		"DBInstance":[
			{
				"CurrentKernelVersion":"mongodb_20190408_3.0.12",
				"ZoneId":"cn-hangzhou-b",
				"MongosList":{
					"MongosAttribute":[]
				},
				"VSwitchId":"vsw-bpxxxxxxxx",
				"Engine":"MongoDB",
				"ReplicationFactor":"3",
				"NetworkType":"VPC",
				"VPCId":"vpc-bpxxxxxxxx",
				"MaxConnections":500,
				"MaintainStartTime":"18:00Z",
				"DBInstanceType":"replicate",
				"ReplicaSets":{
					"ReplicaSet":[
						{
							"NetworkType":"VPC",
							"VPCId":"vpc-bpxxxxxxxx",
							"ConnectionPort":"3717",
							"ReplicaSetRole":"Primary",
							"ConnectionDomain":"dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
							"VSwitchId":"vsw-bpxxxxxxxx",
							"VPCCloudInstanceId":"dds-bpxxxxxxxx"
						},
						{
							"NetworkType":"VPC",
							"VPCId":"vpc-bpxxxxxxxx",
							"ConnectionPort":"3717",
							"ReplicaSetRole":"Secondary",
							"ConnectionDomain":"dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
							"VSwitchId":"vsw-bpxxxxxxxx",
							"VPCCloudInstanceId":"dds-bpxxxxxxxx"
						}
					]
				},
				"VpcAuthMode":"Open",
				"EngineVersion":"4.0",
				"DBInstanceStatus":"Running",
				"ChargeType":"PostPaid",
				"LockMode":"Unlock",
				"MaxIOPS":1000,
				"MaintainEndTime":"22:00Z",
				"DBInstanceClass":"dds.mongo.mid",
				"DBInstanceId":"dds-bpxxxxxxxx",
				"ResourceGroupId":"rg-xxxxxxxx",
				"DBInstanceDescription":"Test database",
				"DBInstanceStorage":10,
				"CreationTime":"2019-04-23T03:52:01Z",
				"Tags":{
					"Tag":[]
				},
				"RegionId":"cn-hangzhou",
				"StorageEngine":"WiredTiger",
				"ShardList":{
					"ShardAttribute":[]
				},
				"ReplicaSetName":"mgset-xxxxxxxx"
			}
		]
	}
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

