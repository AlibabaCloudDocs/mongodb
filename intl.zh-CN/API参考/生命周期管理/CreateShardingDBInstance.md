# CreateShardingDBInstance {#doc_api_Dds_CreateShardingDBInstance .reference}

调用CreateShardingDBInstance接口创建或者克隆MongoDB分片集群实例。

 **请确保在使用该接口前，已充分了解云数据库MongoDB产品的收费方式和[价格](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing)。** 

关于云数据库MongoDB实例的规格，请参见[实例规格表](~~57141~~)。

如需创建副本集实例，可通过调用[CreateDBInstance](~~61763~~)接口创建。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=CreateShardingDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateShardingDBInstance|要执行的操作，取值： **CreateShardingDBInstance**。

 |
|Engine|String|是|MongoDB|数据库引擎，取值：**MongoDB**。

 |
|EngineVersion|String|是|4.0|数据库版本号，取值：**3.4**或**4.0**。

 **说明：** 

 -   关于存储引擎与版本的选择约束请参考[版本与存储引擎](~~61906~~)。
-   调用本接口用于克隆实例时，该值必须与源实例保持一致。

 |
|AccountPassword|String|是|Alitest!159|root账号的密码。

 -   密码由大写字母、小写字母、数字、特殊字符中的至少三种组成，特殊字符为!\#$%^&\*\(\)\_+-=
-   密码长度为8-32位

 |
|RegionId|String|是|cn-hangzhou|地域ID，您可以可调用[DescribeRegions](~~61933~~)查询可用的地域，使用此参数指定实例创建的地域。

 |
|ZoneId|String|否|cn-hangzhou-b|可用区ID，您可以通过[DescribeRegions](~~61933~~)查询可用的可用区，使用此参数指定实例创建的可用区。

 |
|DBInstanceDescription|String|否|测试数据库1|实例名称，长度为2~256个字符。以中文、英文字母开头，可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 |
|SecurityIPList|String|否|10.23.12.24/24|-   实例的IP白名单，以逗号隔开，不可重复，最多1000个IP。
-   支持格式：%，0.0.0.0/0，10.23.12.24（IP）或者10.23.12.24/24（CIDR模式，无类域间路由，/24表示地址前缀的长度，范围为1~32。

 **说明：** %和0.0.0.0/0表示任何IP地址都可以访问实例的数据库，属于高危设置，请谨慎设置。

 |
|ChargeType|String|否|PrePaid|实例的付费类型，取值：

 -   PostPaid：后付费（按量付费）。
-   PrePaid：预付费（包年包月）。

 默认付费类型为按量付费。

 **说明：** 当本参数值为**PrePaid**时，还需要传入**Period**参数。

 |
|Period|Integer|否|1|实例的购买时长，单位为月。取值范围为：**1**~**9**，**12**，**24**，**36**。

 **说明：** 当**ChargeType**参数值为**PrePaid**时，本参数才可用。

 |
|NetworkType|String|否|VPC|实例的网络类型。 默认创建经典网络类型的实例。

 -   **CLASSIC**：经典网络。
-   **VPC**：专有网络。

 **说明：** 当本参数值为**VPC**时，还需要传入**VpcId**参数和**VSwitchId**参数。

 |
|VpcId|String|否|vpc-bpxxxxxxxx|专有网络（VPC）ID。

 **说明：** 当**NetworkType**参数值为**VPC**时，本参数才可用。

 |
|Mongos.N.Class|String|否|dds.mongos.standard|Mongos节点的规格，取值详情请参见[实例规格表](~~57141~~)。

 **N**代表的是传入第几个Mongos节点的规格，例如：

 -   **Mongos.1.Class**表示传入第一个Mongos节点规格。
-   **Mongos.2.Class**表示传入第二个Mongos节点规格。

 **说明：** 可传入的Mongos节点数量为2~32个。

 |
|ReplicaSet.N.Class|String|否|dds.shard.standard|Shard节点的规格，取值详情请参见[实例规格表](~~57141~~)。

 **N**代表的是传入第几个Shard节点的规格，例如：

 -   **ReplicaSet.1.Class**表示传入第一个Shard节点规格。
-   **ReplicaSet.2.Class**表示传入第二个Shard节点规格。

 **说明：** 可传入的Shard节点数量为2~32个。

 |
|ReplicaSet.N.Storage|Integer|否|20|Shard节点的存储空间。

 -   取值范围：**10**~**2000**，单位为GB。
-   每10GB递增。

 **说明：** 具体取值受实例规格约束，详情请参考[实例规格表](~~57141~~)。

 **N**代表的是传入第几个Shard节点的存储空间，例如：

 -   **ReplicaSet.1.Storage**表示传入第一个Shard节点的存储空间。
-   **ReplicaSet.2.Storage**表示传入第二个Shard节点的存储空间。

 |
|ConfigServer.N.Class|String|否|dds.cs.mid|CongfigServer的规格，取值：**dds.cs.mid**。

 **说明：** 规格固定为1核2GB规格，数量固定为1个，例如：传入**ConfigServer.1.Class**参数，取值为**dds.cs.mid**。

 |
|ConfigServer.N.Storage|Integer|否|20|CongfigServer的存储空间，取值：**20**。

 **说明：** 存储空间取值固定为20GB。传入**ConfigServer.1.Storage**参数，取值为**20**。

 |
|VSwitchId|String|否|vsw-bpxxxxxxxx|虚拟交换机ID。

 **说明：** 当**NetworkType**参数值为**VPC**时，本参数才可用。

 |
|SrcDBInstanceId|String|否|dds-bpxxxxxxxx|源实例ID，只有调用本接口用于克隆实例时才能传入该参数，且必须和**RestoreTime**参数一同传入。

 |
|RestoreTime|String|否|2019-03-08T02:30:25Z|克隆实例时所恢复的时间点，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 只有调用本接口用于克隆实例时才能传入该参数，且必须和**SrcDBInstanceId**参数一同传入。

 **说明：** 支持选择7天内的任一时间点进行克隆。

 |
|StorageEngine|String|否|WiredTiger|实例使用的存储引擎，取值为**WiredTiger**，**RocksDB**，**TerarkDB**，默认值为WiredTiger。关于存储引擎与版本的选择约束请参考[版本与存储引擎](~~61906~~)。

 **说明：** 调用本接口用于克隆实例时，该值必须与源实例保持一致。

 |
|AutoRenew|String|否|true|设置实例是否自动续费，取值：

 -   **true**：自动续费。
-   **false**：不自动续费，即手动续费。

 默认为手动续费。

 **说明：** 当**ChargeType**参数值为**PrePaid**时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|dds-bpxxxxxxxx|实例ID。

 |
|OrderId|String|2033xxxxxxxxxxxx|订单ID。

 |
|RequestId|String|D8F1D721-6439-4257-A89C-F1E8E9C9623D|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=CreateShardingDBInstance
&Engine=MongoDB
&EngineVersion=4.0
&AccountPassword=Alitest!159
&ZoneId=cn-hangzhou-b
&ClientToken=ETnLKlblzczshOTUbOCzxxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateDBInstanceResponse>
  <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
  <OrderId>2033xxxxxxxxxxxx</OrderId>
  <RequestId>D8F1D721-6439-4257-A89C-F1E8E9C9623D</RequestId>
</CreateDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"D8F1D721-6439-4257-A89C-F1E8E9C9623D",
	"OrderId":"2033xxxxxxxxxxxx",
	"DBInstanceId":"dds-bpxxxxxxxx"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

