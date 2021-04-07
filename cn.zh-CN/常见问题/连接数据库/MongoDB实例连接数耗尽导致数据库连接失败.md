# 排查因连接数耗尽导致的数据库连接问题

当MongoDB实例的连接数被耗尽后，新发起的连接请求将无法被响应，本文介绍如何排查因连接数耗尽导致的数据库连接问题。

## 故障表现

不同的MongoDB实例规格支持的最大连接数有所不同，详情请参见[实例规格表](/cn.zh-CN/产品简介/实例规格表.md)。

-   部署的应用程序突然无法连接数据库。
-   已正确设置了白名单，通过Mongo Shell连接数据库时，提示如下错误：

    ```
    2019-07-10T10:30:43.597+0800 E QUERY    [js] Error: network error while attempting to run command 'isMaster' on host 'dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717'  :
    connect@src/mongo/shell/mongo.js:328:13
    @(connect):1:6
    exception: connect failed
    ```

-   已正确设置了白名单，通过DMS连接数据库时，提示如下错误：

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3774797951/p51168.png)


## 检查连接数是否被耗尽

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**分片集群实例列表**。

4.  找到目标实例，单击实例ID。

5.  在左侧导航栏中，单击**监控信息**。

6.  在**监控信息**页面，查看实例当前的**Connections**（连接数）信息。 如下图所示，该实例已使用的连接数为500。

    **说明：** 实例为分片集群实例时，您需要在页面右上角选择业务当前使用的**Mongos**节点。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3774797951/p51156.png)

7.  在左侧导航栏，单击**基本信息**。

8.  在**基本信息**页面中，您可以查看到当前实例规格对应的最大连接数，本案例为500。

    **说明：** 结合第6步获取到的实例已使用的连接数，可判断实例的连接数被耗尽。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3774797951/p51158.png)


## 解决方法

您可以通过[重启实例](/cn.zh-CN/用户指南/实例管理/重启实例.md)来临时释放所有的连接。为避免再次出现该问题，重启后建议您参考下述方法进行调整：

**说明：** 重启实例的操作会将实例的节点进行轮转重启，每个节点会有30秒左右的闪断，如果集合的数量较多（超过1万），闪断时间也会随之变长，重启前请做好业务安排并确保应用有重连机制。

-   合理地配置连接池，详情请参见[如何限制终端的连接数](/cn.zh-CN/常见问题/连接数据库/如何查询及限制MongoDB实例的连接数.md)。
-   [分析连接的来源](/cn.zh-CN/常见问题/连接数据库/如何查询及限制MongoDB实例的连接数.md)，如果经过分析是业务将连接数耗尽，请通过升级实例的规格，详情请参见[变更配置方案概览](/cn.zh-CN/用户指南/实例管理/变更实例配置/变更配置方案概览.md)。

