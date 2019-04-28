# 通过 Mongo Shell 登录MongoDB数据库 {#concept_atc_g3d_2gb .concept}

您可以在本地或[ECS](https://help.aliyun.com/document_detail/25367.html)上安装 Mongo Shell 工具，通过 Mongo Shell 的方式登录MongoDB数据库。

## 注意事项 {#section_php_33d_2gb .section}

-   为保障鉴权成功，请安装 Mongo Shell 3.0及以上的版本。安装步骤请参考官方文档 [Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。
-   需要提前将访问该实例的IP地址或者IP段加入到实例白名单中，详情请参见[设置白名单](cn.zh-CN/单节点快速入门/设置白名单.md#)。
-   同一地域内、不同可用区之间的MongoDB实例和ECS实例可以通过专有网络进行连接，详情请参见[MongoDB跨可用区内网访问实例](../../../../cn.zh-CN/用户指南/连接实例/MongoDB跨可用区内网访问实例.md#)。
-   如需通过公网登录MongoDB数据库，需要申请公网连接地址，详情请参见[申请公网连接地址](cn.zh-CN/单节点快速入门/申请公网连接地址.md#)。

## 操作步骤 {#section_gd4_l3d_2gb .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的地域。
3.  在左侧导航栏，单击**副本集实例列表**。
4.  找到目标实例，单击实例ID。
5.  单击左侧导航栏的**数据库连接**，获取连接 Primary 节点的连接地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6664/155643543513741_zh-CN.png)

6.  在安装有 Mongo Shell 的本地服务器或ECS上进行连接。

    ```
    mongo --host <host> -u <username> -p --authenticationDatabase <database>
    ```

    **说明：** 

    -   <host\>：Primary 节点的连接地址。
    -   <username\>：登录数据库的账号，默认为 root 。
    -   <database\>：对登录数据库的账号和密码进行认证的数据库，默认为 admin 。
    示例：

    ```
    mongo --host dds-bpxxxxxxxxxx.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  命令行提示`Enter password:`时，输入数据库账号对应的密码。如果忘记了root账号的密码，您可以通过[设置密码](cn.zh-CN/单节点快速入门/设置密码.md#)的方式来重置密码。

    **说明：** 输入密码时，密码字符是不可见的。


## 连接MongoDB数据库的各类场景 {#section_eii_nos_pkx .section}

-   [如何通过公网连接MongoDB实例](../../../../cn.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md#)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md#)
-   [ECS实例与MongoDB实例地域不同如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同如何连接.md#)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md#)

## 相关问题 {#section_dld_xjd_2gb .section}

-   [排查 Mongo Shell 登录问题](../../../../cn.zh-CN/产品使用问题/连接数据库/排查 Mongo Shell 登录问题.md#)
-   [排查 MongoDB CPU使用率高的问题](../../../../cn.zh-CN/最佳实践/排查MongoDB CPU使用率高的问题.md#)
-   [如何查询及限制连接数](../../../../cn.zh-CN/产品使用问题/如何查询及限制连接数.md#)

