# View performance trends of an ApsaraDB for MongoDB instance

CloudDBA provides the performance trends feature to monitor the basic performance metrics and the corresponding performance trends of an ApsaraDB for MongoDB instance over a specified time range. The basic performance metrics include CPU utilization, memory usage, total number of connections, and network traffic. This topic describes how to view performance trends of an ApsaraDB for MongoDB instance.

## Precautions

CloudDBA is not supported in MongoDB V4.4 and unavailable for ApsaraDB for MongoDB \(Serverless\) instances.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **CloudDBA** \> **Performance**.


## Nodes

On the page that appears, you can view the **node ID**, **role**, **specifications**, **maximum number of connections**, **CPU utilization**, and **memory usage** in the **Nodes** section.

**Note:** The **Nodes** section is not displayed if the instance is a standalone instance.

![Nodes](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1731825161/p211061.png)

## Performance trends

This section provides the **Performance Trends**, **Performance Trend Comparison**, and **Custom Chart** tabs.

-   **Performance Trends**: displays trend charts of metrics over a specified time range. Each chart visualizes a metric.

    ![Performance Trends](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1624775161/p211324.png)

-   **Performance Trend Comparison**: displays trend charts of metrics over two specified time ranges. For example, the following figure shows the trend charts over the same time range on January 07, 2021 and January 08, 2021. The trend comparison chart helps you identify performance regressions and investigate the cause. Each chart visualizes a metric.

    ![Performance Trend Comparison](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1624775161/p211328.png)

-   **Custom Chart**: You can present multiple metrics in one trend chart over a specified time range. Each chart visualizes multiple metrics. For more information, see [Customize a performance trend chart](/intl.en-US/User Guide/CloudDBA/Customize a performance trend chart.md).

    ![Custom Chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1624775161/p211352.png)


**Note:**

-   By default, **Correlation** is enabled. When you move the pointer over a chart to view the performance data of the instance at 09:00:00, all charts display the corresponding performance data.
-   In the upper-right corner of the chart that you want to view, you can click **Definition?** to view the definitions of metrics and click **Details** to view a larger performance trend chart.

