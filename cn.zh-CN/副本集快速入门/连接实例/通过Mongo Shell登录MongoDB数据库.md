# 通过Mongo Shell登录MongoDB数据库 {#concept_qgf_hv4_dgb .concept}

您可以在本地服务器上或 [ECS](https://www.alibabacloud.com/help/zh/doc-detail/25367.htm)上安装 Mongo Shell 工具，通过 Mongo Shell 的方式登录MongoDB数据库。

## 前提条件 {#section_psj_jv4_dgb .section}

-   为保障鉴权成功，请安装 Mongo Shell 3.0及以上的版本。安装步骤请参见官方文档 [Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。
-   请提前将需要访问该实例的服务器IP地址加入到实例白名单中，详情请参见[设置白名单](intl.zh-CN/副本集快速入门/设置白名单.md#)。
-   如需通过公网登录MongoDB数据库，需要申请公网连接地址，详情请参见[申请公网连接地址](intl.zh-CN/副本集快速入门/申请公网连接地址.md#)。

## 操作步骤 {#section_i15_dw4_dgb .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的地域。
3.  在左侧导航栏，单击**副本集实例列表**。
4.  找到目标实例，单击实例ID。
5.  单击左侧导航栏的**数据库连接**，获取单个节点的连接地址和 ConnectionStringURI 连接地址。
6.  在安装有 Mongo Shell 的本地服务器或ECS上进行连接。
    -   副本集中的单个节点连接方式。

        日常测试时，可直接连接 Primary 节点。需要注意的是一旦发生[主备切换](../../../../intl.zh-CN/用户指南/主备切换/副本集实例设置主备切换.md#)，连接节点的角色将发生变化，从而会对读写操作造成影响。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6675/156144189031535_zh-CN.png)

        在安装有 Mongo Shell 的本地服务器或ECS上进行连接。

        ``` {#codeblock_0ir_ix4_mhb}
        mongo --host <host> -u <username> -p --authenticationDatabase <database>
        ```

        **说明：** 

        -   <host\>：Primary 节点或 Secondary 节点的连接地址。

            -   Primary 节点：副本集实例中的主节点，该节点拥有数据库读写权限。
            -   Secondary 节点：副本集实例中的从节点，该节点仅拥有数据库的读权限
        -   <username\>：登录数据库的账号，默认为 root 。
        -   <database\>：对登录数据库的账号和密码进行认证的数据库，默认为 admin 。
        示例：

        ``` {#codeblock_0uo_225_fl1}
        mongo --host dds-bp**********.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
        ```

        命令行提示`Enter password:`时，输入数据库账号对应的密码。如果忘记了root账号的密码，您可以通过[设置密码](intl.zh-CN/副本集快速入门/设置密码.md#)的方式来重置密码。

        **说明：** 输入密码时，密码字符是不可见的。

    -   高可用连接方式（推荐）：使用ConnectionStringURI连接数据库，可实现高可用性。确保连接的节点始终为 Primary 节点，不会因为主备切换而影响应用的读写操作。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6675/156144189034449_zh-CN.png)

        在安装有 Mongo Shell 的本地服务器或ECS上进行连接。

        ``` {#codeblock_wdb_fxr_di4}
        mongo "<ConnectionStringURI>"
        ```

        **说明：** 

        -   双引号须为英文双引号（""）。
        -   <ConnectionStringURI\>：实例的**ConnectionStringURI**地址。

             **ConnectionStringURI**地址中`****`替换为数据库密码。数据库密码设置请参见[设置密码](intl.zh-CN/副本集快速入门/设置密码.md#)。


## 相关问题 {#section_why_5w4_dgb .section}

-    [排查 Mongo Shell 登录问题](../../../../intl.zh-CN/常见问题/热点问题/排查 Mongo Shell 登录问题.md#) 
-    [排查 MongoDB CPU使用率高的问题](../../../../intl.zh-CN/最佳实践/排查MongoDB CPU使用率高的问题.md#) 
-    [如何查询及限制连接数](../../../../intl.zh-CN/常见问题/热点问题/如何查询及限制连接数.md#) 

## 更多信息 {#section_zsr_lf2_qgb .section}

不建议在生产环境中直接使用 root 用户登录数据库。您可以根据业务需求，创建用户并分配权限，详情请参见[使用DMS管理MongoDB数据库用户](../../../../intl.zh-CN/用户指南/账号管理/使用DMS管理MongoDB数据库用户.md#)。

