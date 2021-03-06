# 设置SSL加密

为提高链路的安全性，您可以启用SSL（Secure Sockets Layer）加密，然后安装SSL CA证书到您的应用服务。SSL加密功能在传输层对网络连接进行加密，在提升通信数据安全性的同时，保证数据的完整性。本章节介绍SSL加密功能的相关操作。

-   实例类型为副本集实例。
-   实例的数据库版本为3.4、4.0、4.2或4.4版本。

## 影响

在开通、关闭SSL加密和更新SSL证书时，实例会被重启一次，请提前做好业务安排并确保应用有重连机制。

**说明：** 重启实例会对实例的节点执行轮转重启，每个节点会有30秒左右的闪断，如果集合的数量较多（超过1万），闪断时间也会随之变长。

## 注意事项

-   SSL CA证书只能通过MongoDB控制台下载。
-   由于SSL加密的固有缺陷，开通SSL加密会显著增加实例的CPU使用率，建议在有加密需求时才开通SSL加密（例如通过公网连接MongoDB实例）。

    **说明：** 内网链路相对较安全，一般无需对链路加密。

-   开通SSL后支持SSL和非SSL两种连接方式。

## 操作步骤

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**副本集实例列表**。

4.  找到目标实例，单击实例ID。

5.  在左侧导航栏，选择**数据安全性** \> **SSL** 。

6.  根据要执行的操作，选择下述操作步骤。

    **说明：** 在开通、关闭SSL加密和更新SSL证书时，实例会被重启一次，请提前做好业务安排并确保应用有重连机制。

    |要执行的操作|前提条件|操作步骤|
    |:-----|:---|:---|
    |开通SSL加密|SSL加密处于**未开通**状态。|单击**SSL状态**右侧的滑块，然后在弹出对话框中单击**确定**。|
    |更新SSL证书有效期|SSL加密处于**已开通**状态。|单击**更新证书**，然后在弹出的对话中单击**确定**。|
    |下载SSL CA证书|SSL加密处于**已开通**状态。|单击**下载证书**，将CA证书下载至本地。|
    |关闭SSL加密|SSL加密处于**已开通**状态。|单击**SSL状态**右侧的滑块，然后在弹出对话框中单击**确定**。|


## 相关文档

[使用Mongo Shell通过SSL加密连接数据库](/cn.zh-CN/用户指南/数据安全性/使用Mongo Shell通过SSL加密连接数据库.md)

