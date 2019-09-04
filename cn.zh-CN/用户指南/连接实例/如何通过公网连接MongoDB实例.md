# 如何通过公网连接MongoDB实例 {#concept_183456 .concept}

当您的本地设备需要通过公网地址连接MongoDB实例时，您可以使用本文中的方法快速实现连接。

## 前提条件 {#section_llp_kv7_b7l .section}

已为MongoDB实例申请公网连接地址，详情请参见：

-   [单节点实例申请公网连接地址](../../../../cn.zh-CN/单节点快速入门/申请公网连接地址.md#)
-   [副本集实例申请公网连接地址](../../../../cn.zh-CN/副本集快速入门/申请公网连接地址.md#)
-   [分片集群实例申请公网连接地址](../../../../cn.zh-CN/分片集群快速入门/申请公网连接地址.md#)

## 注意事项 {#section_zb0_uhw_7ay .section}

本文仅适用于本地设备连接MongoDB实例的情况，如需通过ECS实例连接MongoDB实例，您可以在ECS实例的详情页面查看准确的公网IP地址和内网IP地址。

通过公网连接至MongoDB实例存在一定的安全风险，建议通过ECS实例连接MongoDB实例。

## 方法一 通过IP地址查询定位本地设备的公网地址并连接实例 {#section_jyp_fmc_rks .section}

**操作步骤**

1.  访问[淘宝IP地址库](http://ip.taobao.com/ipSearch.html)查询您的公网地址。

    ![IP地址查询](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157550/156758214144638_zh-CN.png)

2.  将获取到的公网地址添加至MongoDB白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。
3.  在本地设备上，通过Mongo Shell登录MongoDB实例，详情请参考[通过 Mongo Shell 登录MongoDB数据库](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)。

    **说明：** 您也可以使用其他客户端工具登录MongoDB实例。


如果已经将本地设备的公网IP地址添加至MongoDB实例的白名单中，仍然无法连接MongoDB实例，而将MongoDB的白名单设置为0.0.0.0/0后可以连接。针对此情况，建议通过连接信息来定位公网地址，详情请参考[方法二 通过连接信息定位公网地址并连接实例](#section_6vm_is9_ani)。

## 方法二 通过连接信息定位公网地址并连接实例 {#section_6vm_is9_ani .section}

**操作步骤**

1.  将IP地址0.0.0.0/0添加到MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

    **说明：** 0.0.0.0/0表示允许任何设备访问MongoDB实例，有安全风险，请谨慎使用。如果使用，应当及时从白名单中删除。

2.  在本地设备上，通过Mongo Shell登录MongoDB实例，详情请参考[通过 Mongo Shell 登录MongoDB数据库](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)。

    **说明：** 通过Mongo Shell登录MongoDB实例时，请使用公网连接地址登录。

3.  通过下述命令查询通过Mongo Shell登录的客户端信息。

    ``` {#codeblock_zug_isw_oks}
    db.currentOp({"appName" : "MongoDB Shell","active" : true})
    ```

    输出示例

    ![客户端IP查询](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157550/156758214144647_zh-CN.png)

    **说明：** 如果通过其他方式登录MongoDB实例，您可通过下述命令查询所有客户端信息。

    ``` {#codeblock_wyj_b93_qav}
    db.runCommand({currentOp: 1, "active" : true})
    ```

4.  将获取到的IP地址加入至MongoDB实例白名单中，并将[步骤1](#li_cz7_zr1_e25)中添加的IP地址0.0.0.0/0删除。

## 更多信息 {#section_d1k_0nu_2ez .section}

如果您的公网地址不是固定的且经常变动，您可以通过以下方法连接MongoDB实例。

-   通过ECS连接MongoDB实例，详情请参考[通过 Mongo Shell 登录MongoDB数据库](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)。
-   通过VPN连接MongoDB实例，详情请参考[通过SSL-VPN隧道连接MongoDB实例](cn.zh-CN/用户指南/连接实例/本地客户端通过SSL-VPN隧道连接MongoDB实例.md#)。

