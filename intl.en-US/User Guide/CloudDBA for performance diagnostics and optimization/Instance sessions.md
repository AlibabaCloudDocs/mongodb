# Instance sessions

This topic describes how to view real-time monitoring statistics of your ApsaraDB for MongoDB instances, such as read/write latency, queries per second \(QPS\), operations, connections, and network traffic.

## View instance sessions

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **CloudDBA** \> **Sessions**.

    ![Instance sessions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3645298951/p58965.png)

    **Note:**

    -   If you turn on **Auto Refresh**, the system updates session data on the page every five seconds. By default, the system displays the active sessions. You can turn on the **Display All** switch to view both active and inactive sessions.
    -   In the **Session Statistics** section, you can view information about sessions in the **Overview**, **Statistics by Client**, and **Statistics by Namespace** charts.

## Terminate instance sessions

**Warning:** To avoid unexpected results, we recommend that you do not terminate system-level sessions.

1.  In the Instance Sessions section, select the sessions that you want to terminate, and click **Kill Selected**.

    ![Terminate sessions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1447559951/p58996.png)

2.  In the dialog box that appears, click **OK**.


