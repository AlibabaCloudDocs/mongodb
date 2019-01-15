# 通过 Mongo Shell 登录MongoDB数据库 {#task_wdf_npz_jfb .task}

您可以在ECS上安装mongo shell，用mongo shell的方式连接云数据库MongoDB。

为保障鉴权成功，请安装 Mongo Shell 3.0及以上的版本。安装步骤请参考官方文档 [Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。

已经将允许访问该实例的IP地址或者IP段加入到实例白名单中，详情请参见[设置白名单](intl.zh-CN/分片集群快速入门/设置白名单.md#)。

如需通过公网登录MongoDB数据库，需要申请公网连接地址，详情请参见[申请公网连接地址](intl.zh-CN/分片集群快速入门/申请公网连接地址.md#)。

1.   登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/#/mongodb/detail/dds-bp141308a7947204/info)。 
2.  在页面左上角，选择实例所在的地域。 
3.  在左侧导航栏，单击**分片集群实例列表**。 
4.  找到目标实例，单击实例ID。 
5.  单击左侧导航栏的**数据库连接**，获取 Mongos 节点的连接地址。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6695/154753292713838_zh-CN.png)

    本示例有三个 Mongos 节点，需要登录某个节点，使用对应的地址进行登录即可。

6.  在安装有 Mongo Shell 的 本地服务器或ECS上进行连接。 

    ```
    mongo --host <mongos_host> -u <username> -p --authenticationDatabase <database>
    ```

    说明：

    -   <mongos\_host\>：任一 Mongos 节点连接地址中的域名信息。
    -   <username\>：登录数据库的账号，默认为 root 。
    -   <database\>：对登录数据库的账号和密码进行认证的数据库，默认为 admin 。
    示例：

    ```
    mongo --host s-bp**********.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  命令行提示`Enter password:`时，输入数据库账号对应的密码。忘记密码请参考[设置密码](intl.zh-CN/单节点快速入门/设置密码.md#)。 

    **说明：** 输入密码时，密码字符是不可见的。

    相关问题

    -   [排查 Mongo Shell 登录问题](../../../../../intl.zh-CN/产品使用问题/排查 Mongo Shell 登录问题.md#)
    -   [排查 MongoDB CPU使用率高的问题](../../../../../intl.zh-CN/最佳实践/排查 MongoDB CPU使用率高的问题.md#)
    -   [如何查询及限制连接数](../../../../../intl.zh-CN/产品使用问题/如何查询及限制连接数.md#)

