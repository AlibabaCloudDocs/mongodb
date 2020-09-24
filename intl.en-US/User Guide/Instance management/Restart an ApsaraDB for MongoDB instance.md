# Restart an ApsaraDB for MongoDB instance

This topic describes how to restart an ApsaraDB for MongoDB instance when the number of connections exceeds the upper limit or the performance of the instance deteriorates.

## Precautions

-   When you restart an instance, all its nodes are restarted in turn and each node has a brief disconnection of about 30 seconds. If the instance houses more than 10,000 collections, the brief disconnections last longer. Therefore, we recommend that you restart an instance during off-peak hours or make sure that your application is configured to reconnect to the instance after it is disconnected.
-   When you restart a replica set instance, a primary/secondary switchover may occur and cause the roles of connected nodes to change. We recommend that you use a connection string URI to connect to the instance to avoid impact on the read/write operations of your application. For more information, see [Overview of replica set instance connections](/intl.en-US/Quick Start for Replica Set/Connect to an instance/Overview of replica set instance connections.md).
-   You can restart a sharded cluster instance, or a mongos or shard in the instance. This kind of nodes are inaccessible until restarted.

## Restart an instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and choose **![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Restart** in the **Actions** column.

    **Note:** Alternatively, you can click the ID of the target instance. On the **Basic Information** page that appears, click **Restart Instance** in the upper-right corner.

5.  In the **Restart Instance** message that appears, click **OK**.

    The instance status changes to **Rebooting**. When the instance enters the **Running** state, the restart is complete.


## Restart a node in a sharded cluster instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  Follow these steps to restart a node:

    -   Restart a mongos.

        In the **Mongos List** section, find the target mongos and choose **![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Restart** in the Operation column.

        ![Restart a mongos](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0935298951/p11719.png)

    -   Restart a shard.

        In the **Shard List** section, find the target shard and choose **![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Restart** in the Operation column.

        ![Restart a shard](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0935298951/p37111.png)

6.  In the **Restart Node** message that appears, click **OK**.

    The instance status changes to **Rebooting**. When the instance enters the **Running** state, the restart is complete.


