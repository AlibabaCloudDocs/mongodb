# ApsaraDB for MongoDB console \(Standalone instances\)

The ApsaraDB for MongoDB console is a web application for managing instances. In the ApsaraDB for MongoDB console, you can create and manage instances, configure the instance IP whitelists, passwords, and network types, and perform other operations.

The ApsaraDB for MongoDB console is part of the Alibaba Cloud Management Console. For more information about common settings and basic operations in the Alibaba Cloud Management Console, see [Alibaba Cloud console](https://www.alibabacloud.com/help/zh/doc-detail/47605.htm).

## Prerequisites

An Alibaba Cloud account is used. To create an Alibaba Cloud account, click [Create Your Alibaba Cloud Account](https://account.alibabacloud.com/register/intl_register.htm).

## ApsaraDB for MongoDB console homepage

The console homepage shows the same information for all standalone instances.

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) and go to the **Replica Set Instances** page as shown in the following figure.

![ApsaraDB for MongoDB console homepage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9698106951/p13185.png)

UI element description

|No.|UI element|Description|
|:--|:---------|:----------|
|1|Replica Set Instances|The ApsaraDB for MongoDB console homepage, which shows all replica set instances in a region that belong to the account.|
|2|Resource group and region|Selects a resource group and region to show all instances that reside within the resource group and region.|
|3|Refresh|The button to refresh the instance information page.|
|4|Create Instance|The button to create a standalone instance. For more information, see [Create a standalone instance](/intl.en-US/Quick Start/Create an instance/Create a standalone instance.md).|
|5|The ID of the instance.|Clicks an instance ID to go to the Basic Information page of the instance.|
|6|Status|The status of the instance. Instances may be in different states.|
|7|Manage|Clicks this button to go to the Basic Information page of the instance. On this page, you can view the basic information of the instance, configure instance backup and restoration, view monitoring information, and configure a whitelist. For more information, see [View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md) and [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md).|
|8|Restart|The button to restart an ApsaraDB for MongoDB instance. For more information, see [Restart an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.md).|
|9|More|Other buttons such as change configurations and release an instance. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md) and [Release an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Release an ApsaraDB for MongoDB instance.md).|
|10|Edit icon|Clicks this icon to modify the instance name. By default, the instance name is identical to the instance ID.|
|11|Export|The button to export the list of instances. For more information, see [Export the list of instances](/intl.en-US/User Guide/Instance management/Export the list of instances.md).|

## ApsaraDB for MongoDB instance console

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Click **Instance ID/Name** in the Actions column corresponding to an instance. The Basic Information page is displayed. The following table lists the UI elements on the page.

|UI element or page|Section|Description|Operation|
|:-----------------|:------|:----------|:--------|
|Top navigation bar|-|Migrates, backs up, and restarts the instance.|-   [Connect to a standalone ApsaraDB for MongoDB instance by using DMS](/intl.en-US/Quick Start/Connect to an instance/Connect to a standalone ApsaraDB for MongoDB instance by using DMS.md)
-   [Migrate self-managed standalone MongoDB databases to Alibaba Cloud by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate self-managed standalone MongoDB databases to Alibaba Cloud by using DTS.md)
-   [Manually back up an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md)
-   [Restart an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.md) |
|Left-side navigation pane|**Basic Information**|Views the basic information of the instance, such as the instance ID, and network type. You can also change the configurations of the instance.|[Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md)|
|**Accounts**|Views account information and resets passwords.|[Reset the password](/intl.en-US/Quick Start/Reset the password.md)|
|**Database Connections**|Views the endpoint of the node.|[Overview of replica set instance connections]()|
|**Backup and Recovery**|Configures automatic backup for an instance, manages backup data, and creates an instance by time point.|[Configure automatic backup for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md)|
|**Monitoring Data**|Queries the resource usage of an instance.|[View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md)|
|**Alert Rules**|Sets alert rules of an instance.|[Configure alert rules](/intl.en-US/User Guide/Monitoring and alerting/Configure alert rules.md)|
|**Service Availability**|Views the zone distribution of the instance.|N/A|
|**Parameter List**|Sets database parameters.|[Configure database parameters for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Parameter settings/Configure database parameters for an ApsaraDB for MongoDB instance.md)|
|**Data Security**|The security configurations of the instance such as whitelists, SSL, and TDE.|[Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md)|
|**Logs**|Standalone instances do not support this feature.|N/A|
|**CloudDBA**|Use Database Autonomy Service \(DAS\) to analyze ApsaraDB for MongoDB databases.|-   [View performance trends of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/CloudDBA for performance diagnostics and optimization/View performance trends of an ApsaraDB for MongoDB instance.md)
-   [Real-time performance](/intl.en-US/User Guide/CloudDBA for performance diagnostics and optimization/Real-time performance.md)
-   [Instance sessions](/intl.en-US/User Guide/CloudDBA for performance diagnostics and optimization/Instance sessions.md)
-   [Capacity analysis](/intl.en-US/User Guide/CloudDBA for performance diagnostics and optimization/Capacity analysis.md)
-   [Slow query logs](/intl.en-US/User Guide/CloudDBA for performance diagnostics and optimization/Slow query logs.md) |

