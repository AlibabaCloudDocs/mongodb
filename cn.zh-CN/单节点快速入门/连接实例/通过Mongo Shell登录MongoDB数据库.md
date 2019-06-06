# 通过Mongo Shell登录MongoDB数据库 {#concept_atc_g3d_2gb .concept}

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
5.  单击左侧导航栏的**数据库连接**，获取连接Primary节点的连接地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6664/155979037513741_zh-CN.png)

    |项目|说明|
    |:-|:-|
    |网络类型|     -   **内网连接 - 专有网络**：也称为VPC（Virtual Private Cloud）。VPC是一种隔离的网络环境，安全性和性能均高于传统的经典网络。专有网络需要事先创建，详情请参考[创建专有网络](https://help.aliyun.com/document_detail/65402.html)。
    -   **公网连接**：为保障安全性，公网连接地址默认没有创建，需要您手动申请。详情请参考[申请公网连接地址](cn.zh-CN/副本集快速入门/申请公网连接地址.md#)。
 |
    |角色|Primary节点：单节点实例的主节点，该节点拥有数据库读写权限。|
    |Primary节点连接地址|控制台获取的Primary节点连接地址格式如下。     ``` {#codeblock_1q2_2f7_ahe}
<host>:<port>
    ```

     -   <host\>：登录Primary节点的域名地址。
    -   <port\>：登录Primary节点的端口。
 |
    |Connection String URI连接地址|控制台获取的Connection String URI连接地址格式如下。     ``` {#codeblock_vnk_cv6_zgy}
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
    ```

     -   mongodb://：前缀，代表这是一个Connection String。
    -   username:password@：登录MongoDB数据库的用户名和密码，中间用英文的冒号分隔。
    -   hostX:portX：单节点实例的连接地址。
    -   /database：鉴权时，用户帐号所属的数据库。
    -   ?options：指定额外的连接选项。
 |

6.  在安装有 Mongo Shell 的本地服务器或ECS上进行连接。

    ``` {#codeblock_86p_3bk_2y6}
    mongo --host <host:port> -u <username> -p --authenticationDatabase <database>
    ```

    **说明：** 

    -   <host:port\>：Primary节点的连接地址，包含域名和端口号信息。
    -   <username\>：登录数据库的账号，默认为root 。
    -   <database\>：对登录数据库的账号和密码进行认证的数据库，默认为admin 。
    示例：

    ``` {#codeblock_ivt_3nd_6re}
    mongo --host dds-bpxxxxxxxxxx.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  命令行提示`Enter password:`时，输入数据库账号对应的密码。如果忘记了root账号的密码，您可以通过[设置密码](cn.zh-CN/单节点快速入门/设置密码.md#)的方式来重置密码。

    **说明：** 输入密码时，密码字符是不可见的。


## 连接MongoDB数据库的各类场景 {#section_eii_nos_pkx .section}

-   [如何通过公网连接MongoDB实例](../../../../cn.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md#)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md#)
-   [ECS实例与MongoDB实例地域不同如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同时如何连接.md#)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md#)

## 相关问题 {#section_dld_xjd_2gb .section}

-   [排查 Mongo Shell 登录问题](../../../../cn.zh-CN/常见问题/热点问题/排查 Mongo Shell 登录问题.md#)
-   [排查 MongoDB CPU使用率高的问题](../../../../cn.zh-CN/最佳实践/排查MongoDB CPU使用率高的问题.md#)
-   [如何查询及限制连接数](../../../../cn.zh-CN/常见问题/热点问题/如何查询及限制连接数.md#)

