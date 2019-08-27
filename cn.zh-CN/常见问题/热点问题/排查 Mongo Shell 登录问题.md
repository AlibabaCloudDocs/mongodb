# 排查 Mongo Shell 登录问题 {#concept_fyp_rkd_lfb .concept}

您可以通过DMS或 Mongo Shell 登陆MongoDB数据库，本文介绍使用 Mongo Shell 登陆数据库时出现的典型问题及解决方法。

## 提示connection attempt failed错误 {#section_iwx_xkd_lfb .section}

现象：

```
#mongo --host ali12345678.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -p xxx
MongoDB shell version: 3.2.3
DB Prefix:
connecting to: 10.1.2.8:3717/admin
2016-05-31T15:25:58.940+0800 W NETWORK  Failed to connect to 10.1.2.8:3717 after 5000 milliseconds, giving up.
2016-05-31T15:25:58.943+0800 E QUERY    Error: couldn't connect to server 10.1.2.8:3717 (10.1.2.8), connection attempt failed
    at connect (src/mongo/shell/mongo.js:181:14)
    at (connect):1:6 at src/mongo/shell/mongo.js:181
exception: connect failed
```

|可能的原因|解决方法|
|:----|:---|
|执行 Mongo Shell 命令的ECS与MongoDB实例不在同一个可用区。|详情请参考[MongoDB跨可用区内网访问实例](../../../../intl.zh-CN/用户指南/连接实例/MongoDB跨可用区内网访问实例.md#)。|
|执行 Mongo Shell 命令的ECS与MongoDB实例不在同一个VPC网络。|

辅助排查方法：可以通过telnet来确认到达MongoDB实例的网络是否通畅，例如`telnet dds-ali123456789.mongodb.rds.aliyuncs.com 3717`

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6847/154520085334454_zh-CN.png)

图中示例表示可以正常解析该域名地址，且3717端口可正常通信。

## 提示Authentication failed错误 {#section_ih5_5xd_lfb .section}

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
|登录数据库的密码错误。|使用正确的数据库密码登录，如忘记密码，您在控制台[重置root用户的数据库密码](../../../../intl.zh-CN/用户指南/账号管理/重置密码.md#)。|
|连接的用户跟鉴权数据库不匹配|用户需要和鉴权数据库对应，比如root用户是admin数据库下的用户，使用root连接时，必须指定鉴权数据库为admin。|
|客户端版本过低|Mongo Shell 版本必须3.0及以上的版本，安装步骤请参考官方文档 [Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。其他语言客户端的版本要求请参考[Driver兼容性文档](https://docs.mongodb.com/ecosystem/drivers/driver-compatibility-reference/)。|

## 提示运行 isMaster 命令出现网络错误 {#section_op3_xjx_dgb .section}

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
|ECS的IP地址没有加入到MongoDB实例白名单中|将ECS的IP地址加入MongoDB实例的白名单中，详情请参见[设置白名单](../../../../intl.zh-CN/用户指南/数据安全性/设置白名单.md#)。|

## 提示Timeout while receiving message信息 {#section_wgt_p3x_dgb .section}

```
org.springframework.data.mongodb.UncategorizedMongoDbException: Timeout while receiving message; nested exception is com.mongodb.MongoSocketReadTimeoutException: Timeout while receiving message
```

|可能的原因|解决方法|
|:----|:---|
|异常的慢查询占用实例资源，导致CPU使用率激增甚至到达峰值。|检查是否有慢查询，建议进行添加索引优化。具体方法请参考[分析数据库慢请求](../../../../intl.zh-CN/最佳实践/排查 MongoDB CPU使用率高的问题.md#)。|
|应用端连接池的配置错误引起，如超时时间的设置等。|详情请参考如何[查询及限制连接数](intl.zh-CN/产品使用问题/如何查询及限制连接数.md#)。|

