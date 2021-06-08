# 关于MongoDB控制台（Serverless实例）

MongoDB管理控制台是用于管理MongoDB实例的Web应用程序，您可以在MongoDB管理控制台上执行创建实例、设置IP白名单、设置连接数据库的密码、设置网络类型等操作。

MongoDB管理控制台是阿里云管理控制台的一部分，关于控制台的通用设置和基本操作请参见[使用阿里云管理控制台](https://help.aliyun.com/document_detail/47605.html)。

## 前提条件

使用阿里云账号登录MongoDB管理控制台。若没有阿里云账号，请单击[注册](https://account.aliyun.com/register/register.htm)。

## 控制台首页

对于MongoDB所有Serverless实例而言，控制台首页的界面信息都是相同的。

登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)，进入**Serverless实例列表**页面，如下图所示（仅为示例，请以实际界面为准）。

![控制台首页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4415322061/p170762.png)

参考说明

|序号|名称|说明|
|:-|:-|:-|
|①|Serverless实例列表|MongoDB控制台的Serverless实例列表，显示同一账户中某个地域下的Serverless实例信息。|
|②|地域|下拉选择某个地域，该地域下的所有实例会显示在实例列表中。|
|③|创建实例|[创建Serverless实例的入口](/cn.zh-CN/快速入门/创建实例/创建Serverless实例.md)。|
|④|刷新|刷新实例信息页面。|
|⑤|实例名称/ID|-   单击实例ID进入该实例详情页面。
-   单击实例ID后的![修改](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9878113261/p280997.png)，可以修改实例的备注名。 |
|⑥|运行状态|实例运行状态，根据实例的不同情况也会有不同的状态。|
|⑦|管理实例|单击**操作**列的![更多](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9878113261/p280998.png)，可快捷对实例进行管理、续费、编辑标签操作。|
|⑧|导出|[导出实例列表](/cn.zh-CN/用户指南/实例管理/导出实例列表.md)。|

## MongoDB实例控制台

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的资源组和地域。
3.  在左侧导航栏，单击**Serverless实例列表**。
4.  找到目标实例，单击目标实例所在行**操作**列的![更多](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9878113261/p280998.png)，选择**管理**。

进入Serverless实例的管理页面，详情如下表所示：

|控制台页面名称|区块名称|描述|常用操作链接|
|:------|:---|:-|:-----|
|**基本信息**|**基本信息**|查看实例的基本信息，如**实例ID**、**实例名称**、**可用区**、**网络类型**、**存储引擎**。|无|
|**规格信息**|查看MongoDB**版本**、**可维护时间段**、**付费方式**、**创建时间**、**到期时间**等。|[设置可维护时间段](/cn.zh-CN/用户指南/实例管理/设置可维护时间段.md)|
|**连接信息**|查看实例的**VPC ID**、**VSwitch ID**、**账号名**、**内网地址**和**公网地址**。|[重置密码]()|
|**监控信息**|无|根据选定的MongosID和查询时间查看Serverless实例的监控信息。|[查看监控信息](/cn.zh-CN/用户指南/监控与报警/监控信息/查看监控信息.md)|
|**数据库连接**|**私网连接**|查看实例的内网连接地址。|无|
|**公网连接**|查看实例的公网连接地址。|无|
|**安全设置**|无|进行实例的IP白名单设置以及安全组设置。|[设置白名单]()|

