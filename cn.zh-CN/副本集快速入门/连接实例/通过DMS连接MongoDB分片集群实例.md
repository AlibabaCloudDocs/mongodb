# 通过DMS连接MongoDB分片集群实例

数据管理服务DMS（Data Management Service）是一种集数据管理、结构管理、用户授权、安全审计、数据趋势、数据追踪、BI图表、性能优化和服务器管理于一体的数据管理服务。通过DMS连接MongoDB分片集群实例，可以更便捷地管理MongoDB实例。

## 准备工作

根据MongoDB实例的网络类型，将DMS服务器的IP地址加入至MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/分片集群快速入门/设置白名单.md)。

**说明：** 如您已经将DMS服务器的IP地址加入至MongoDB实例的白名单中，可跳过此步骤。

|MongoDB实例的网络类型|DMS服务器的IP地址|
|:-------------|:----------|
|专有网络|100.104.0.0/16|
|经典网络|120.55.177.0/24

121.43.18.0/24

101.37.74.0/24

10.153.176.0/24

10.137.42.0/24

11.193.54.0/24 |

## 操作步骤

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**分片集群实例列表**。

4.  找到目标实例，单击实例ID。

5.  单击页面右上角的**登录数据库**，选择任意Mongos节点ID，跳转到数据管理控制台页面。

    ![选择mongos节点登录](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7425715061/p66241.png)

6.  在数据管理控制台页面，填写相应信息。

    ![DMS登录页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0594087951/p13740.png)

    |配置|说明|
    |--|--|
    |**网络地址及端口**|已自动填入Mongos节点的内网连接地址，无需配置。|
    |**数据库用户名**|填入MongoDB实例的数据库账号，初始账号为root。|
    |**数据库名**|填入鉴权数据库名，即数据库账号所属的数据库。 **说明：**

    -   如果**数据库用户名**填写的是root，那么对应的数据库名即为admin。
    -   不建议在生产环境中直接使用root账号连接数据库。您可以根据业务需求创建用户并分配权限，详情请参见[使用DMS管理MongoDB实例的账号]()。 |
    |**密码**|填入该数据库账号对应的密码。 **说明：** 如果忘记root账号的密码，您可以[重置密码](/cn.zh-CN/单节点快速入门/设置密码.md)。 |

7.  单击**登录**。


## 常见的连接场景

-   [如何通过公网连接MongoDB实例](/cn.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md)
-   [ECS实例与MongoDB实例地域不同时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同时如何连接.md)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md)

## 相关问题

-   [排查 Mongo Shell 登录问题](/cn.zh-CN/常见问题/热点问题/Linux实例使用Mongo Shell登录MongoDB数据库提示“Timeout while receiving message”错误.md)
-   [排查因连接数耗尽导致的数据库连接问题](/cn.zh-CN/常见问题/热点问题/MongoDB实例连接数耗尽导致数据库连接失败.md)
-   [排查 MongoDB CPU使用率高的问题](/cn.zh-CN/最佳实践/性能/排查MongoDB CPU使用率高的问题.md)
-   [如何查询及限制连接数](/cn.zh-CN/常见问题/热点问题/如何查询及限制MongoDB实例的连接数.md)

## 更多信息

在DMS控制台的顶部菜单栏中，您可以通过选择**SQLConsole** \> **单库查询**打开单库查询页签，然后把鼠标放在![图标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9953325061/p182003.png)图标上，通过单击下拉菜单中的选项进入数据库自治服务DAS（Database Autonomy Service）控制台。

![进入DAS管理页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9953325061/p182002.png)

**说明：** 在DAS控制台中，您可以对MongoDB实例的实时性能、实时会话等信息进行监控和管理，详情请参见[数据库自治服务帮助文档](https://help.aliyun.com/product/63907.html)中用户指南的相关文档。

