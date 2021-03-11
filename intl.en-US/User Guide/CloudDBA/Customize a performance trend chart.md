# Customize a performance trend chart

By default, the Performance Trends tab displays the basic performance metrics of a specific ApsaraDB for MongoDB instance. On the Custom Chart tab, you can present multiple specified performance metrics in a customized trend chart to monitor and analyze the performance metrics and the corresponding performance trends. This topic describes how to customize a performance trend chart for an ApsaraDB for MongoDB instance in a dashboard.

## Precautions

CloudDBA is not supported in MongoDB 4.4 and unavailable for ApsaraDB for MongoDB \(Serverless\) instances.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  Click the **Custom Chart** tab.

6.  Create a dashboard.

    1.  Click **Add Monitoring Dashboard**. In the Create Monitoring Dashboard dialog box, set **Dashboard Name**, and click **OK**.

    2.  Click **+Add Chart** or **Add Monitoring Chart**. The **Select Metrics of Monitoring Chart** panel appears. In the Chart Name section, set **Monitoring Chart Name**. In the **Select Metrics** section, select the metrics that you want to analyze and click the ![Icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1721825161/p211424.png) icon.

    3.  Click **OK**.

7.  Manage a dashboard.

    -   View a dashboard

        Select a dashboard that you want to manage, specify a time range, and then click **Search**.

    -   Modify the dashboard

        You can click the icons as shown in the following figure to modify or delete the dashboard.

        ![Modify the dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1721825161/p211482.png)

    -   Delete the dashboard

        Choose **Operate Dashboard** \> **Delete Monitoring Dashboard**. In the message that appears, click **OK**.


