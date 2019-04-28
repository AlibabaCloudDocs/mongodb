# 通过 Mongo Shell 登录MongoDB数据库 {#concept_mnd_xg2_qgb .concept}

您可以在本地服务器上或[ECS](https://help.aliyun.com/document_detail/25367.html)上安装 Mongo Shell 工具，通过 Mongo Shell 的方式登录MongoDB数据库。

## 前提条件 {#section_u3n_sh2_qgb .section}

-   为保障鉴权成功，请安装 Mongo Shell 3.0及以上的版本。安装步骤请参考官方文档 [Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。
-   请提前将需要访问该实例的服务器IP地址加入到实例白名单中，详情请参见[设置白名单](cn.zh-CN/分片集群快速入门/设置白名单.md#)。
-   如需通过公网登录MongoDB数据库，需要申请公网连接地址，详情请参见[申请公网连接地址](cn.zh-CN/分片集群快速入门/申请公网连接地址.md#)。

## 操作步骤 {#section_xx5_wh2_qgb .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/#/mongodb/detail/dds-bp141308a7947204/info)。
2.  在页面左上角，选择实例所在的地域。
3.  在左侧导航栏，单击**分片集群实例列表**。
4.  找到目标实例，单击实例ID。
5.  单击左侧导航栏的**数据库连接**，获取 Mongos 节点的连接地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6695/155643631613838_zh-CN.png)

    本示例有三个 Mongos 节点，需要登录某个节点，使用对应的地址进行登录即可。

6.  在安装有 Mongo Shell 的本地服务器或ECS上进行连接。

    ```
    mongo --host <mongos_host> -u <username> -p --authenticationDatabase <database>
    ```

    **说明：** 

    -   <mongos\_host\>：任一 Mongos 节点连接地址中的域名信息。
    -   <username\>：登录数据库的账号，默认为 root 。
    -   <database\>：对登录数据库的账号和密码进行认证的数据库，默认为 admin 。
    示例：

    ```
    mongo --host s-bp**********.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  命令行提示`Enter password:`时，输入数据库账号对应的密码。如果忘记了root账号的密码，您可以通过[设置密码](cn.zh-CN/分片集群快速入门/设置密码.md#)的方式来重置密码。

    **说明：** 输入密码时，密码字符是不可见的。


## 连接MongoDB数据库的常见场景 {#section_eii_nos_pkx .section}

-   [如何通过公网连接MongoDB实例](../../../../cn.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md#)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md#)
-   [ECS实例与MongoDB实例地域不同如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同如何连接.md#)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md#)

## 相关问题 {#section_um4_g32_qgb .section}

-   [排查 Mongo Shell 登录问题](../../../../cn.zh-CN/产品使用问题/连接数据库/排查 Mongo Shell 登录问题.md#)
-   [排查 MongoDB CPU使用率高的问题](../../../../cn.zh-CN/最佳实践/排查MongoDB CPU使用率高的问题.md#)
-   [如何查询及限制连接数](../../../../cn.zh-CN/产品使用问题/如何查询及限制连接数.md#)

## 更多信息 {#section_zsr_lf2_qgb .section}

不建议在生产环境中直接使用 root 用户登录数据库。您可以根据业务需求，创建用户并分配权限，详情请参考[使用DMS管理MongoDB数据库用户](../../../../cn.zh-CN/用户指南/账号管理/使用DMS管理MongoDB数据库用户.md#)。

**说明：** 关于DMS中MongoDB数据库的更多相关操作介绍请参考[DMS for MongoDB](https://help.aliyun.com/document_detail/47683.html)。

