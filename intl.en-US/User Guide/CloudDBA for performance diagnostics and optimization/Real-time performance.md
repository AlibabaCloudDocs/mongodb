# Real-time performance

This topic describes how to view real-time monitoring statistics of your ApsaraDB for MongoDB instances, such as read/write latency, queries per second \(QPS\), operations, connections, and network traffic.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **CloudDBA** \> **Real-time Performance**.

    ![Real-time performance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2645298951/p58848.png)


## Real-time Monitoring

On the Real-time Monitoring page, you can select the Real-time Charts or Mongostat tab to view monitoring statistics. When you refresh or go to the Real-time Monitoring page, the information on the Real-time Charts and Mongostat tabs is refreshed, and the **number of available refreshes** is reset in the upper-right corner.

-   Real-time charts

    ![Real-time charts](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0447559951/p58851.png)

    The Real-time Charts tab is displayed on the Real-time Monitoring page. Line charts on the tab are refreshed every five seconds. In this case, you can view the trend of system performance in real time.

    **Note:** For more information about performance metrics, click the![Info icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0447559951/p58850.png) icon above each chart.

-   mongostat

    ![Mongostat](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0447559951/p58852.png)

    Click the **Mongostat** tab. On the tab, you can view Mongostat command outputs. A new line of performance statistics is added every five seconds. The tab can display a maximum of 999 lines of statistics.

    **Note:** For more information about Mongostat command outputs, see [MongoDB official documentation](https://docs.mongodb.com/manual/reference/program/mongostat/index.html).


