---
keyword: [mongo 连接指定数据库, mongodb安全写入, mongo登录方法, mongodb如何连接, mongo密码登录连接数据库]
---

# 通过Mongo Shell连接MongoDB副本集实例

Mongo Shell是MongoDB数据库自带的数据库管理工具，您可以在本地或ECS上安装Mongo Shell工具，然后通过Mongo Shell连接MongoDB副本集实例。本文详细介绍MongoDB的登录方法。

-   为保障鉴权成功，请安装与MongoDB实例版本相对应的Mongo Shell版本。安装步骤请参见官方文档[Install MongoDB](https://docs.mongodb.com/manual/installation/)（请根据您的客户端版本在页面左上角选择版本号）。
-   已将客户端的IP地址加入到MongoDB实例的白名单中，详情请参见[设置白名单]()。

    **说明：** 如需通过公网连接MongoDB实例，需要[申请公网连接地址]()。


## 操作步骤

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**副本集实例列表**。

4.  找到目标实例，单击实例ID。

5.  在左侧导航栏，单击**数据库连接**，获取单个节点的连接地址和ConnectionStringURI连接地址。

    **说明：** 关于如何获取连接地址的详情说明，请参见[连接地址说明]()

6.  在安装有Mongo Shell的客户端或ECS中连接实例。

    -   单个节点的连接方式。

        日常测试时，可直接连接Primary、Secondary节点。需要注意的是一旦发生[主备切换](/intl.zh-CN/用户指南/主备切换/副本集实例设置主备切换.md)，连接节点的角色将发生变化，从而会对读写操作造成影响。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2594087951/p31535.png)

        命令格式：

        ```
        mongo --host <host> -u <username> -p --authenticationDatabase <database>
        ```

        **说明：**

        -   <host\>：Primary节点或Secondary节点的连接地址。
            -   Primary节点：副本集实例中的主节点，连接该节点可执行数据库的读写操作。
            -   Secondary节点：副本集实例中的从节点，连接该节点仅能执行数据库的读操作。
        -   <username\>：MongoDB实例的数据库账号，初始账号为root。不建议在生产环境中直接使用root账号连接数据库。您可以根据业务需求创建用户并分配权限，详情请参见[MongoDB数据库账号权限管理](/intl.zh-CN/用户指南/账号管理/MongoDB数据库账号权限管理.md)。
        -   <database\>：鉴权数据库名，即数据库账号所属的数据库。当数据库账号为root时，对应的数据库为admin。如果您希望指定其他数据库，请先在该数据库中使用[db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/index.html)命令创建账号，然后再使用该账号进行连接。
        示例：

        ```
        mongo --host dds-bp**********.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
        ```

        在命令行提示`Enter password:`时，输入数据库账号对应的密码并按回车键确认。如果忘记了root账号的密码，您可以通过[设置密码](/intl.zh-CN/快速入门/重置密码.md)的方式来重置密码。

        **说明：** 输入密码时，密码字符是不可见的。

    -   高可用连接方式（推荐）：使用ConnectionStringURI连接数据库，可确保连接的节点始终为Primary节点，不会因为主备切换而影响应用的读写操作。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3594087951/p34449.png)

        命令格式：

        ```
        mongo "<ConnectionStringURI>"    
        ```

        **说明：**

        -   双引号须为英文双引号（""）。
        -   <ConnectionStringURI\>：实例的ConnectionStringURI地址。

            ConnectionStringURI地址中的`****`需要替换为数据库密码。数据库密码设置请参见[设置密码](/intl.zh-CN/快速入门/重置密码.md)。


## 常见的连接场景

-   [如何通过公网连接MongoDB实例](/intl.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md)

    **说明：** 通过公网地址连接数据库时，建议使用SSL加密连接，详情请参见[使用Mongo Shell通过SSL加密连接数据库](/intl.zh-CN/用户指南/数据安全性/使用Mongo Shell通过SSL加密连接数据库.md)。

-   [ECS实例与MongoDB实例网络类型不同时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md)
-   [ECS实例与MongoDB实例地域不同时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同时如何连接.md)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](/intl.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md)

## 相关问题

-   [排查Mongo Shell 登录问题](/intl.zh-CN/常见问题/热点问题/Linux实例使用Mongo Shell登录MongoDB数据库提示“Timeout while receiving message”错误.md)
-   [排查因连接数耗尽导致的数据库连接问题](/intl.zh-CN/常见问题/热点问题/MongoDB实例连接数耗尽导致数据库连接失败.md)
-   [排查MongoDB CPU使用率高的问题](/intl.zh-CN/最佳实践/性能/排查MongoDB CPU使用率高的问题.md)
-   [如何查询及限制连接数](/intl.zh-CN/常见问题/热点问题/如何查询及限制MongoDB实例的连接数.md)

