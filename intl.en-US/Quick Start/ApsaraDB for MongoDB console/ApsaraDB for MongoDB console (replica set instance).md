# ApsaraDB for MongoDB console \(replica set instance\)

The ApsaraDB for MongoDB console is a web application for managing instances. In the ApsaraDB for MongoDB console, you can create instances and configure the instance IP whitelists, passwords, and network types.

The ApsaraDB for MongoDB console is part of the Alibaba Cloud Management Console. For more information about common settings and basic operations in the Alibaba Cloud Management Console, see [Alibaba Cloud Management Console](https://www.alibabacloud.com/help/zh/doc-detail/47605.html).

## Prerequisites

An Alibaba Cloud account is used. To create an Alibaba Cloud account, go to the [Alibaba Cloud official website](https://account.aliyun.com/register/register.htm).

## ApsaraDB for MongoDB console homepage

The console homepage displays the same information for all replica set instances.

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) and go to the **Replica Set Instances** page, as shown in the following figure. This figure is used only for reference. The actual page content may be different.

![ApsaraDB for MongoDB console homepage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7998026061/p13769.png)

UI element description

|No.|UI element|Description|
|:--|:---------|:----------|
|1|Replica Set Instances|The ApsaraDB for MongoDB console homepage, which displays all replica set instances in a region that belong to the current account.|
|2|Resource Groups and Regions|After you select a resource group and region, all instances in the selected resource groups and regions are displayed.|
|3|Refresh|The button to refresh the instance information page.|
|4|Create Instance|The button to create an instance. For more informaiton, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md).|
|5|Instance ID/Name|You can click an instance ID to go to the Basic Information page of the instance.|
|6|Status|The status of the instance. Instances may be in different states.|
|7|Manage|You can click this button to go to the Basic Information page of the instance. On this page, you can view the basic information about the instance, configure instance backup and recovery, view monitoring information, set alert rules, and configure a whitelist. For more information, see [View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md), [Set alert rules](/intl.en-US/User Guide/Monitoring and alerting/Set alert rules.md), and [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md).|
|8|Restart|[Restart an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.md).|
|9|More|Other buttons such as [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md) and [Release an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Release an ApsaraDB for MongoDB instance.md).|
|10|Edit icon|You can click this icon to modify the instance name. By default, the instance name is identical to the instance ID.|
|11|Export|[Export the list of instances](/intl.en-US/User Guide/Instance management/Export the list of instances.md).|

## ApsaraDB for MongoDB instance console

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Click **Instance ID/Name**. The Basic Information page is displayed. The following table lists the UI elements on the page.

|UI element or page|Section|Description|Operation|
|:-----------------|:------|:----------|:--------|
|Top navigation bar|-|You can migrate, back up, and restart the instance.|-   [Connect to a replica set ApsaraDB for MongoDB instance by using DMS](/intl.en-US/Quick Start/Connect to an instance/Connect to a replica set ApsaraDB for MongoDB instance by using DMS.md)
-   [Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB
         by using DTS.md)
-   [Manually back up an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md)
-   [Restart an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.md) |
|Basic Information|**Basic Information**|You can view the basic information about the instance, such as the instance ID and network type. You can also change the configurations of the instance.|[Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md)|
|**Accounts**|You can view account information and reset passwords.|[Reset the password](/intl.en-US/Quick Start/Reset the password.md)|
|**Database Connection**|You can view the connection addresses of nodes.|[Overview of replica set instance connections]()|
|**Backup and Recovery**|You can configure the automatic backup feature for an instance, manage backup data, and create an instance based on a point of time.|-   [Configure automatic backup for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md)
-   [Restore data to a new ApsaraDB for MongoDB instance by point in time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md) |
|**Monitoring Info**|You can view the resource usage of an instance.|[View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md)|
|**Alert Rules**|You can set alert rules of instances.|[Set alert rules](/intl.en-US/User Guide/Monitoring and alerting/Set alert rules.md)|
|**Service Availability**|You can manually switch the role of an instance node.|[Switch node roles](/intl.en-US/User Guide/Instance management/Switch node roles.md)|
|**Parameter List**|You can set database parameters.|[Configure database parameters for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Parameter settings/Configure database parameters for an ApsaraDB for MongoDB instance.md)|
|**Data Security**|You can configure data security, such as whitelists, audit logs, SSL, and TDE.|-   [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md)
-   [Configure SSL encryption for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure SSL encryption for an ApsaraDB for MongoDB instance.md)
-   [Configure TDE for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure TDE for an ApsaraDB for MongoDB instance.md)
-   [Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md) |
|**Logs**|You can view the operational log of the database.|[Overview](/intl.en-US/User Guide/Log management/Overview.md)|
|**CloudDBA**|You can use Database Autonomy Service \(DAS\) to analyze data stored in ApsaraDB for MongoDB.|-   [Real-time performance](/intl.en-US/User Guide/CloudDBA/Real-time performance.md)
-   [Instance sessions](/intl.en-US/User Guide/CloudDBA/Instance sessions.md)
-   [Capacity analysis](/intl.en-US/User Guide/CloudDBA/Capacity analysis.md)
-   [Slow query logs](/intl.en-US/User Guide/CloudDBA/Slow query logs.md) |

