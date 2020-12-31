# DescribeBackupDBs

在为MongoDB实例执行单库恢复前，您可以调用本接口查询指定的时间点或备份集内包含的数据库。

您可以调用[CreateDBInstance](~~61763~~)接口进行单库恢复，更多信息请参见[MongoDB单库恢复](~~112274~~)。

调用本接口时，实例必须满足以下条件：

-   实例的创建时间晚于2019年3月26日。
-   实例属于华北 1、华北 2、华北 3、华北 5、华东 1、华东 2、华南 1或亚太东南 1（新加坡）地域。
-   实例类型为副本集实例。
-   实例版本须为3.4、4.0、4.2或4.4版本（当前仅中国站支持4.4版本）。
-   实例存储引擎必须为WiredTiger。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeBackupDBs&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeBackupDBs|要执行的操作，取值：**DescribeBackupDBs**。 |
|SourceDBInstance|String|是|dds-bpxxxxxxxx|待恢复数据的源实例ID。 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的最大值，默认值为**1**。 |
|PageSize|Integer|否|30|每页可展示的记录数，取值： **30**、**50**、**100**，默认值为**30**。 |
|RestoreTime|String|否|2019-08-22T12:00:00Z|实例所需恢复的时间点，格式为yyyy-MM-ddTHH:mm:ssZ（UTC时间）。

 **说明：**

 -   本参数可取值为7天内的任意时间，但是须早于当前时间，且晚于实例的创建时间。
-   本参数和**BackupId**参数两者中必须传入一项。 |
|BackupId|String|否|5664xxxx|备份ID。

 **说明：**

-   您可以通过调用[DescribeBackups](~~62172~~)接口查询备份ID。
-   本参数和**RestoreTime**参数两者中必须传入一项。 |
|ResourceGroupId|String|否|rg-axxxxxxxxxx|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Databases|Array of Database| |数据库列表。 |
|Database| | | |
|DBName|String|mongodbtest|数据库名。 |
|PageNumber|Integer|1|页码。 |
|TotalCount|Integer|5|查询结果中数据库的数量。 |
|PageSize|Integer|30|每页可展示的记录数。 |
|RequestId|String|1AF0AD89-ED4F-44AD-B65F-BFC1D5CD9455|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeBackupDBs
&SourceDBInstance=dds-bpxxxxxxxx
&RestoreTime=2019-08-22T12:00:00Z
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeBackupDBsResponse>
	  <Databases>
		    <Database>
			      <DBName>admin</DBName>
		    </Database>
		    <Database>
			      <DBName>config</DBName>
		    </Database>
		    <Database>
			      <DBName>mongodbtest</DBName>
		    </Database>
		    <Database>
			      <DBName>db1</DBName>
		    </Database>
		    <Database>
			      <DBName>db2</DBName>
		    </Database>
	  </Databases>
	  <PageNumber>1</PageNumber>
	  <TotalCount>5</TotalCount>
	  <PageSize>30</PageSize>
	  <RequestId>1AF0AD89-ED4F-44AD-B65F-BFC1D5CD9455</RequestId>
</DescribeBackupDBsResponse>
```

`JSON` 格式

```
{
	"Databases": {
		"Database": [
			{
				"DBName": "admin"
			},
			{
				"DBName": "config"
			},
			{
				"DBName": "mongodbtest"
			},
			{
				"DBName": "db1"
			},
			{
				"DBName": "db2"
			}
		]
	},
	"PageNumber": 1,
	"TotalCount": 5,
	"PageSize": 30,
	"RequestId": "1AF0AD89-ED4F-44AD-B65F-BFC1D5CD9455"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|IncorrectDBInstanceType|Current DB instance type does not support this operation.|当前的实例类型不支持此操作。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

