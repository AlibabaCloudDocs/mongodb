# DescribeDBInstanceAttribute

调用DescribeDBInstanceAttribute接口查询MongoDB实例详情。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceAttribute&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceAttribute|要执行的操作，取值：**DescribeDBInstanceAttribute**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。 |
|Engine|String|否|MongoDB|数据库引擎，取值：**MongoDB**。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |
|ResourceGroupId|String|否|sg-bpxxxxxxxxxxxxxxxxxx|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C373EED9-5125-4DD9-89DB-FB1ECD2C2B4F|请求ID。 |
|DBInstances|Array of DBInstance| |实例详情信息列表。 |
|DBInstance| | | |
|ChargeType|String|PostPaid|实例的付费类型。

 -   **PrePaid**：预付费，包年包月。
-   **PostPaid**：后付费，按量付费。 |
|ConfigserverList|Array of ConfigserverAttribute| |Configserver节点信息列表。

 **说明：** 当实例类型为分片集群实例时返回该参数。 |
|ConfigserverAttribute| | | |
|ConnectString|String|mongodb://root:\*\*\*\*@dds-bpxxxxxxxxxxxxxx-cs1730-pub.mongodb.rds.aliyuncs.com:3717,|Configserver节点连接地址。 |
|MaxConnections|Integer|0|Configserver节点的最大连接数。 |
|MaxIOPS|Integer|1000|Configserver节点的最大IOPS。 |
|NodeClass|String|dds.cs.mid|Configserver节点规格。 |
|NodeDescription|String|testConfigserver|Configserver节点名称。 |
|NodeId|String|dds-bpxxxxxxxxxxxxxx-cs|Configserver节点ID。 |
|NodeStorage|Integer|20|Configserver节点的存储空间。 |
|Port|Integer|3717|Configserver节点的端口。 |
|CreationTime|String|2018-11-21T05:10:00Z|实例创建的时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|CurrentKernelVersion|String|mongodb\_20180914\_1.1.5|实例当前数据库的小版本号。 |
|DBInstanceClass|String|dds.mongo.mid|实例规格。 |
|DBInstanceDescription|String|测试|实例名称。 |
|DBInstanceId|String|dds-bpxxxxxxxx|实例ID。 |
|DBInstanceReleaseProtection|Boolean|true|是否开启了实例释放保护。返回值：

 -   **true**：开启
-   **false**：关闭 |
|DBInstanceStatus|String|Running|实例状态，详情请参见[实例状态表](~~63870~~)。 |
|DBInstanceStorage|Integer|10|实例存储空间。 |
|DBInstanceType|String|replicate|实例类型。

 -   **replicate**：副本集实例。
-   **sharding**：分片集群实例。 |
|Engine|String|MongoDB|数据库引擎。 |
|EngineVersion|String|3.4|数据库版本。 |
|ExpireTime|String|2019-04-08T16:00Z|包年包月实例的到期时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 **说明：** 当实例的付费类型为包年包月时返回该参数。 |
|KindCode|String|1|表示实例的类型。取值：

 -   **0**：物理机
-   **1**：ECS
-   **2**：DOCKER
-   **18**：k8s新架构实例 |
|LastDowngradeTime|String|2019-03-08|实例最近一次降配时间。 |
|LockMode|String|Unlock|实例的锁定状态。

 -   **Unlock**：正常，没有被锁定。
-   **ManualLock**：手动触发锁定。
-   **LockByExpiration**：实例过期自动锁定。
-   **LockByRestoration**：实例回滚前自动锁定。
-   **LockByDiskQuota**：实例空间满自动锁定。
-   **Released**：实例已释放。此时实例无法进行解锁，只能使用备份数据重新创建新实例，重建时间较长，请耐心等待。 |
|MaintainEndTime|String|03:00Z|实例可维护时间段的结束时间，格式为*HH:mm*Z（UTC时间）。 |
|MaintainStartTime|String|02:00Z|实例可维护时间段的开始时间，格式为*HH:mm*Z（UTC时间）。 |
|MaxConnections|Integer|500|实例最大连接数。 |
|MaxIOPS|Integer|1000|实例最大IOPS。 |
|MongosList|Array of MongosAttribute| |Mongos节点信息列表。

 **说明：** 当实例类型为分片集群实例时返回该参数。 |
|MongosAttribute| | | |
|ConnectSting|String|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|Mongos节点连接地址。 |
|MaxConnections|Integer|1000|Mongos节点的最大连接数。 |
|MaxIOPS|Integer|0|Mongos节点的最大IOPS。 |
|NodeClass|String|dds.mongos.mid|Mongos节点规格。 |
|NodeDescription|String|mongos1|Mongos节点名称。 |
|NodeId|String|s-bpxxxxxxxx|Mongos节点ID。 |
|Port|Integer|3717|Mongos节点连接端口。 |
|VPCId|String|vpc-bp1xxxxxxxxxxxxxxxxxx|Mongos节点的专有网络VPCID。 |
|VSwitchId|String|vsw-bp1xxxxxxxxxxxxxxxxxx|Mongos节点的交换机VSwitchID。 |
|VpcCloudInstanceId|String|s-bp1xxxxxxxxxxxxx|Mongos节点的专有网络实例ID。 |
|NetworkType|String|VPC|实例的网络类型。

 -   **Classic**：经典网络。
-   **VPC**：专有网络。 |
|ProtocolType|String|mongodb|实例的访问协议类型。返回值：

 -   **mongodb**：MongoDB协议
-   **dynamodb**：DynamoDB协议 |
|ReadonlyReplicas|String|0|实例的只读节点个数。 |
|RegionId|String|cn-hangzhou|实例所属地域ID。 |
|ReplacateId|String|bls-mxxxxxxxx|BLS通道ID。 |
|ReplicaSetName|String|mgset-10xxxxxxxx|实例的副本集名称。

 **说明：** 当实例类型为副本集实例时，返回该参数。 |
|ReplicaSets|Array of ReplicaSet| |副本集信息。

 **说明：** 当实例类型为副本集实例时，返回该参数。 |
|ReplicaSet| | | |
|ConnectionDomain|String|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|节点的连接地址。 |
|ConnectionPort|String|ConnectionPort|节点的连接端口。 |
|NetworkType|String|VPC|节点的网络类型。

 -   **Classic**：经典网络。
-   **VPC**：专有网络。 |
|ReplicaSetRole|String|Primary|节点的角色。

 -   **Primary**：主节点。
-   **Secondary**：从节点。 |
|VPCCloudInstanceId|String|vpc-xxxxxxxx|专有网络实例ID。 |
|VPCId|String|vpc-bpxxxxxxxx|节点的专有网络ID。 |
|VSwitchId|String|vsw-bpxxxxxxxx|节点的专有网络中交换机ID。 |
|ReplicationFactor|String|3|实例的节点数。

 **说明：** 当实例类型为副本集实例时返回该参数。 |
|ResourceGroupId|String|rg-axxxxxxxx|实例所属资源组ID。 |
|ShardList|Array of ShardAttribute| |Shard节点信息列表。

 **说明：** 当实例类型为分片集群实例时返回该参数。 |
|ShardAttribute| | | |
|ConnectString|String|d-bpxxxxxxxxxxxxxxxxxx.mongodb.rds.aliyuncs.com|Shard节点连接地址。 |
|MaxConnections|Integer|8000|Shard节点的最大连接数。 |
|MaxIOPS|Integer|8000|Shard节点的最大IOPS。 |
|NodeClass|String|dds.shard.mid|Shard节点规格。 |
|NodeDescription|String|testshard|Shard节点名称。 |
|NodeId|String|d-bpxxxxxxxx|Shard节点ID。 |
|NodeStorage|Integer|10|Shard节点的存储空间。 |
|Port|Integer|3717|Shard节点的端口。 |
|ReadonlyReplicas|Integer|1|Shard节点中只读节点的个数。返回值范围：**0**~**5**。

 **说明：** 当前仅中国站支持本参数。 |
|StorageEngine|String|WiredTiger|实例的存储引擎类型。 |
|Tags|Array of Tag| |实例的标签信息列表。 |
|Tag| | | |
|Key|String|test|实例的标签键。 |
|Value|String|api|实例的标签值。 |
|VPCCloudInstanceIds|String|s-bp1xxxxxxxxxxxxx|实例的专有网络实例ID。 |
|VPCId|String|vpc-bpxxxxxxxx|专有网络ID。 |
|VSwitchId|String|vsw-bpxxxxxxxx|专有网络的交换机ID。 |
|VpcAuthMode|String|Open|内网免密访问模式。

 -   **Open**：内网免密访问处于开启状态。
-   **Close**：内网免密访问处于关闭状态，需要使用密码访问。
-   **NotSupport**：不支持该功能。 |
|ZoneId|String|cn-hangzhou-b|实例所属可用区ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeDBInstanceAttribute
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

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
			      <DBInstanceDescription>测试数据库</DBInstanceDescription>
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

`JSON` 格式

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
				"DBInstanceDescription": "测试数据库",
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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

