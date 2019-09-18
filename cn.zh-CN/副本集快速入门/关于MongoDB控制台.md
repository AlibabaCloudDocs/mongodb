# 关于MongoDB控制台 {#concept_pp1_vyq_52b .concept}

MongoDB管理控制台是用于管理MongoDB实例的Web应用程序，您可以在MongoDB管理控制台上执行创建实例、设置IP白名单、设置连接数据库的密码、设置网络类型等操作。

MongoDB管理控制台是阿里云管理控制台的一部分，关于控制台的通用设置和基本操作请参见：[使用阿里云管理控制台](https://help.aliyun.com/document_detail/47605.html)。

## 前提条件 {#section_a3c_t2h_hfb .section}

使用阿里云账号登录MongoDB管理控制台。若没有阿里云账号，请单击[注册](https://account.aliyun.com/register/register.htm)。

## 控制台首页 {#section_bnm_4gh_hfb .section}

对于MongoDB所有副本集实例而言，控制台首页的界面信息都是相同的。

登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)，进入实例列表页面，如下图所示（仅为示例，请以实际界面为准）。

![控制台首页](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6668/156878480513769_zh-CN.png)

参考说明

|序号|名称|说明|
|:-|:-|:-|
|1|副本集实例列表|MongoDB控制台的首页，显示同一账户中某个地区下的副本集实例信息。|
|2|地域|单击某一个地域名称，该地域下的所有实例就会显示在实例列表中。|
|3|刷新|刷新实例信息页面。|
|4|新建实例|[新建实例入口](https://help.aliyun.com/document_detail/26572.html)。|
|5|实例ID|单击进入该实例详情页面。|
|6|运行状态|实例运行状态，根据实例的不同情况也会有不同的状态。|
|7|管理|单击进入实例的管理详情页面，如查看基本信息、设置备份与恢复、[查看监控信息](https://help.aliyun.com/document_detail/60518.html)、[设置报警规则](https://help.aliyun.com/document_detail/61585.html)、[设置白名单](https://help.aliyun.com/document_detail/54529.html)等。|
|8|重启|[重启实例](https://help.aliyun.com/document_detail/44658.html)。|
|9|更多|一些操作的便捷按钮，如[变更配置](https://help.aliyun.com/document_detail/44655.html?spm=a2c4g.11186623.2.22.7316390a06ETar)、[续费](https://help.aliyun.com/document_detail/54285.html?spm=a2c4g.11186623.2.23.7316390a06ETar)。|
|10|修改实例备注|单击铅笔图标可修改实例的备注名，若不修改，则与实例ID一致。|

## MongoDB实例控制台 {#section_r2s_zhh_hfb .section}

登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)，单击**实例ID**操作栏下的**管理**，即可进入MongoDB实例的管理详情页面，详情如下表所示：

|控制台页面名称|区块名称|描述|常用操作链接|
|:------|:---|:-|:-----|
|界面上方操作区|-|自建MongoDB迁移、备份实例、重启实例操作。| -   [自建MongoDB迁移](https://help.aliyun.com/document_detail/44660.html)
-   备份实例
-   [重启实例](https://help.aliyun.com/document_detail/44658.html)

 |
|基本信息|基本信息|查看实例的基本信息，如实例ID、地域、网络类型、规格、磁盘空间，进行变更实例配置操作。|[变更实例配置](https://help.aliyun.com/document_detail/44655.html)|
|账号管理|查看实例账号，重置密码操作。|[重置密码](https://help.aliyun.com/document_detail/54544.html)|
|连接信息|查看节点的域名地址、端口号。|-|
|主实例资源状况|查看实例的磁盘空间使用率、IOPS使用率、连接数和CPU使用率。|-|
|实例关系|查看实例节点间的关系。|-|
|备份与恢复|备份列表|查看选定时间的数据备份列表、按照时间范围恢复数据、从备份点创建实例、按时间点新建实例。| -   [下载备份数据](https://help.aliyun.com/document_detail/55011.html)
-   [从备份点创建实例](https://help.aliyun.com/document_detail/55013.html)
-   [数据恢复](https://help.aliyun.com/document_detail/55015.html)
-   [按时间点新建实例](https://help.aliyun.com/document_detail/55014.html)

 |
|备份设置|按照选定的时间点进行周期性的自动备份。|[设置备份周期](https://help.aliyun.com/document_detail/55008.html)|
|监控信息|资源监控|根据选定的数据指标和查询时间查看Primary节点和Secondary节点的监控信息。|-|
|报警规则|设置报警规则|设置报警规则操作。|[报警规则](https://help.aliyun.com/document_detail/61585.html)|
|安全控制|安全控制|进行IP白名单设置。|[设置IP白名单](https://help.aliyun.com/document_detail/66111.html)|

