# DescribeBackupDBs

You can call this operation to query the databases at a specified time or the databases in a specified backup set before you restore a database for an ApsaraDB for MongoDB instance.

You can call the [CreateDBInstance](~~61763~~) operation to restore a single database. For more information, see [Restore data to a new ApsaraDB for MongoDB instance](~~112274~~).

Before you call this operation, make sure that the following requirements are met:

-   The instance was created after March 26, 2019.
-   The instance is located in the China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou\), China \(Hohhot\), China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), or Singapore region. Other regions are not supported.
-   The instance is a replica set instance.
-   The version of the database engine is 3.4, 4.0, or 4.2.
-   The storage engine of the instance is WiredTiger.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeBackupDBs&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeBackupDBs|The operation that you want to perform. Set the value to **DescribeBackupDBs**. |
|SourceDBInstance|String|Yes|dds-bpxxxxxxxx|The ID of the source instance. |
|PageNumber|Integer|No|1|The number of the page to return. The value must be an integer that is larger than 0. Default value: **1**. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30**, **50**, and **100**. Default value: **30**. |
|RestoreTime|String|No|2019-08-22T12:00:00Z|The point in time to which the instance is restored. Specify the time in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

 **Note:**

 -   It can be any time within the past seven days. The time must be earlier than the current time, but later than the time when the database was created.
-   You must specify one of the RestoreTime and **BackupId** parameters. |
|BackupId|String|No|5664xxxx|The ID of the backup.

 **Note:**

-   You can call the [DescribeBackups](~~62172~~) to query the backup ID.
-   You must specify one of the **RestoreTime** and BackupId parameters. |
|ResourceGroupId|String|No|rg-axxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Databases|Array of Database| |Details about the databases. |
|Database| | | |
|DBName|String|mongodbtest|The name of the database. |
|PageNumber|Integer|1|The page number of the returned page. |
|TotalCount|Integer|5|The number of databases. |
|PageSize|Integer|30|The number of entries returned per page. |
|RequestId|String|1AF0AD89-ED4F-44AD-B65F-BFC1D5CD9455|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeBackupDBs
&SourceDBInstance=dds-bpxxxxxxxx
&RestoreTime=2019-08-22T12:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|IncorrectDBInstanceType|Current DB instance type does not support this operation.|The error message returned because the operation is not supported by the current instance type.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

