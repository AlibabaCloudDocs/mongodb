# Serverless实例连接说明

MongoDB Serverless版实例提供高可用数据库连接地址。本文介绍该连接地址的获取方式和连接说明。

## 获取数据库连接地址

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**Serverless实例列表**。

4.  找到目标实例，单击实例ID。

5.  在左侧导航栏，单击**数据库连接**，查看数据库连接信息。

    ![查看数据库连接信息](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8215322061/p170985.png)


## 连接地址说明

|项目|说明|
|:-|:-|
|地址类型|-   专有网络连接地址：专有网络是一种隔离的网络环境，安全性和性能均高于传统的经典网络。 MongoDB Serverless版实例仅提供专有网络连接地址，专有网络拥有更高的安全性和性能。
-   公网连接地址：由于通过公网连接实例存在一定的安全风险，MongoDB Serverless版实例默认未提供公网连接地址。如果您要使用阿里云以外的设备（例如本地设备）连接MongoDB Serverless版实例，您可以手动[申请公网连接地址](/cn.zh-CN/Serverless版快速入门/申请公网连接地址.md)。 |
|连接地址|连接地址的格式如下。 ```
<host>:<port>
```

-   <host\>：登录MongoDB数据库的域名地址。
-   <port\>：登录MongoDB数据库的端口。 |
|ConnectionstringURI连接地址|ConnectionstringURI连接地址格式如下。 ```
mongodb://[username:password@]host[:port][/[database][?options]]
```

-   mongodb://：前缀，代表这是一个Connection String URI连接地址。
-   username:password@：连接MongoDB实例的用户名和密码，使用英文冒号（:）分隔。
-   host:port：实例的连接地址和端口号。
-   /database：鉴权数据库名，即数据库账号所属的数据库。
-   ?options：指定额外的连接选项。 |

## 登录MongoDB数据库

1.  获取了上述的[数据库连接地址](#section_e2o_ajm_d6k)后，您还需要获取下述信息：

    -   MongoDB Serverless版实例的数据库账号，由系统默认提供。 获取方法：
        1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
        2.  在页面左上角，选择实例所在的资源组和地域。
        3.  在左侧导航栏，单击**Serverless实例列表**。
        4.  找到目标实例，单击实例ID。
        5.  在**基本信息**页面的**连接信息**区域，查看系统提供的**账号名**。
    -   登录数据库的密码，如密码遗失可以[重置密码](/cn.zh-CN/Serverless版快速入门/重置密码.md)。
    -   鉴权数据库名，即数据库账号所属的数据库。如果使用系统提供的初始账号，则对应的数据库名为admin。
2.  登录MongoDB数据库。

    -   [通过Mongo Shell连接MongoDB Serverless版实例](/cn.zh-CN/Serverless版快速入门/连接实例/通过Mongo Shell连接MongoDB Serverless版实例.md)
    -   [程序代码连接](/cn.zh-CN/Serverless版快速入门/连接实例/程序代码连接.md)

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

