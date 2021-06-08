# 关于MongoDB控制台（分片集群实例）

MongoDB管理控制台是用于管理MongoDB实例的Web应用程序，您可以在MongoDB管理控制台执行创建实例、设置IP白名单、设置连接数据库的密码、设置网络类型等操作。

MongoDB管理控制台是阿里云管理控制台的一部分，关于控制台的通用设置和基本操作请参见[使用阿里云管理控制台](https://help.aliyun.com/document_detail/47605.html)。

## 前提条件

使用阿里云账号登录MongoDB管理控制台。若没有阿里云账号，请单击[注册](https://account.aliyun.com/register/register.htm)。

## 控制台首页

对于MongoDB所有分片集群实例而言，控制台首页的界面信息都是相同的。

登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)，进入实例列表页面，如下图所示（仅为示例，请以实际界面为准）。

![控制台首页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8178317951/p87948.png)

参考说明

|序号|名称|说明|
|:-|:-|:-|
|①|分片集群实例列表|MongoDB管理控制台的分片集群实例列表，显示同一账户中某个地区下的分片集群实例信息。|
|②|地域|下拉选择某个地域，该地域下的所有实例就会显示在实例列表中。|
|③|刷新|刷新实例信息页面。|
|④|新建实例|[新建实例入口](https://help.aliyun.com/document_detail/55137.html)。|
|⑤|实例ID|-   单击进入该实例详情页面。
-   单击实例ID后的![修改](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9878113261/p280997.png)，可以修改实例的备注名。 |
|⑥|运行状态|实例运行状态，根据实例的不同情况也会有不同的状态。|
|⑦|管理|单击**操作**列的![更多](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9878113261/p280998.png)，可快捷对实例进行管理、重启、释放等操作。|
|⑧|导出|[导出实例列表](/cn.zh-CN/用户指南/实例管理/导出实例列表.md)。|

## MongoDB实例控制台

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的资源组和地域。
3.  在左侧导航栏，单击**分片集群实例列表**。
4.  找到目标实例，单击目标实例所在行**操作**列的![更多](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9878113261/p280998.png)，选择**管理**。

进入MongoDB实例的管理详情页面，详情如下表所示：

|控制台页面名称|区块名称|描述|常用操作链接|
|:------|:---|:-|:-----|
|界面上方操作区|-|可进行备份实例、重启实例操作。|-   [备份实例](/cn.zh-CN/用户指南/数据备份/手动备份MongoDB数据.md)。
-   [重启实例](/cn.zh-CN/用户指南/实例管理/重启实例.md)。 |
|基本信息|基本信息|查看实例的基本信息，例如实例ID、地域、可用区、网络类型、存储引擎等。|无|
|规格信息|查看MongoDB版本、可维护时间段、付费方式、创建时间、到期时间等。|[设置可维护时间段](/cn.zh-CN/用户指南/实例管理/设置可维护时间段.md)。|
|Mongos列表或者Shard列表|-   在Mongos列表中，选择目标ID，单击![更多](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9878113261/p280998.png)可以变配、登录、重启。
-   在Shard列表中，选择目标ID，单击![更多](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9878113261/p280998.png)可以主备切换、变更配置、登录、重启实例的Shard节点。
-   重启节点时，可能会导致数据库的读写操作失败，所以不建议用户在重启数据库，或者是重启节点的时候进行数据库的增删改查等操作。

|-   [主备切换](/cn.zh-CN/用户指南/主备切换/分片集群实例设置主备切换.md)。
-   [变更配置](/cn.zh-CN/用户指南/实例管理/变更实例配置/变更配置方案概览.md)。
-   [登录数据库](/cn.zh-CN/快速入门/连接实例/通过DMS连接MongoDB分片集群实例.md)。
-   [重启节点](/cn.zh-CN/用户指南/实例管理/重启实例.mdsection_q52_thn_cfb)。
-   [查看监控信息](/cn.zh-CN/用户指南/监控与报警/监控信息/查看监控信息.md)。 |
|备份与恢复|-|查看选定时间的数据备份列表、按照时间范围恢复数据、从备份点创建实例、按时间点新建实例等。|-   [下载备份数据]()。
-   [按时间点新建实例](/cn.zh-CN/用户指南/数据恢复/按时间点新建实例.md)。 |
|监控信息|-|根据选定的数据指标和查询时间查看Mongos节点和Shard节点的监控信息。|无|
|数据安全性|白名单设置|可进行IP白名单设置。|[IP白名单设置]()。|
|审计日志|MongoDB审计日志记录了您对数据库执行的所有操作，您可以通过对审计日志进行分析。|[查看审计日志]()。|

