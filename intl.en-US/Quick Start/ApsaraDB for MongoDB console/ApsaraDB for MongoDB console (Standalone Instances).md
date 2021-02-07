# ApsaraDB for MongoDB console \(Standalone Instances\)

The ApsaraDB for MongoDB console is a web application for managing instances. In the ApsaraDB for MongoDB console, you can create and manage instances, configure the instance IP whitelists, passwords, and network types, and perform other operations.

The ApsaraDB for MongoDB console is a part of the Alibaba Cloud Management Console. For more information about general settings and basic operations in the console, see the [Alibaba Cloud Management Console](https://www.alibabacloud.com/help/zh/doc-detail/47605.htm).

## Prerequisites

An Alibaba Cloud account is used. To create an Alibaba Cloud account, go to the [Alibaba Cloud official website](https://account.alibabacloud.com/register/intl_register.htm).

## ApsaraDB for MongoDB console homepage

The console homepage displays the same information for all standalone instances.

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) and go to the Instances page, as shown in the following figure. This figure is only to be used for reference. The actual page may be different.

![ApsaraDB for MongoDB console homepage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9698106951/p13185.png)

UI element description

|No.|UI element|Description|
|:--|:---------|:----------|
|1|Replica Set Instances|The ApsaraDB for MongoDB console homepage, which displays all standalone o replica set instances in a region that belong to the current account.|
|2|Region|You can click a region to display all instances that reside within the region.|
|3|Create Instance|The button to [Create a standalone instance](/intl.en-US/Quick Start/Create an instance/Create a standalone instance.md).|
|4|Refresh|The button to refresh the instance information page.|
|5|Export|The button to [Export the list of instances](/intl.en-US/User Guide/Instance management/Export the list of instances.md).|
|6|Instance ID|You can click an instance ID to go to the Basic Information page of the instance.|
|7|Status|The status of the instance. Instances may be in different states.|
|8|Manage|You can click this button to go to the Basic Information page of the instance. On this page, you can view the basic information about the instance, configure instance backup and recovery, [view monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md), and [configure a whitelist]().|
|9|Restart|The button to [restart an instance](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.md).|
|10|More|Other buttons, such as [Change Configuration](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md) and Renew.|
|11|Edit icon|You can click this icon to modify the instance name. By default, the instance name is identical to the instance ID.|

## ApsaraDB for MongoDB instance console

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Click an **Instance ID** or **Manage** in the Actions column corresponding to an instance. The Basic Information page is displayed. The following table lists the UI elements on the page.

|UI element or page|Section|Description|Operation|
|:-----------------|:------|:----------|:--------|
|Top navigation bar|-|You can migrate, back up, and restart the instance.|-   [Migrate the data of an instance](/intl.en-US/User Guide/Data migration and synchronization/Overview.md)
-   [Log on to a database](/intl.en-US/Quick Start/Connect to an instance/Connect to a standalone ApsaraDB for MongoDB instance by using DMS.md)
-   [Back up an instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md)
-   [Restart an instance](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.md) |
|Basic Information|Basic Information|You can view the basic information about the instance, such as the instance ID, region, network type, specifications, and disk space. You can also change the configurations of the instance.|[Change the configurations of an instance](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md)|
|Connection Info|You can view the public and internal IP addresses of the instance.|N/A|
|Specification Information|You can view the specification details and disk space usage of the instance.|N/A|
|Accounts|N/A|You can view account information and reset passwords.|[Reset a password](/intl.en-US/User Guide/Account management/Reset the password for an ApsaraDB for MongoDB instance.md)|
|Backup and Recovery|Backups|You can view and download a list of data backups for a specified time period, restore data from the specified time period, or create an instance from a specified backup point.|-   [Create an instance from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md) |
|Backup Settings|You can set a backup policy to automatically and periodically back up data based on the specified backup time.|[Configure automatic backup for an instance](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md)|
|Monitoring Info|N/A|You can view the monitoring information of the primary node based on the specified metrics and time range.|[View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md)|
|Data Security|Whitelist Settings|You can configure an IP whitelist.|[Configure an IP whitelist]()|

