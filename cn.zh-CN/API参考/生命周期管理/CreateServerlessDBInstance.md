# CreateServerlessDBInstance

调用CreateServerlessDBInstance接口创建MongoDB Serverless版实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=CreateServerlessDBInstance&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateServerlessDBInstance|要执行的操作，取值：**CreateServerlessDBInstance**。 |
|AccountPassword|String|是|Abc12345|数据库登录账号对应的密码。

 -   密码长度为8~32位。
-   密码至少由大写字母、小写字母、数字、特殊字符中的任意三种组成，特殊字符为`!#$%^&*()_+-=`

**说明：** MongoDB Serverless实例提供一个默认的数据库登录账号，该账号无法被修改，您仅可以设置或修改该账号对应的密码。 |
|DBInstanceStorage|Integer|是|1|实例存储空间。

 -   取值范围：**1**~**10**，单位为GB。
-   每1GB递增。 |
|Engine|String|是|MongoDB|数据库引擎，取值：**MongoDB**。 |
|EngineVersion|String|是|4.2|数据库版本号，固定为**4.2**。 |
|RegionId|String|是|ap-southeast-1|地域ID，您可以通过调用[DescribeRegions](~~61933~~)查询可用的地域，使用此参数指定实例创建的地域。 |
|ZoneId|String|否|ap-southeast-1c|可用区ID，您可以通过调用[DescribeRegions](~~61933~~)查询可用的可用区，使用此参数指定实例创建的可用区。 |
|DBInstanceDescription|String|否|测试数据库1|实例名称，长度为2~256个字符。以中文、英文字母开头，可以包含数字、中文、英文、下划线（\_）、短横线（-）。 |
|SecurityIPList|String|否|10.23.12.24/24|实例的IP白名单。

 -   以逗号隔开，不可重复，最多1000个IP。
-   支持格式：%，0.0.0.0/0，10.23.12.24（IP）或者10.23.12.24/24（CIDR模式，无类域间路由，/24表示地址前缀的长度，范围为1~32）。

**说明：** %和0.0.0.0/0表示任何IP地址都可以访问实例的数据库，属于高危设置，请谨慎设置。 |
|ChargeType|String|否|PrePaid|实例的付费类型，仅支持预付费模式（包年包月），取值：**PrePaid**。 |
|Period|Integer|否|1|实例的购买时长，单位为月。取值范围为：**1**~**9**、**12**、**24**、**36**、**60**。 |
|NetworkType|String|否|VPC|实例的网络类型，Serverless实例仅支持专有网络类型，取值：**VPC**。 |
|VpcId|String|否|vpc-bpxxxxxxxx|专有网络（VPC）ID。 |
|VSwitchId|String|否|vsw-bpxxxxxxxx|专有网络中的虚拟交换机ID。 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。 |
|StorageEngine|String|否|WiredTiger|实例使用的存储引擎，取值固定为**WiredTiger**。关于存储引擎与版本的选择约束请参见[版本与存储引擎](~~61906~~)。 |
|AutoRenew|String|否|true|设置实例是否自动续费，取值：

 -   **true**：自动续费。
-   **false**：不自动续费，即需要手动续费。

默认为手动续费。 |
|ResourceGroupId|String|否|rg-axxxxxxxx|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|dds-t4nxxxxxxxxxx|实例ID。 |
|OrderId|String|2033xxxxxxxxxxxx|订单ID。 |
|RequestId|String|7A9807F0-1301-4154-9849-6497E94A04DB|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=CreateServerlessDBInstance
&AccountPassword=Abc12345
&DBInstanceStorage=1
&Engine=MongoDB
&EngineVersion=4.2
&RegionId=ap-southeast-1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>7A9807F0-1301-4154-9849-6497E94A04DB</RequestId>
<DBInstanceId>dds-t4nxxxxxxxxxx</DBInstanceId>
<OrderId>2033xxxxxxxxxxxx</OrderId>
```

`JSON` 格式

```
{
    "RequestId":"7A9807F0-1301-4154-9849-6497E94A04DB",
    "DBInstanceId":"dds-t4nxxxxxxxxxx",
    "OrderId":"2033xxxxxxxxxxxx"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

