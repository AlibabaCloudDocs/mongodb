# 通过Mongo Shell连接MongoDB分片集群实例

Mongo Shell是MongoDB数据库自带的数据库管理工具，您可以在本地或ECS上安装Mongo Shell工具，然后通过Mongo Shell连接MongoDB分片集群实例。

-   为保障鉴权成功，请安装与MongoDB实例版本相对应的Mongo Shell版本。安装步骤请参见官方文档[Install MongoDB](https://docs.mongodb.com/manual/installation/)（请根据您的客户端版本在页面左上角选择版本号）。
-   已将客户端的IP地址加入到MongoDB实例的白名单中，详情请参见[设置白名单](/intl.zh-CN/分片集群快速入门/设置白名单.md)。

    **说明：** 如需通过公网连接MongoDB实例，需要[申请公网连接地址](/intl.zh-CN/分片集群快速入门/申请公网连接地址.md)。


## 操作步骤

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**分片集群实例列表**。

4.  找到目标实例，单击实例ID。

5.  在左侧导航栏，单击**数据库连接**，获取Mongos节点的连接地址。

    ![连接信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3378317951/p13833.png)

6.  在安装有Mongo Shell的本地服务器或ECS中连接实例。

    ```
    mongo --host <mongos_host> -u <username> -p --authenticationDatabase <database>
    ```

    **说明：**

    -   <mongos\_host\>：任一Mongos节点连接地址中的连接地址。
    -   <username\>：MongoDB实例的数据库账号，初始账号为root。不建议在生产环境中直接使用root账号连接数据库。您可以根据业务需求创建用户并分配权限，详情请参见[使用DMS管理MongoDB数据库用户]()。
    -   <database\>：鉴权数据库名，即数据库账号所属的数据库。当数据库账号为root时，对应的数据库为admin。
    示例：

    ```
    mongo --host s-bp**********.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  在命令行提示`Enter password:`时，输入数据库账号对应的密码并按回车键确认。如果忘记了root账号的密码，您可以通过[设置密码](/intl.zh-CN/分片集群快速入门/设置密码.md)的方式来重置密码。

    **说明：** 输入密码时，密码字符是不可见的。


## 常见的连接场景

-   [如何通过公网连接MongoDB实例](/intl.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md)
-   [ECS实例与MongoDB实例地域不同时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同时如何连接.md)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md)

## 相关问题

-   [排查 Mongo Shell 登录问题](/intl.zh-CN/常见问题/热点问题/Linux实例使用Mongo Shell登录MongoDB数据库提示“Timeout while receiving message”错误.md)
-   [排查因连接数耗尽导致的数据库连接问题](/intl.zh-CN/常见问题/热点问题/MongoDB实例连接数耗尽导致数据库连接失败.md)
-   [排查 MongoDB CPU使用率高的问题](/intl.zh-CN/最佳实践/性能/排查MongoDB CPU使用率高的问题.md)
-   [如何查询及限制连接数](/intl.zh-CN/常见问题/热点问题/如何查询及限制MongoDB实例的连接数.md)

