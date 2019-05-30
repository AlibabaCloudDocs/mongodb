# DescribeBackups {#doc_api_Dds_DescribeBackups .reference}

调用DescribeBackups接口查询MongoDB实例的备份列表。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeBackups)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeBackups|要执行的操作，取值：**DescribeBackups**。

 |
|StartTime|String|是|2019-03-12T12:00Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|EndTime|String|是|2019-03-13T12:00Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|BackupId|String|否|5664xxxx|备份ID。

 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的的最大值，默认值为**1**。

 |
|PageSize|Integer|否|30|每页记录数，取值： **30、50、100**，默认值为**30**。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|页码。

 |
|PageSize|Integer|30|每页记录数。

 |
|RequestId|String|8925E66F-1971-4C8C-90A7-F93BF1867E25|请求ID。

 |
|TotalCount|Integer|1|备份总个数。

 |
|Backups| | |备份文件详情列表。

 |
|└BackupDBNames|String|mongodbtest,new,test|备份的数据库名。

 |
|└BackupDownloadURL|String|http://xxxxx.oss-cn-hangzhou.aliyuncs.com/xxxxx/hinsxxxxx\_data\_xxxxx.tar.gz|备份文件的外网下载地址，若当前不可下载，则为空字符串。

 |
|└BackupEndTime|String|2019-03-13T04:34:57Z|本次备份结束时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└BackupId|Integer|11111111|备份ID。

 |
|└BackupIntranetDownloadURL|String|http://xxxxx.oss-cn-hangzhou-internal.aliyuncs.com/xxxxx/xxxxx.tar.gz|备份文件的内网下载地址。

 **说明：** 您可以在和此MongoDB实例连通的ECS（二者需属于同地域的经典网络或者在同一VPC内）上使用该地址下载目标备份文件。

 |
|└BackupMethod|String|Physical|备份方式。

 -   **Snapshot**：快照备份。
-   **Physical**：物理备份。
-   **Logical**：逻辑备份。

 |
|└BackupMode|String|Automated|备份模式。

 -   **Automated**：系统自动备份。
-   **Manual**：手动备份。

 |
|└BackupSize|Long|335520510|备份文件大小，单位为Byte。

 |
|└BackupStartTime|String|2019-03-13T04:32:42Z|本次备份开始时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└BackupStatus|String|Success|备份状态。

 -   **Success**：备份成功。
-   **Failed**：备份失败。

 |
|└BackupType|String|FullBackup|备份类型。

 -   **FullBackup**：全量备份。
-   **IncrementalBackup**：增量备份。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeBackups
&StartTime=2019-03-12T12:00Z
&EndTime=2019-03-13T12:00Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeBackupsResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>30</PageSize>
  <RequestId>09308D8E-136C-4053-89D8-51350248C31B</RequestId>
  <Backups>
    <Backup>
      <BackupDownloadURL>http://xxxxx.oss-cn-hangzhou.aliyuncs.com/xxxxx/xxxxx.tar.gz</BackupDownloadURL>
      <BackupIntranetDownloadURL>http://xxxxx.oss-cn-hangzhou-internal.aliyuncs.com/xxxxx/xxxxx.tar.gz</BackupIntranetDownloadURL>
      <BackupType>FullBackup</BackupType>
      <BackupDBNames>mongousertest</BackupDBNames>
      <BackupEndTime>2019-05-27T14:27:11Z</BackupEndTime>
      <BackupMethod>Physical</BackupMethod>
      <BackupMode>Automated</BackupMode>
      <BackupSize>25849856</BackupSize>
      <BackupStatus>Success</BackupStatus>
      <BackupStartTime>2019-05-27T14:24:55Z</BackupStartTime>
      <BackupId>11111</BackupId>
    </Backup>
  </Backups>
</DescribeBackupsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":30,
	"RequestId":"09308D8E-136C-4053-89D8-51350248C31B",
	"Backups":{
		"Backup":[
			{
				"BackupDownloadURL":"http://xxxxx.oss-cn-hangzhou.aliyuncs.com/xxxxx/xxxxx.tar.gz",
				"BackupIntranetDownloadURL":"http://xxxxx.oss-cn-hangzhou-internal.aliyuncs.com/xxxxx/xxxxx.tar.gz",
				"BackupType":"FullBackup",
				"BackupDBNames":"mongousertest",
				"BackupEndTime":"2019-05-27T14:27:11Z",
				"BackupMode":"Automated",
				"BackupMethod":"Physical",
				"BackupStatus":"Success",
				"BackupSize":25849856,
				"BackupId":11111,
				"BackupStartTime":"2019-05-27T14:24:55Z"
			}
		]
	}
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

