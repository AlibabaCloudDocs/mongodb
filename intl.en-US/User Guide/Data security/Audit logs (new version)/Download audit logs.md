# Download audit logs

You can download the queried audit logs to your local server, and then archive, filter, or analyze the logs.

You have enabled the new audit log feature. For more information, see [Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md).

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane of the **Instance** page, choose **Data Security** \> **Audit Logs**.

6.  In the log chart section, choose **![More_Download Log](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6528449951/p77664.png)** \> **Download Log** in the upper-right corner of the target chart.

    **Note:** You can filter logs by using the following methods. Then, you can download the content that meets your requirements.

    -   Filter log data by keyword, type, account, or client IP address. For more information, see [Filter audit logs](/intl.en-US/User Guide/Data security/Audit logs (new version)/Query audit logs.md).
    -   Filter logs by the time when logs are generated. Click **Select Time Range** above the **Download Log** button to select a time range.
    ![Download Log](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9245298951/p102789.png)

    After you click **Download Log**, the selected log entries are saved to a .csv file on your local server through the web browser. Then, you can view the log data by using tools such as Excel.


**Related topics**  


[Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md)

[Overview](/intl.en-US/User Guide/Log management/Overview.md)

[Slow query logs](/intl.en-US/User Guide/CloudDBA/Slow query logs.md)

