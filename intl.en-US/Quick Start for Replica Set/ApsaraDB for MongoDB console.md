# ApsaraDB for MongoDB console

The ApsaraDB for MongoDB console is a web application for managing instances. In the ApsaraDB for MongoDB console, you can create and manage instances, configure the instance IP whitelists, passwords, and network types, and perform other operations.

The ApsaraDB for MongoDB console is part of the Alibaba Cloud Management Console. For more information about common settings and basic operations in the Alibaba Cloud Management Console, see [Alibaba Cloud Management Console](https://www.alibabacloud.com/help/zh/doc-detail/47605.html).

## Prerequisites

Use your Alibaba Cloud account to log on to the ApsaraDB for MongoDB console. To create an Alibaba Cloud account, go to the [Alibaba Cloud official website](https://account.aliyun.com/register/register.htm).

## ApsaraDB for MongoDB console homepage

The console homepage displays the same information for all replica set instances.

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) and go to the Replica Set Instances page, as shown in the following figure. This figure is only to be used for reference. The actual page may be different.

![ApsaraDB for MongoDB console homepage](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9913797951/p13769.png)

UI element description

|No.|UI element|Description|
|:--|:---------|:----------|
|1|Replica Set Instances|The ApsaraDB for MongoDB console homepage, which displays all replica set instances in a region that belong to the current account.|
|2|Region|You can click a region to display all instances that reside within the region.|
|3|Refresh|The button to refresh the instance information page.|
|4|Create Instance|The button to [create an instance](https://www.alibabacloud.com/help/zh/doc-detail/26572.htm).|
|5|Instance ID|You can click an instance ID to go to the Basic Information page of the instance.|
|6|Status|The status of the instance. Instances may be in different states.|
|7|Manage|You can click this button to go to the Basic Information page of the instance. On this page, you can view the basic information about the instance, configure instance backup and recovery, [view monitoring information](https://www.alibabacloud.com/help/zh/doc-detail/60518.htm), [set alert rules](https://www.alibabacloud.com/help/zh/doc-detail/61585.htm), and [configure a whitelist](https://www.alibabacloud.com/help/zh/doc-detail/54529.htm).|
|8|Restart|The button to [restart an instance](https://www.alibabacloud.com/help/zh/doc-detail/44658.htm).|
|9|More|Other buttons, such as [Change Configuration](https://www.alibabacloud.com/help/zh/doc-detail/44655.htm) and [Renew](https://www.alibabacloud.com/help/zh/doc-detail/54285.htm).|
|10|Edit icon|You can click this icon to modify the instance name. By default, the instance name is identical to the instance ID.|

## ApsaraDB for MongoDB instance console

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Click an **Instance ID** or **Manage** in the Actions column corresponding to an instance. The Basic Information page is displayed. The following table lists the UI elements on the page.

|UI element or page|Section|Description|Operation|
|:-----------------|:------|:----------|:--------|
|Top navigation bar|N/A|You can migrate, back up, and restart the instance.|-   [Migrate the data of an instance](https://www.alibabacloud.com/help/zh/doc-detail/99995.htm)
-   Back up an instance
-   [Restart an instance](https://www.alibabacloud.com/help/zh/doc-detail/44658.htm) |
|Basic Information|Basic Information|You can view the basic information about the instance, such as the instance ID, region, network type, specifications, and disk space. You can also change the configurations of the instance.|[Change the configurations of an instance](https://www.alibabacloud.com/help/zh/doc-detail/44655.htm)|
|Accounts|You can view account information and reset passwords.|[Reset a password](https://www.alibabacloud.com/help/zh/doc-detail/54544.htm)|
|Connection Info|You can view the endpoints and port numbers of the instance.|N/A|
|Backup and Recovery|Backups|You can view and download a list of data backups for a specified time period, restore data from the specified time period, or create an instance from a specified backup point.|-   [Download backup data](https://www.alibabacloud.com/help/zh/doc-detail/55011.htm)
-   [Restore data to an instance](https://www.alibabacloud.com/help/zh/doc-detail/55015.htm) |
|Backup Settings|You can set a backup policy to automatically and periodically back up data based on the specified backup time.|[Configure automatic backup for an instance](https://www.alibabacloud.com/help/zh/doc-detail/55008.htm)|
|Monitoring Info|Resource monitoring|You can view the monitoring information of the primary and secondary nodes based on the specified metrics and time range.|N/A|
|Alert Rules|Set Alert Rule|You can set alert rules.|[Set alert rules](https://www.alibabacloud.com/help/zh/doc-detail/61585.htm)|
|Data Security|Whitelist Settings|You can configure an IP whitelist.|[Configure an IP whitelist](https://www.alibabacloud.com/help/zh/doc-detail/54529.htm)|

