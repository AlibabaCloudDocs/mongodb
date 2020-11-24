# 通过Mongo Shell连接MongoDB Serverless版实例

Mongo Shell是MongoDB数据库自带的数据库管理工具，您可以在本地或ECS上安装Mongo Shell工具，然后通过Mongo Shell连接Serverless实例。

-   为保障鉴权成功，请安装与MongoDB实例版本相对应的Mongo Shell版本。安装步骤请参见官方文档[Install MongoDB](https://docs.mongodb.com/manual/installation/)（请根据您的客户端版本在页面左上角选择版本号）。
-   已将客户端的IP地址加入到MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/Serverless版快速入门/设置白名单.md)。

    **说明：** 如需通过公网连接MongoDB实例，需要[申请公网连接地址](/cn.zh-CN/Serverless版快速入门/申请公网连接地址.md)。


## 操作步骤

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**Serverless实例列表**。

4.  找到目标实例，单击实例ID。

5.  在**基本信息**页面的**连接信息**区域，获取连接地址。

    ![连接地址](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5215322061/p171187.png)

6.  在安装有Mongo Shell的本地服务器或ECS中通过如下命令连接实例。

    ```
    mongo "<连接串地址>"
    ```

    **说明：**

    -   双引号须为英文双引号（""）。
    -   <连接串地址\>：实例的ConnectionStringURI地址。

        ConnectionStringURI或ReadOnly ConnectionStringURI地址中的`****`需要替换为数据库密码。如您丢失数据库密码请[重置密码](/cn.zh-CN/Serverless版快速入门/重置密码.md)。

    示例：

    ```
    mongo "mongodb://user******:****@dds-t4n*******-pub.mongodb.singapore.rds.aliyuncs.com:3717/admin"
    ```


## 常见的连接场景

-   [如何通过公网连接MongoDB实例](/cn.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md)
-   [ECS实例与MongoDB实例地域不同时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同时如何连接.md)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md)

## 相关问题

-   [排查 Mongo Shell 登录问题](/cn.zh-CN/常见问题/热点问题/Linux实例使用Mongo Shell登录MongoDB数据库提示“Timeout while receiving message”错误.md)
-   [排查因连接数耗尽导致的数据库连接问题](/cn.zh-CN/常见问题/热点问题/MongoDB实例连接数耗尽导致数据库连接失败.md)
-   [排查 MongoDB CPU使用率高的问题](/cn.zh-CN/最佳实践/性能/排查MongoDB CPU使用率高的问题.md)
-   [如何查询及限制连接数](/cn.zh-CN/常见问题/热点问题/如何查询及限制MongoDB实例的连接数.md)

