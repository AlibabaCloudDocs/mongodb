# ApsaraDB for MongoDB console {#concept_pp1_vyq_52b .concept}

The [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) is a Web application for managing MongoDB instances. In the ApsaraDB for MongoDB console, you can create and manage instances, configure the instance IP whitelists, passwords, and network types, and perform other operations.

The ApsaraDB for MongoDB console is part of the Alibaba Cloud console. For more information about common settings and basic operations in the Alibaba Cloud console, see [Alibaba Cloud console](https://www.alibabacloud.com/help/zh/doc-detail/47605.html).

## Prerequisites {#section_a3c_t2h_hfb .section}

Use your Alibaba Cloud account to log on to the ApsaraDB for MongoDB console. If you do not have an Alibaba Cloud account, click [Register](https://account.aliyun.com/register/register.htm).

## Homepage {#section_bnm_4gh_hfb .section}

The console homepage displays the same information for all MongoDB sharded cluster instances.

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) and go to the Instances page, as shown in the following figure. This figure is only to be used for reference. The actual page may be different.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6687/155927160313822_en-US.png)

UI element description

|No.|UI element|Description|
|:--|:---------|:----------|
|1|Sharding Instances|The ApsaraDB for MongoDB console homepage, which displays all instances in a region that belong to the current account.|
|2|Region|You can click a region to display all instances that reside within the region.|
|3|Refresh|The button to refresh the instance information page.|
|4|Create Instance|[The button to create a new instance](https://www.alibabacloud.com/help/zh/doc-detail/55137.htm).|
|5|Instance ID| -   You can click an instance ID to go to the Basic Information page of the instance.
-   You can click the icon following an instance ID to modify the name of the instance.

 |
|6|Running Status|The status of the instance. Instances may be in different states.|
|7|Management icon|You can click this icon to manage, restart, or release an instance.|

## MongoDB instance console {#section_r2s_zhh_hfb .section}

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Click the management icon in the Actions column corresponding to an **Instance ID** and choose **Manage** from the shortcut menu. The Basic Information page is displayed. The following table lists the parameters on the page.

|Page name|Area|Description|Link of common operation|
|:--------|:---|:----------|:-----------------------|
|Operation area in the window|-|You can back up and restart instances.| -   Back up an instance
-   
 |
|Basic Information|Basic Information|You can view the basic information of an instance, such as its ID, region, network type, and storage engine.|-|
|Specifications|You can view instance specifications such as the database version, maintenance period, billing method, creation time, and expiration time.|[Specify a maintenance period](../../../../intl.en-US/User Guide/Instance management/Specify a maintenance period.md#)|
|Mongos Nodes or Shard Nodes| -   In the mongos list, you can locate a mongos ID and click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6687/155927160348346_en-US.png) icon to change its configurations, and log on to or restart the mongos.
-   In the shard list, you can locate a shard ID and click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6687/155927160348346_en-US.png) icon to log on to a shard, restart the shard, trigger a failover, or change the shard configurations.
-   Database read and write operations may fail when you restart nodes. We recommend that you do not perform the Create, Retrieve, Update, and Delete \(CRUD\) operations on databases when you restart nodes.

 | -   [Trigger a failover](../../../../intl.en-US/User Guide/Primary__Secondary failover/Trigger a primary__secondary failover for a shard of a sharded cluster instance.md#ul_bl4_fkh_kfb)
-   [Change configurations](../../../../intl.en-US/User Guide/Instance management/Change the configuration.md#section_lzh_wn4_1fb)
-   Log on to a database
-   Restart a node
-   View monitoring information of mongos or shards

 |
|Backup and Restore|-|You can view and download a list of data backups for a specified time period, restore data from the specified time period, or create an instance from a specified backup point.| -   Download backup data.
-   Create an instance at a specified time

 |
|Monitoring information|-|You can view monitoring information of mongos or shards for a specified time period based on specified metrics.|-|
|Security Control|Whitelist Settings|You can configure an IP whitelist.|[Configure a whitelist](intl.en-US/Quick Start for Cluster/Configure a whitelist.md#).|
|Audit Log|MongoDB audit logs record all operations that your perform on a database. You can use these logs in analysis.|[View audit logs](../../../../intl.en-US/User Guide/Data security/Configure log auditing.md#).|

