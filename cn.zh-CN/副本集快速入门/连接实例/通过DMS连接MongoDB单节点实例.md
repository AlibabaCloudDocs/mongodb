# 通过DMS连接MongoDB单节点实例

数据管理服务DMS（Data Management Service）是一种集数据管理、结构管理、用户授权、安全审计、数据趋势、数据追踪、BI图表、性能优化和服务器管理于一体的数据管理服务。通过DMS连接MongoDB单节点实例，可以更便捷地管理MongoDB实例。

## 准备工作

将DMS服务器IP地址（100.104.0.0/16）加入至MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/单节点快速入门/设置白名单.md)。

**说明：** 如果您已经将DMS服务器的IP地址加入至MongoDB实例的白名单中，可跳过此步骤。

## 操作步骤

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**副本集实例列表**。

4.  找到目标实例，单击实例ID。

5.  单击页面右上角的**登录数据库**，并单击要登录的数据库节点（**Primary**或**Secondary**），跳转到数据管理控制台页面。

    **说明：**

    -   Primary节点：副本集实例中的主节点，连接该节点可执行数据库的读写操作。
    -   Secondary节点：副本集实例中的从节点，连接该节点仅能执行数据库的读操作。
6.  在数据管理控制台页面，填写如下信息。

    ![DMS登录MongoDB页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0594087951/p13740.png)

    |配置|说明|
    |--|--|
    |**网络地址及端口**|已自动填入MongoDB实例的Primary节点内网连接地址，无需配置。|
    |**数据库用户名**|填入MongoDB实例的数据库账号，初始账号为root。|
    |**数据库名**|填入鉴权数据库名，即数据库账号所属的数据库。 **说明：**

    -   如果**数据库用户名**填写的是root，那么对应的数据库名称即为admin。
    -   不建议在生产环境中直接使用root账号连接数据库。您可以根据业务需求创建用户并分配权限，详情请参见[使用DMS管理MongoDB实例的账号]()。 |
    |**密码**|填入该数据库账号对应的密码。 **说明：** 如果忘记root账号的密码，您可以[重置密码](/cn.zh-CN/单节点快速入门/设置密码.md)。 |

7.  单击**登录**。


## 常见的连接场景

-   [如何通过公网连接MongoDB实例](/cn.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md)
-   [ECS实例与MongoDB实例地域不同时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同时如何连接.md)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](/cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md)

## 相关问题

-   [排查Mongo Shell登录问题](/cn.zh-CN/常见问题/热点问题/Linux实例使用Mongo Shell登录MongoDB数据库提示“Timeout while receiving message”错误.md)
-   [排查因连接数耗尽导致的数据库连接问题](/cn.zh-CN/常见问题/热点问题/MongoDB实例连接数耗尽导致数据库连接失败.md)
-   [排查MongoDB CPU使用率高的问题](/cn.zh-CN/最佳实践/性能/排查MongoDB CPU使用率高的问题.md)
-   [如何查询及限制连接数](/cn.zh-CN/常见问题/热点问题/如何查询及限制MongoDB实例的连接数.md)

## 更多信息

在DMS控制台的顶部导航栏中，您可以通过单击**性能**菜单下的选项，进入数据库自治服务DAS（Database Autonomy Service）控制台。

![进入HDM控制台](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0594087951/p47679.png)

**说明：** 在DAS控制台中，您可以对MongoDB实例的实时性能、实时会话、慢日志、磁盘空间等信息进行监控和管理，详情请参见[数据库自治服务帮助文档](https://help.aliyun.com/product/63907.html)中用户指南的相关文档。

