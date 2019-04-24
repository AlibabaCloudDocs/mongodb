# ApsaraDB for MongoDB console {#concept_pp1_vyq_52b .concept}

The [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) is a web application used to manage ApsaraDB for MongoDB instances. You can log on to the ApsaraDB for MongoDB console to create an instance, configure an IP address whitelist, set a password for connecting to the instance, configure the connection information, and perform other operations.

The ApsaraDB for MongoDB console is part of the Alibaba Cloud console. For more information about general settings and basic operations in the console, see [Alibaba Cloud console](https://www.alibabacloud.com/help/zh/doc-detail/47605.html).

## Prerequisites {#section_a3c_t2h_hfb .section}

You have logged on to the ApsaraDB for MongoDB console with your Alibaba Cloud account. If you do not have an Alibaba Cloud account, click [Register](https://account.aliyun.com/register/register.htm).

## Console home page {#section_bnm_4gh_hfb .section}

The information on the home page of the ApsaraDB for MongoDB console is the same for all replica set instances.

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). In the left-side navigation pane, click Replica Set Instances to view the list of instances, as shown in the following figure, which is provided only as an example. The actual GUI prevails.![](images/13769_en-US.png)

GUI element description

|No.|GUI element|Description|
|:--|:----------|:----------|
|1|Replica Set Instances|On the home page of the ApsaraDB for MongoDB console, click it to list the information about all replica set instances of a region under your account.|
|2|Region|Click it to select a region. Then, all instances of this region under your account can be listed.|
|3|Refresh|Click it to refresh the instance list.|
|4|Create Instance|Click it to [create an instance](https://www.alibabacloud.com/help/zh/doc-detail/26572.htm).|
|5|Instance ID|Click an instance ID to go to the details page of this instance.|
|6|Running Status|The running status of an instance. The running status can vary with each instance.|
|7|Manage|Select it to go to the management details page of an instance, on which you can view the basic information about the instance, configure instance backup and recovery, [view the monitoring information](https://www.alibabacloud.com/help/zh/doc-detail/60518.htm), [set alert rules](https://www.alibabacloud.com/help/zh/doc-detail/61585.htm), [configure a whitelist](https://www.alibabacloud.com/help/zh/doc-detail/54529.htm), and perform other operations.|
|8|Restart|Select it to [restart an instance](https://www.alibabacloud.com/help/zh/doc-detail/44658.htm).|
|9|More|Perform more operations, for example, [change the configuration](https://www.alibabacloud.com/help/zh/doc-detail/44655.htm) and [renew an instance](https://www.alibabacloud.com/help/zh/doc-detail/54285.htm).|
|10|Modify the instance alias|Click the pencil icon to modify the alias of an instance. If you do not modify the instance alias, it is the same as the instance ID by default.|

## ApsaraDB for MongoDB instance management details page {#section_r2s_zhh_hfb .section}

Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Click the More icon and select **Manage** in the Operation column corresponding to an instance to go to the Basic Information page of this instance. The following table describes the detailed information on this page.****

|GUI element or page|Area|Description|Common operation and link|
|:------------------|:---|:----------|:------------------------|
|Top navigation bar|-|Migrate data from the user-created MongoDB instance, back up the instance, and restart the instance.| -   [Migrate data from the user-created MongoDB instance](https://www.alibabacloud.com/help/zh/doc-detail/44660.htm)
-   Back up an instance
-   [Restart an instance](https://www.alibabacloud.com/help/zh/doc-detail/44658.htm)

 |
|Basic Information|Basic Information|View the basic information about the instance, including the instance ID, region, network type, specifications, and disk space. Change the configuration of the instance.|[Change the configuration of an instance](https://www.alibabacloud.com/help/zh/doc-detail/44655.htm)|
|Accounts|View the accounts of the instance and reset the password.|[Reset the password](https://www.alibabacloud.com/help/zh/doc-detail/54544.htm)|
|Connection Info|View the domain names and port numbers of the primary and secondary nodes.|-|
|\[DO NOT TRANSLATE\]|\[DO NOT TRANSLATE\]|-|
|\[DO NOT TRANSLATE\]|\[DO NOT TRANSLATE\]|-|
|Backup and Recovery|Backup List|View the backup list based on a specified time range, recover the instance from backup data, create an instance based on a backup, and create an instance based on a time point.| -   [Download backup data](https://www.alibabacloud.com/help/zh/doc-detail/55011.htm)
-   [Recover data](https://www.alibabacloud.com/help/zh/doc-detail/55015.htm)

 |
|Backup Settings|Set a backup policy to automatically and periodically back up data based on the specified backup time.|[Set a backup policy](https://www.alibabacloud.com/help/zh/doc-detail/55008.htm)|
|Monitoring Info|Monitoring Info|View the monitoring information about the primary and secondary nodes of the instance based on the specified metrics and time range.|-|
|Alarm Rules|Set Alarm Rule|Set alert rules.|[Set alert rules](https://www.alibabacloud.com/help/zh/doc-detail/61585.htm)|
|Data Security|Data Security|Configure an IP address whitelist.|[Configure an IP address whitelist](https://www.alibabacloud.com/help/zh/doc-detail/54529.htm)|

