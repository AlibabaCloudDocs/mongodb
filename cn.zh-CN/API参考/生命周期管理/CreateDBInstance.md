# CreateDBInstance

该接口用于创建MongoDB副本集实例，同时也可用于克隆MongoDB副本集实例。

请确保在使用该接口前，已充分了解云数据库MongoDB产品的收费方式和[价格](https://www.aliyun.com/price/product#/mongodb/detail)。

关于云数据库MongoDB实例的规格，请参见[实例规格表](~~57141~~)。

如需创建分片集群实例，可通过调用[CreateShardingDBInstance](~~61884~~)接口创建。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=CreateDBInstance&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDBInstance|要执行的操作，取值：**CreateDBInstance**。 |
|ClientToken|String|是|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。 |
|Engine|String|是|MongoDB|数据库引擎，取值：**MongoDB**。 |
|EngineVersion|String|是|4.0|数据库版本号。取值：**3.4**、**4.0**、**4.2**或**4.4**。

 **说明：** 调用此接口用于克隆实例时，数据库版本号必须和源数据库的一致。 |
|DBInstanceClass|String|是|dds.mongo.standard|实例规格，取值详情请参见[实例规格表](~~57141~~)。 |
|DBInstanceStorage|Integer|是|10|实例存储空间。

 -   取值范围：**10**~**3000**，单位为GB。
-   每10GB递增。

 **说明：** 具体取值受实例规格约束，详情请参见[实例规格表](~~57141~~)。 |
|RegionId|String|是|cn-hangzhou|地域ID，您可以通过调用[DescribeRegions](~~61933~~)查询可用的地域，使用此参数指定实例创建的地域。 |
|ZoneId|String|否|cn-hangzhou-b|可用区ID，您可以通过[DescribeRegions](~~61933~~)查看可用的可用区，使用此参数指定实例创建的可用区。 |
|DBInstanceDescription|String|否|测试数据库1|实例名称，长度为2~256个字符。以中文、英文字母开头，可以包含数字、中文、英文、下划线（\_）、短横线（-）。 |
|SecurityIPList|String|否|10.23.12.24/24|-   实例的IP白名单，以逗号隔开，不可重复，最多1000个IP。
-   支持格式：%，0.0.0.0/0，10.23.12.24（IP）或者10.23.12.24/24（CIDR模式，无类域间路由，/24表示地址前缀的长度，范围为1~32）。

 **说明：** %和0.0.0.0/0表示任何IP地址都可以访问实例的数据库，属于高危设置，请谨慎设置。 |
|AccountPassword|String|否|Alitest!159|root账号的密码。

 -   密码由大写字母、小写字母、数字、特殊字符中的至少三种组成，特殊字符为`!#$%^&*()_+-=`。
-   密码长度为8-32位。 |
|ChargeType|String|否|PrePaid|实例的付费类型，取值：

 -   **PostPaid**：后付费（按量付费）。
-   **PrePaid**：预付费（包年包月）。

 默认付费类型为按量付费。

 **说明：** 当本参数值为**PrePaid**时，还需要传入**Period**参数。 |
|Period|Integer|否|1|实例的购买时长，单位为月。取值范围为：**1**~**9**，**12**，**24**，**36**。

 **说明：** 当**ChargeType**参数值为**PrePaid**时，本参数才可用且必须传入。 |
|NetworkType|String|否|VPC|实例的网络类型，取值：

 -   **CLASSIC**：经典网络。
-   **VPC**：专有网络。

 默认网络类型为经典网络。

 **说明：** 当本参数值为**VPC**时，还需要传入**VpcId**参数和**VSwitchId**参数。 |
|VpcId|String|否|vpc-bpxxxxxxxx|专有网络（VPC）ID。

 **说明：** 当**NetworkType**参数值为**VPC**时，本参数才可用。 |
|VSwitchId|String|否|vsw-bpxxxxxxxx|虚拟交换机ID。

 **说明：** 当**NetworkType**参数值为**VPC**时，本参数才可用。 |
|SrcDBInstanceId|String|否|dds-bpxxxxxxxx|源实例ID，只有调用本接口用于克隆实例时才能传入该参数，且必须和**BackupId**或**RestoreTime**参数一同传入。 |
|BackupId|String|否|32994xxxx|具体的备份集ID，只有调用本接口用于克隆实例时才能传入该参数，且必须和**SrcDBInstanceId**参数一同传入。

 **说明：** 您可以通过调用[DescribeBackups](~~62172~~)接口查询备份集ID。 |
|RestoreTime|String|否|2019-03-13T12:11:14Z|克隆实例时所恢复的时间点，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：**

-   只有调用本接口用于克隆实例时才能传入该参数，且必须和**SrcDBInstanceId**、**BackupId**参数一同传入。
-   支持选择7天内的任一时间点进行克隆。 |
|BusinessInfo|String|否|\{“ActivityId":"000000000"\}|附加参数，业务信息。 |
|DatabaseNames|String|否|mongodbtest|数据库名。

 **说明：** 调用本接口用于克隆实例操作时，可传入该参数指定需要克隆的数据库，如不传入，则克隆实例的所有数据库。 |
|AutoRenew|String|否|true|设置实例是否自动续费，取值：

 -   **true**：自动续费。
-   **false**：不自动续费，即手动续费。

 默认为手动续费。

 **说明：** 当**ChargeType**参数值为**PrePaid**时，本参数才可用。 |
|CouponNo|String|否|youhuiquan\_promotion\_option\_id\_for\_blank|优惠码，默认为：**youhuiquan\_promotion\_option\_id\_for\_blank**。 |
|StorageEngine|String|否|WiredTiger|实例使用的存储引擎，取值为**WiredTiger**，**RocksDB**，**TerarkDB**，默认值为**WiredTiger**。关于存储引擎与版本的选择约束请参见[版本与存储引擎](~~61906~~)。

 **说明：** 调用本接口用于克隆实例时，该值必须与源实例保持一致。 |
|ReplicationFactor|String|否|3|副本集节点个数，取值：**3**，**5**，**7**。默认值为**3**。 |
|ReadonlyReplicas|String|否|1|创建只读节点的个数，取值范围为**1**-**5**。

 **说明：** 默认不传入该参数，即默认不创建只读节点。 |
|ResourceGroupId|String|否|rg-axxxxxxxx|资源组ID。 |
|ClusterId|String|否|dhg-2x7\*\*\*\*\*\*\*\*\*\*\*\*\*|专属集群ID。如果您希望在专属集群中创建MongoDB实例，需要提前在[专属集群控制台](https://cddc.console.aliyun.com/)中创建数据库引擎为MongoDB的专属集群，并在该集群中创建3台主机。详情请参见[创建集群](~~141766~~)。

 **说明：** 该参数目前仅支持中国站。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|dds-bpxxxxxxxx|实例ID。 |
|OrderId|String|2033xxxxxxxxxxxx|订单ID。 |
|RequestId|String|D8F1D721-6439-4257-A89C-F1E8E9C9624D|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=CreateDBInstance
&ClientToken=ETnLKlblzczshOTUbOCzxxxxxxxxxx
&Engine=MongoDB
&EngineVersion=4.0
&DBInstanceClass=dds.mongo.standard
&DBInstanceStorage=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateDBInstanceResponse>
	  <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
	  <OrderId>2033xxxxxxxxxxxx</OrderId>
	  <RequestId>D8F1D721-6439-4257-A89C-F1E8E9C9624D</RequestId>
</CreateDBInstanceResponse>
```

`JSON` 格式

```
{
	"DBInstanceId": "dds-bpxxxxxxxx",
	"OrderId": "2033xxxxxxxxxxxx",
	"RequestId": "D8F1D721-6439-4257-A89C-F1E8E9C9624D"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InsufficientBalance|Your account does not have enough balance.|余额不足，请您先充值后再试。|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|用户未进行实名认证，请您先进行实名认证后再试。|
|400|InvalidCapacity.NotFound|The Capacity provided does not exist in our records.|容量配置不合法，请您检查输入的参数是否正确。|
|400|IdempotentParameterMismatch|Request uses a client token in a previous request but is not identical to that request.|用了一个已经使用过的 ClientToken，但此次请求内容却又与上一次使用该 Token 的 request 不一样。|
|403|IncorrectBackupSetState|Current backup set state does not support operations.|备份集状态不支持此操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

