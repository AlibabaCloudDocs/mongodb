# Set common alert rules for ApsaraDB for MongoDB

ApsaraDB for MongoDB provides the instance monitoring and alerting feature. This topic describes how to configure common metrics such as disk usage, input/output operations per second \(IOPS\), connections, and CPU utilization.

## Background information

-   With the growth of business data, more performance resources of ApsaraDB for MongoDB instances are consumed. Sometimes performance resources may even be used up.
-   For example, when a great number of slow queries occur, writing a large amount of data causes performance resources of ApsaraDB for MongoDB instances exceptionally consumed.

    **Note:** Instances with insufficient disk space may be locked. If an instance is locked, you can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex). After that, you can increase disk space with the [configuration change](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md) feature.


You can set alert rules for key performance metrics of instances to help you detect abnormal data and troubleshoot errors.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Alert Rules**.

6.  Click **Set Alert Rule**. You are redirected to the Cloud Monitor console.

7.  On the Threshold Value Alert tab of the Cloud Monitor console, click **Create Alert Rule** in the upper-right corner.

8.  On the Create Alert Rule page, configure related resource parameters.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6829256951/p35063.png)

    |Parameter|Description|
    |:--------|:----------|
    |Products|The architecture type of the instance. Valid values:     -   ApsaraDB for MongoDB-Instance Copy
    -   ApsaraDB for MongoDB-Cluster Instance
    -   ApsaraDB for MongoDB-Single Node Instance
**Note:** If you select **ApsaraDB for MongoDB-Cluster Instance**, you must specify the **mongos** and **shard** nodes to be monitored. |
    |Resource Range|    -   **All Resources**: The alert rule is applicable to all ApsaraDB for MongoDB instances.
    -   **Instances**: The alert rule is applicable to the specified ApsaraDB for MongoDB instances. |
    |Region|The region where the instance is deployed.|
    |Instances|The ID of the instance. You can select multiple instance IDs.|

9.  Set alert rules. You can set the disk usage first, and then click **Add Alert Rule**

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6829256951/p35064.png)

    **Note:**

    -   If you set Rule Description to Disk Usage 5mins Average \>= 80%, the alerting module checks the disk usage every 5 minutes to detect whether the average disk usage in the last 5 minutes is greater than or equal to 80%. You can adjust each alert threshold based on your business scenarios.
    -   If you select AnyRole for the Role parameter, the primary and secondary nodes for each instance are monitored.
10. Set alert rules for IOPS, connections, and CPU utilization in the similar way to disk usage.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6829256951/p35065.png)

11. Set other parameters for alert rules.

    |Parameter|Description|
    |:--------|:----------|
    |Mute for|Specifies the mute period. If the alert is not cleared within the mute period, a new alert notification is sent when the mute period ends.|
    |Effective Period|The period when the alert rule takes effect.|

12. Set the notification method.

    |Parameter|Description|
    |:--------|:----------|
    |Notification Contact|The contacts or contact group to which an alert notification is sent. For more information, see [Manage an alert contact or alert group](https://www.alibabacloud.com/help/zh/doc-detail/28609.htm).|
    |Notification Methods|The notification methods corresponding to an alert severity, which can be Critical, Warning, or Info.     -   Critical: phone calls, SMS messages, emails, and DingTalk ChatBot.
    -   Warning: SMS messages, emails, and DingTalk ChatBot.
    -   Info: emails and DingTalk ChatBot. |
    |Email Subject|The subject of the alert notification email. The default email subject is in the format of service name + metric name + instance ID.|
    |Email Remark|The custom additional information in the alert notification email. Remarks will be included in the alert notification email if you specify this parameter.|
    |HTTP Callback|For more information, see [Use the alert callback feature](https://www.alibabacloud.com/help/zh/doc-detail/60714.htm).|

13. Click **Confirm**. Alert rules automatically take effect.


