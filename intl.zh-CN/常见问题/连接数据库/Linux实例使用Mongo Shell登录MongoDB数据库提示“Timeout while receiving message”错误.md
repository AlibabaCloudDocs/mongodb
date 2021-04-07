# 排查Mongo Shell登录问题

您可以通过DMS或Mongo Shell登录MongoDB数据库，本文介绍使用Mongo Shell登录数据库时出现的典型问题及解决方法。

## 提示connection attempt failed错误

现象：

```
#mongo --host ali12345678.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -p xxx
MongoDB shell version: 3.2.3
DB Prefix:
connecting to: 10.1.2.8:3717/admin
2016-05-31T15:25:58.940+0800 W NETWORK  Failed to connect to 10.*.*.8:3717 after 5000 milliseconds, giving up.
2016-05-31T15:25:58.943+0800 E QUERY    Error: couldn't connect to server 10.*.*.8:3717 (10.1.2.8), connection attempt failed
    at connect (src/mongo/shell/mongo.js:181:14)
    at (connect):1:6 at src/mongo/shell/mongo.js:181
exception: connect failed
```

|可能的原因|解决方法|
|:----|:---|
|执行Mongo Shell命令的ECS与MongoDB实例不在同一个专有网络或网络类型不一致。|-   不在同一专有网络时：将MongoDB实例的网络类型切换为经典网络，然后再切换回专有网络。

**说明：** 切换回专有网络时选择和ECS实例相同的专有网络即可。

-   网络类型不同时：详情请参见[ECS实例与MongoDB实例网络类型不同时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md)。 |

辅助排查方法：可以通过telnet来确认到达MongoDB实例的网络是否通畅，例如`telnet dds-ali123456789.mongodb.rds.aliyuncs.com 3717`

![测试端口](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1774797951/p34454.png)

图中示例表示可以正常解析该域名地址，且3717端口可正常通信。

## 提示Authentication failed错误

现象：

```
#mongo --host ali12345678.mongodb.rds.aliyuncs.com:3717  --authenticationDatabase admin -u root -p xxx
MongoDB shell version: 3.2.3
connecting to: 10.1.2.8:3717/test
2016-05-31T15:50:18.623+0800 E QUERY    Error: 18 Authentication failed.
    at DB._authOrThrow (src/mongo/shell/db.js:1271:32)
    at (auth):6:8
    at (auth):7:2 at src/mongo/shell/db.js:1271
exception: login failed
```

|可能的原因|解决方法|
|:----|:---|
|登录数据库用户名错误。|使用正确的数据库用户名登录。|
|登录数据库的密码错误。|使用正确的数据库密码登录，如忘记密码，您在控制台[重置root用户的数据库密码](/intl.zh-CN/用户指南/账号管理/重置密码.md)。|
|连接的用户跟鉴权数据库不匹配|用户需要和鉴权数据库对应，例如root用户是admin数据库下的用户，使用root连接时，必须指定鉴权数据库为admin。|
|客户端版本过低|Mongo Shell版本必须3.0及以上的版本，安装步骤请参见官方文档 [Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。其他语言客户端的版本要求请参见[Driver兼容性文档](https://docs.mongodb.com/ecosystem/drivers/driver-compatibility-reference/)。|

## 提示运行isMaster命令出现网络错误

现象：

```
#mongo --host ali12345678.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase test -u root -p xxxxxx
MongoDB shell version v3.4.10
connecting to: mongodb:ali1234567878.mongodb.rds.aliyuncs.com:3717/
2018-12-18T14:26:11.946+0800 E QUERY    [thread1] Error: network error while attempting to run command 'isMaster' on host 'ft12345678.mongodb.rds.aliyuncs.com:3717'  :
connect@src/mongo/shell/mongo.js:237:13
@(connect):1:6
exception: connect failed
```

|可能的原因|解决方法|
|:----|:---|
|ECS的IP地址没有加入到MongoDB实例白名单中|将ECS的IP地址加入MongoDB实例的白名单中，详情请参见[设置白名单](/intl.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。|

## 提示Timeout while receiving message信息

```
org.springframework.data.mongodb.UncategorizedMongoDbException: Timeout while receiving message; nested exception is com.mongodb.MongoSocketReadTimeoutException: Timeout while receiving message
```

|可能的原因|解决方法|
|:----|:---|
|异常的慢查询占用实例资源，导致CPU使用率激增甚至到达峰值。|检查是否有慢查询，建议进行添加索引优化。具体方法请参见[分析数据库慢请求](/intl.zh-CN/最佳实践/性能/排查MongoDB CPU使用率高的问题.md)。|
|应用端连接池的配置错误引起，如超时时间的设置等。|详情请参见如何[查询及限制连接数](/intl.zh-CN/常见问题/热点问题/如何查询及限制MongoDB实例的连接数.md)。|

## 常见的连接场景

-   [如何通过公网连接MongoDB实例](/intl.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md)
-   [ECS实例与MongoDB实例地域不同时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同时如何连接.md)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md)

