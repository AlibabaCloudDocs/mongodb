# DescribeDBInstances

调用DescribeDBInstances接口查询MongoDB实例列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeDBInstances&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstances|要执行的操作，取值：**DescribeDBInstances**。 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的最大值，默认值为**1**。 |
|PageSize|Integer|否|30|每页记录数，取值： **30、50、100**，默认值为**30**。 |
|DBInstanceId|String|否|dds-bpxxxxxxxx|实例ID。 |
|ReplicationFactor|String|否|3|副本集实例的节点数量，取值：**3、5、7**。 |
|DBInstanceDescription|String|否|测试数据库|实例的描述或备注信息。 |
|DBInstanceStatus|String|否|ACTIVATION|实例的状态信息，取值详情请参见[实例状态表](~~63870~~)。 |
|DBInstanceType|String|否|replicate|实例类型，取值：

 -   **sharding**：分片集群实例。
-   **replicate**：副本集实例和单节点实例，默认值为replicate。 |
|DBInstanceClass|String|否|dds.mongo.mid|实例规格，取值详情请参见[实例规格表](~~57141~~)。 |
|Engine|String|否|MongoDB|数据库引擎，取值为**MongoDB**。 |
|EngineVersion|String|否|4.0|数据库版本号。取值：**3.2**、**3.4**、**4.0**或**4.2**。 |
|NetworkType|String|否|VPC|实例网络类型，取值：

 -   **Classic**：经典网络。
-   **VPC**：VPC网络。 |
|VpcId|String|否|vpc-bpxxxxxxxx|专有网络ID。 |
|VSwitchId|String|否|vsw-bpxxxxxxxx|专有网络的交换机ID。 |
|ChargeType|String|否|PrePaid|实例付费类型，取值：

 -   **PrePaid**：预付费，包年包月。
-   **PostPaid**：按量付费。 |
|ZoneId|String|否|cn-hangzhou-b|可用区ID，您可以通过[DescribeRegions](~~61933~~)查询可用的可用区。 |
|Tag.N.Key|String|否|testdatabase|实例的标签键。N的取值范围：**1**~**20**。最多支持64个字符，不能以`aliyun`、`acs:`、`http://`或者`https://`开头。

 **说明：** 不允许传入空字符串。 |
|Tag.N.Value|String|否|apitest|实例的标签值。N的取值范围：**1**~**20**。最多支持128个字符，不能以`aliyun`、`acs`:、`http://`或者`https://`开头。

 **说明：** TagValue可以为空。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |
|ExpireTime|String|否|2019-12-26T16:00Z|实例的到期时间。 |
|Expired|String|否|true|实例过期状态，取值：

 -   **true**：已过期。
-   **false**：未过期。 |
|ConnectionDomain|String|否|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|节点的连接地址，您可以调用[DescribeDBInstanceAttribute](~~62010~~)查询。 |
|ResourceGroupId|String|否|rg-axxxxxxxx|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|页码。 |
|TotalCount|Integer|1|查询结果中实例的数量。 |
|PageSize|Integer|30|每页记录数。 |
|RequestId|String|A10B8ECB-0BA0-4EC6-93A5-C65FDEDA07CB|请求ID。 |
|DBInstances|Array of DBInstance| |实例信息列表。 |
|DBInstance| | | |
|ChargeType|String|PostPaid|实例付费类型。

 -   **PrePaid**：预付费，包年包月。
-   **PostPaid**：按量付费。 |
|CreationTime|String|2018-09-25T06:33:07Z|实例创建的时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|DBInstanceClass|String|dds.mongo.mid|实例规格。 |
|DBInstanceDescription|String|测试数据库|实例的描述或备注信息。 |
|DBInstanceId|String|dds-bpxxxxxxxx|实例ID。 |
|DBInstanceStatus|String|Running|实例状态，详情请参见[实例状态表](~~63870~~)。 |
|DBInstanceStorage|Integer|20|实例存储空间。 |
|DBInstanceType|String|sharding|实例的类型。

 -   **sharding**：分片集群实例。
-   **replicate**：副本集实例。 |
|DestroyTime|String|2019-03-05T11:26:02Z|实例数据销毁时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：**

-   包年包月实例，到期7天后会被释放，数据也会被删除且无法恢复。
-   按量付费实例，欠费超过24小时会被锁定，持续欠费7天会被释放，数据也被删除且无法恢复。 |
|Engine|String|MongoDB|数据库引擎。 |
|EngineVersion|String|4.0|实例数据库版本。 |
|ExpireTime|String|2019-11-25T16:00Z|实例到期时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。 |
|KindCode|String|1|表示实例的类型。取值：

 -   **0**：物理机
-   **1**：ECS
-   **2**：DOCKER
-   **18**：k8s新架构实例 |
|LastDowngradeTime|String|2019-03-08|实例最后一次降配时间。 |
|LockMode|String|Unlock|实例的锁定状态。

 -   **Unlock**：正常。
-   **ManualLock**：手动触发锁定。
-   **LockByExpiration**：实例过期自动锁定。
-   **LockByRestoration**：实例回滚前自动锁定。
-   **LockByDiskQuota**：实例空间满自动锁定。
-   **Released**：实例已释放。此时实例无法进行解锁，只能使用备份数据重新创建新实例，重建时间较长，请耐心等待。 |
|MongosList|Array of MongosAttribute| |Mongos节点信息列表。

 **说明：** 实例类型为分片集群实例时返回该参数。 |
|MongosAttribute| | | |
|NodeClass|String|dds.mongos.mid|Mongos节点规格。 |
|NodeDescription|String|测试mongos节点|Mongos节点描述。 |
|NodeId|String|s-bpxxxxxxxx|Mongos节点ID。 |
|NetworkType|String|VPC|实例网络类型。

 -   **Classic**：经典网络。
-   **VPC**：专有网络。 |
|RegionId|String|cn-hangzhou|实例所属地域ID。 |
|ReplicationFactor|String|3|实例中节点的个数。

 **说明：** 实例类型为副本集实例时返回该参数。 |
|ResourceGroupId|String|rg-axxxxxxxx|资源组ID。 |
|ShardList|Array of ShardAttribute| |Shard节点信息列表。

 **说明：** 实例类型为分片集群实例时返回该参数。 |
|ShardAttribute| | | |
|NodeClass|String|dds.shard.mid|Shard节点的实例规格。 |
|NodeDescription|String|测试shard节点|Shard节点描述。 |
|NodeId|String|d-bpxxxxxxxx|Shard节点ID。 |
|NodeStorage|Integer|20|Shard节点的存储空间，单位为GB。 |
|ReadonlyReplicas|Integer|1|Shard节点中只读节点的个数。返回值范围：**0**~**5**。

 **说明：** 当前仅中国站支持本参数。 |
|Tags|Array of Tag| |资源标签信息列表。 |
|Tag| | | |
|Key|String|test|资源的标签键。 |
|Value|String|api|资源的标签值。 |
|VpcAuthMode|String|Close|是否开启了专有网络免密访问功能，返回值：

 -   **Open**：开启。
-   **Close**：关闭。 |
|ZoneId|String|cn-hangzhou-b|实例所属可用区ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeDBInstances
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<PageNumber>1</PageNumber>
<TotalCount>1</TotalCount>
<PageSize>30</PageSize>
<RequestId>D1FF92B8-3714-4182-BA0B-D04F917F0463</RequestId>
<DBInstances>
    <DBInstance>
        <ChargeType>PostPaid</ChargeType>
        <LockMode>Unlock</LockMode>
        <DBInstanceClass>dds.mongo.logic</DBInstanceClass>
        <ResourceGroupId>rg-acxxxxxxxx</ResourceGroupId>
        <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
        <ZoneId>cn-hangzhou-i</ZoneId>
        <MongosList>
            <MongosAttribute>
                <NodeId>s-bpxxxxxxxx</NodeId>
                <NodeClass>dds.mongos.mid</NodeClass>
            </MongosAttribute>
            <MongosAttribute>
                <NodeId>s-bpxxxxxxxx</NodeId>
                <NodeClass>dds.mongos.mid</NodeClass>
            </MongosAttribute>
        </MongosList>
        <DBInstanceDescription>testdata</DBInstanceDescription>
        <Engine>MongoDB</Engine>
        <CreationTime>2019-11-23T03:08:01Z</CreationTime>
        <Tags>
        </Tags>
        <NetworkType>VPC</NetworkType>
        <ExpireTime>2999-09-08T16:00Z</ExpireTime>
        <DBInstanceType>sharding</DBInstanceType>
        <RegionId>cn-hangzhou</RegionId>
        <ShardList>
            <ShardAttribute>
                <NodeId>d-bpxxxxxxxx</NodeId>
                <NodeClass>dds.shard.standard</NodeClass>
                <NodeStorage>10</NodeStorage>
            </ShardAttribute>
            <ShardAttribute>
                <NodeId>d-bpxxxxxxxx</NodeId>
                <NodeClass>dds.shard.standard</NodeClass>
                <NodeStorage>10</NodeStorage>
            </ShardAttribute>
        </ShardList>
        <EngineVersion>4.2</EngineVersion>
        <DBInstanceStatus>Running</DBInstanceStatus>
    </DBInstance>
</DBInstances>
```

`JSON` 格式

```
{
	"PageNumber": 1,
	"TotalCount": 1,
	"PageSize": 30,
	"RequestId": "D1FF92B8-3714-4182-BA0B-D04F917F0463",
	"DBInstances": {
		"DBInstance": [
			{
				"ChargeType": "PostPaid",
				"LockMode": "Unlock",
				"DBInstanceClass": "dds.mongo.logic",
				"ResourceGroupId": "rg-acxxxxxxxx",
				"DBInstanceId": "dds-bpxxxxxxxx",
				"ZoneId": "cn-hangzhou-i",
				"MongosList": {
					"MongosAttribute": [
						{
							"NodeId": "s-bpxxxxxxxx",
							"NodeClass": "dds.mongos.mid"
						},
						{
							"NodeId": "s-bpxxxxxxxx",
							"NodeClass": "dds.mongos.mid"
						}
					]
				},
				"DBInstanceDescription": "testdata",
				"Engine": "MongoDB",
				"CreationTime": "2019-11-23T03:08:01Z",
				"Tags": {
					"Tag": []
				},
				"NetworkType": "VPC",
				"ExpireTime": "2999-09-08T16:00Z",
				"DBInstanceType": "sharding",
				"RegionId": "cn-hangzhou",
				"ShardList": {
					"ShardAttribute": [
						{
							"NodeId": "d-bpxxxxxxxx",
							"NodeClass": "dds.shard.standard",
							"NodeStorage": 10
						},
						{
							"NodeId": "d-bpxxxxxxxx",
							"NodeClass": "dds.shard.standard",
							"NodeStorage": 10
						}
					]
				},
				"EngineVersion": "4.2",
				"DBInstanceStatus": "Running"
			}
		]
	}
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

