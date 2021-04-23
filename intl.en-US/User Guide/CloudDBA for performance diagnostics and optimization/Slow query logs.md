# Slow query logs

This topic describes how to view slow query logs of ApsaraDB for MongoDB instances. You can identify, analyze, diagnose, and track slow query logs to create indexes. This improves the utilization of the instance resources.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **CloudDBA** \> **Slow Query Logs**.

    **Note:** By default, slow query logs generated in the past 15 minutes are displayed in the trend chart. You can specify the time range and click **Search** to view slow query logs. The maximum time range is one day.

6.  View details of slow query logs based on the following methods:

    Method 1:

    1.  Click the **Slow Log Details** tab under the trend chart.****

    2.  On the **Slow Log Details** tab, select the database that you want to query.

        **Note:** If the request content of the database is hidden, you can move the pointer over the **request content** and view the complete content.

    Method 2:

    1.  In the trend chart, click the time point of a specific slow query log and view its details on the Slow Log Statistics tab.

        ![View slow query logs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3447559951/p99588.png)

    2.  On the Slow Log Statistics tab, click **Sample** in the **Actions** column.

        In the Slow query log sample dialog box, you can view details of the slow query log.

        ![Slow query log sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3447559951/p58937.png)

        **Note:** If the request content of the database is hidden, you can move the pointer over the **request content** and view the complete content.


## Export slow query logs

You can click Export slow query logs on the **Slow Log Statistics** tab to save the slow query logs information to your computer.

**Related topics**  


[Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md)

[Overview](/intl.en-US/User Guide/Log management/Overview.md)

[Troubleshoot the high CPU utilization of ApsaraDB for MongoDB](/intl.en-US/Best Practices/Performance/Troubleshoot the high CPU utilization of ApsaraDB for MongoDB.md)

