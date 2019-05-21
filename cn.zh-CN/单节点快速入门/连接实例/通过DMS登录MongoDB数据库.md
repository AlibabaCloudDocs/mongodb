# 通过DMS登录MongoDB数据库 {#concept_xdd_13v_cgb .concept}

您可以通过阿里云的[数据管理服务DMS](https://help.aliyun.com/document_detail/47550.html)登录MongoDB数据库。使用DMS您可以更便捷地对MongoDB数据库进行管理。

## 注意事项 {#section_tqx_53v_cgb .section}

通过DMS登录MongoDB实例的数据库时，须使用MongoDB实例的内网连接地址，暂不支持公网连接地址。

## 准备工作 {#section_nlw_mz4_tgb .section}

将DMS服务器的IP地址加入至MongoDB实例的白名单中，详情请参见[设置白名单](cn.zh-CN/单节点快速入门/设置白名单.md#)。

**说明：** 如您已经将DMS服务器的IP地址加入至MongoDB实例的白名单中，可跳过此步骤。

|MongoDB实例的网络类型|DMS服务器的IP地址|
|:-------------|:----------|
|内网连接 - 专有网络| 100.104.175.0/24

 100.104.72.0/24

 100.104.5.0/24

 100.104.205.0/24

 |

## 操作步骤 {#section_wtq_x3v_cgb .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的地域。
3.  在左侧导航栏，单击**副本集实例列表**。
4.  找到目标实例，单击实例ID。
5.  单击左侧导航栏的**数据库连接**，获取 Primary 节点的内网连接地址。

    ![MongoDB内网连接地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23695/155842510334538_zh-CN.png)

6.  单击右上角的**登录数据库**，跳转至数据管理控制台页面。
7.  在数据管理控制台页面，填写如下信息登录MongoDB数据库。

    ![DMS登录MongoDB页面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23695/155842510313740_zh-CN.png)

    -   网络地址及端口：填入 Primary 节点的内网连接地址。
    -   数据库用户名：默认为 root 。
    -   数据库：鉴权数据库，默认为 admin 。
    -   密码：数据库登录密码，如忘记密码可[重置密码](cn.zh-CN/单节点快速入门/设置密码.md#)。
8.  单击**登录**。

## 连接MongoDB数据库的常见场景 {#section_eii_nos_pkx .section}

-   [如何通过公网连接MongoDB实例](../../../../cn.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md#)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md#)
-   [ECS实例与MongoDB实例地域不同如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同如何连接.md#)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](../../../../cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md#)

## 更多信息 {#section_zsr_lf2_qgb .section}

-   建议在生产环境中不要直接使用 root 用户登录数据库。您可以根据业务需求，创建用户并分配权限，详情请参见[使用DMS管理MongoDB数据库用户](../../../../cn.zh-CN/用户指南/账号管理/使用DMS管理MongoDB数据库用户.md#)。

    **说明：** 关于DMS中MongoDB数据库的更多相关操作介绍请参见[DMS for MongoDB](https://help.aliyun.com/document_detail/47683.html)。

-   在DMS控制台的顶部导航栏中，您可以通过单击**性能**菜单下的选项，进入混合云数据库管理HDM（Hybrid Cloud Database Management）控制台。

    **说明：** 在HDM控制台中，您可以对MongoDB实例的实时性能、实时会话、慢日志、磁盘空间等信息进行监控和管理，详情请参见[混合云数据库管理帮助文档](https://help.aliyun.com/product/63907.html)中用户指南的相关文档。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23695/155842510347679_zh-CN.png)


