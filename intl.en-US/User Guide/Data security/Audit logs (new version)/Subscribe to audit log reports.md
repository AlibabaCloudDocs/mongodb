# Subscribe to audit log reports

You can subscribe to audit log reports of ApsaraDB for MongoDB through emails or the DingTalk ChatBot. This allows you to retrieve information about ApsaraDB for MongoDB regularly.

You have enabled the new audit log feature. For more information, see [Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md).

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane of the **Instance** page, choose **Data Security** \> **Audit Logs**.

6.  On the **Mongo audit log center** page, click **Subscribe** in the upper-right corner.

    ![Click Subscribe.](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7528449951/p99399.png)

7.  In the **Subscription Configuration** step, complete the settings and click **Next** at the lower part of the page.

    The following table describes the parameters on the Subscription Configuration page.

    |Parameter|Description|
    |---------|-----------|
    |Subscription Name|The description of the subscription. You can customize the description.|
    |Frequency|Specifies the frequency at which ApsaraDB for MongoDB sends the reports.|
    |Add Watermark|After you enable this feature, the images in the reports are watermarked with the email address or the WebHook URL.|

8.  In the **Notifications** step, click the drop-down list on the right and select a notification method.

    ![Add a notification method](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7528449951/p99421.png)

    **Note:** The available notification methods are **Email** and **WebHook-DingTalk Bot**. You can choose one or both of them.

9.  Specify the **Recipients** of the **Email** or enter the **Request URL** of the **WebHook-DingTalk Bot**, and then click **Submit** at the lower part of the page.


**Related topics**  


[Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md)

[Overview](/intl.en-US/User Guide/Log management/Overview.md)

[Slow query logs](/intl.en-US/User Guide/CloudDBA/Slow query logs.md)

