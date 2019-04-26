# Set common alert rules for monitoring ApsaraDB for MongoDB {#concept_azw_yx5_fgb .concept}

ApsaraDB for MongoDB provides an instance status monitoring and alerting feature. This topic describes how to configure common metrics such as the usage of the disk space, input/output operations per second \(IOPS\), connections, and CPU.

## Background {#section_sw3_2y5_fgb .section}

-   With the growth of data and development of business, more and more performance resources of ApsaraDB for MongoDB instances are consumed and even used up.
-   In some scenarios, lots of performance resources of ApsaraDB for MongoDB instances are abnormally consumed. For example, a great number of slow queries increase the CPU usage and a large amount of data is written to fully occupy the disk space.

    **Note:** Instances with insufficient disk space may be locked. If an instance is locked, you can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex). After unlocking the instance, you can [change the configuration](../../../../intl.en-US/User Guide/Instance management/Change the configuration.md#) to increase its disk space.


You can set alert rules for monitoring the key performance metrics of instances to help you detect abnormal data in a timely manner and quickly locate and handle faults.

## Procedure {#section_hpt_fz5_fgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  Locate the target instance and click its instance ID.
4.  In the left-side navigation pane, click **Alarm Rules**.
5.  Click **Set Alarm Rule** to jump to the CloudMonitor console.
6.  In the upper-right corner of the CloudMonitor console, click **Create Alarm Rule**.
7.  On the Create Alarm Rule page that appears, specify related resources.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82713/155624372735063_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Products|The architecture of the instance.     -   ApsaraDB for MongoDB-Instance Copy
    -   ApsaraDB for MongoDB-Cluster Instance
    -   ApsaraDB for MongoDB-Single node instance
 **Note:** If you select **ApsaraDB for MongoDB-Cluster Instance**, you need to select mongos nodes and shards to be monitored for **Mongos** and **Shard**, respectively.

 |
    |Resource Range|     -   If you select **All Resources**, the alerting service sends an alert notification when any ApsaraDB for MongoDB instances match alert rules.
    -   If you select **Instances**, the alerting service sends an alert notification when any selected ApsaraDB for MongoDB instances match alert rules.
 |
    |Region|The region where the instance is located.|
    |Instances|The ID of the instance to be monitored. You can select multiple instance IDs.|

8.  Set alert rules. You need to set the disk space usage first, and then click **Add Alarm Rule**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82713/155624372835064_en-US.png)

    **Note:** 

    -   For example, if you set Rule Describe to Disk Usage 5mins Average \>= 80%, the alerting service checks the disk space usage every 5 minutes to detect whether the average disk space usage in the last 5 minutes is greater than or equal to 80%. You can adjust each alert threshold based on your business scenarios.
    -   If you select AnyRole for Role, the alerting service monitors all primary and secondary nodes for each instance.
9.  Repeat the last step to set alert rules for the usage of the IOPS, connections, and CPU.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82713/155624372835065_en-US.png)

10. Set other parameters for alert rules.

    |Parameter|Description|
    |:--------|:----------|
    |Mute for|The interval at which the alerting service sends an alert notification repeatedly if an alert is not cleared.|
    |Triggered when threshold is exceeded for| The number of consecutive times that the alerting service detects data that exceeds an alert threshold so as to generate an alert. We recommend that you set the value to **3**.

 For example, if you set Rule Describe to CPU Usage 5mins Average \> 80%, the alerting service generates an alert after it detects that the average CPU usage within 5 minutes exceeds 80% three consecutive times.

 |
    |Effective Period|The period during which alert rules take effect.|

11. Configure notification methods.

    |Parameter|Description|
    |:--------|:----------|
    |Notification Contact|The contacts or contact group to which the alerting service sends an alert notification. For more information, see [Manage alert contacts and alert contact groups](https://www.alibabacloud.com/help/doc-detail/28609.htm).|
    |Notification Methods|The notification methods corresponding to the alert severity, which can be Critical, Warning, or Info.     -   Critical: Email + DingTalk
    -   Warning: Email + DingTalk
    -   Info: Email + DingTalk
 |
    |Email Subject|The subject of the alert notification email. You can customize an email subject. The default email subject is as follows: Product + Metric + Instance ID.|
    |Email Remark|The custom additional information of the alert notification email. After you enter email remarks, the alerting service sends an alert notification email that contains your custom remarks.|
    |HTTP CallBack|For more information, see [Use alert callback](https://www.alibabacloud.com/help/doc-detail/60714.htm).|

12. Click **Confirm**. Alert rules automatically take effect.

