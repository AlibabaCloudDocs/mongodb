# ApsaraDB for MongoDB console \(Sharde cluster instance\)

The ApsaraDB for MongoDB console is a web application for managing instances. In the ApsaraDB for MongoDB console, you can create and manage instances, configure the instance IP whitelists, passwords, and network types, and perform other operations.

The ApsaraDB for MongoDB console is part of the Alibaba Cloud Management Console. For more information about common settings and basic operations in the Alibaba Cloud Management Console, see [Alibaba Cloud Management Console](https://www.alibabacloud.com/help/zh/doc-detail/47605.html).

## Prerequisites

An Alibaba Cloud account is used. To create an Alibaba Cloud account, go to the [Alibaba Cloud official website](https://account.aliyun.com/register/register.htm).

## ApsaraDB for MongoDB console homepage

The console homepage displays the same information for all sharded cluster instances.

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) and go to the Sharded Cluster Instances page, as shown in the following figure. This figure is only to be used for reference. The actual page may be different.

![ApsaraDB for MongoDB console homepage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8178317951/p87948.png)

UI element description

|No.|UI element|Description|
|:--|:---------|:----------|
|1|Sharded Cluster Instances|The ApsaraDB for MongoDB console homepage, which displays all sharded cluster instances in a region that belong to the current account.|
|2|Region|You can click a region to display all instances that reside within the region.|
|3|Refresh|The button to refresh the instance information page.|
|4|Create Instance|The button to [create an instance](https://www.alibabacloud.com/help/zh/doc-detail/55137.htm).|
|5|Instance ID|-   You can click an instance ID to go to the Basic Information page of the instance.
-   You can click the icon following an instance ID to modify the name of the instance. |
|6|Status|The status of the instance. Instances may be in different states.|
|7|More icon|You can click this icon to manage, restart, or release an instance.|
|8|Export|The button to [Export the list of instances](/intl.en-US/User Guide/Instance management/Export the list of instances.md).|

## ApsaraDB for MongoDB instance console

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Click an **Instance ID** or **Manage** in the Actions column corresponding to an instance. The Basic Information page is displayed. The following table lists the UI elements on the page.

|UI element or page|Section|Description|Operation|
|:-----------------|:------|:----------|:--------|
|Top navigation bar|N/A|You can back up and restart the instance.|-   [Back up an instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md)
-   [Restart an instance](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.md) |
|Basic Information|Basic Information|You can view the basic information about the instance, such as the instance ID region, network type, and storage engine.|N/A|
|Specification Information|You can view the instance specifications such as the database version, maintenance period, billing method, creation time, and expiration time.|[Specify a maintenance period](/intl.en-US/User Guide/Instance management/Specify a maintenance period.md)|
|Mongos List or Shard List|-   In the mongos list, you can find a mongos ID and click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8178317951/p13802.png) icon to change its configurations, and log on to or restart the mongos.
-   In the shard list, you can find a shard ID and click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8178317951/p13802.png) icon to log on to a shard, restart the shard, trigger a failover, or change the shard configurations.
-   Database read and write operations may fail when you restart nodes. We recommend that you do not perform the Create, Retrieve, Update, and Delete \(CRUD\) operations on databases when you restart nodes.

|-   [Trigger a failover](/intl.en-US/User Guide/Primary/Secondary failover/Trigger a primary/secondary failover for a shard of a sharded cluster instance.md)
-   [Change Specifications](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md)
-   [Log on to a database](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster ApsaraDB for MongoDB instance through DMS.md)
-   [Restart a node](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.mdsection_q52_thn_cfb)
-   [View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md) |
|Backup and Recovery|N/A|You can view and download a list of data backups for a specified time period, restore data from the specified time period, or create an instance from a specified backup point.|-   [Download backup data]()
-   [Restore data to a new ApsaraDB for MongoDB instance by point in time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md) |
|Monitoring Info|N/A|You can view monitoring information of mongos or shards based on the specified metrics and time range.|N/A|
|Data Security|Whitelist Settings|You can configure an IP whitelist.|[Configure a whitelist]()|
|Audit Logs|Audit logs record all operations that you perform on a database. You can use these logs in analysis.|[View audit logs](/intl.en-US/User Guide/Data security/Audit logs (previous version)/Configure audit logging for an ApsaraDB for MongoDB instance.md)|

