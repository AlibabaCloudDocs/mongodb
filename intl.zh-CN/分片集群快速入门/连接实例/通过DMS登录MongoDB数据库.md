# 通过DMS登录MongoDB数据库 {#concept_qz5_3k2_2gb .concept}

您可以通过[数据管理服务DMS](https://www.alibabacloud.com/help/zh/doc-detail/47550.htm)登录MongoDB数据库。使用DMS您可以更便捷地对MongoDB数据库进行管理。

## 注意事项 {#section_tqx_53v_cgb .section}

通过DMS登录MongoDB数据库时，须使用MongoDB实例的内网连接地址，暂不支持公网连接地址。

## 准备工作 {#section_nlw_mz4_tgb .section}

根据MongoDB实例的网络类型，将DMS服务器的IP地址加入至MongoDB实例的白名单中，详情请参考[设置白名单](intl.zh-CN/分片集群快速入门/设置白名单.md#)。

**说明：** 如您已经将DMS服务器的IP地址加入至MongoDB实例的白名单中，可跳过此步骤。

|MongoDB实例的网络类型|DMS服务器的IP地址|
|:-------------|:----------|
|内网连接 - 专有网络| 100.104.175.0/24

 100.104.72.0/24

 100.104.5.0/24

 100.104.205.0/24

 |
|内网连接 - 经典网络| 120.55.177.0/24

 121.43.18.0/24

 101.37.74.0/24

 10.153.176.0/24

 10.137.42.0/24

 11.193.54.0/24

 |

## 操作步骤 {#section_wtq_x3v_cgb .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的地域。
3.  在左侧导航栏，单击**分片集群实例列表**。
4.  找到目标实例，单击实例ID。
5.  在左侧导航栏，单击**数据库连接**，获取到 Mongos 的内网连接地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6694/156143905834556_zh-CN.png)

6.  单击页面右上角的**登录数据库**，选择要登录的 mongos 节点，跳转到数据管理控制台页面。
7.  在数据管理控制台页面，填写相应信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23695/156143905913740_zh-CN.png)

    -   网络地址及端口：填入任一 Mongos 节点的内网连接地址。
    -   数据库用户名：默认为 root 。
    -   数据库：鉴权数据库，默认为 admin 。
    -   密码：数据库登录密码，如忘记密码可[重置密码](intl.zh-CN/分片集群快速入门/设置密码.md#)。
8.  单击**登录**。

## 更多信息 {#section_xi9_j15_vui .section}

