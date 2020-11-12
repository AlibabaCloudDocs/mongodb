# Trigger a primary/secondary failover for a shard of a sharded cluster instance

Each shard of a sharded cluster instance consists of three nodes by default. If a node is faulty, the high availability system of ApsaraDB for MongoDB automatically triggers a primary/secondary failover to guarantee the availability of the shard. In addition, you can manually trigger a primary/secondary failover for an ApsaraDB for MongoDB instance in scenarios such as routine disaster recovery drills.

## Notes

ApsaraDB for MongoDB provides addresses for you to connect to the primary node and a secondary node of a shard. The other secondary node is hidden as a backup to guarantee high availability. After you log on to the ApsaraDB for MongoDB console or call the SwitchDBInstanceHA operation to trigger a primary/secondary failover for a shard of a sharded cluster instance, ApsaraDB for MongoDB interchanges the roles of the primary and secondary nodes.

**Note:**

-   You can trigger a primary/secondary failover only for replica set and sharded cluster instances, but not for standalone instances due to their single-node architecture.
-   You can trigger a primary/secondary failover only for shards in the normal running status.
-   After you trigger a primary/secondary failover for an instance, the instance may be disconnected for 30s once. We recommend that you perform this operation during off-peak hours and ensure that your applications can automatically re-establish a connection.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the **Shard List** area, locate the target shard and choose **![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Failover** in the Operation column.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6511715061/p13849.png)

    You can trigger a primary/secondary failover separately for each shard. The failover takes effect only for the current node and does not affect other shards of the same sharded cluster instance.

6.  In the **Failover** dialog box that appears, choose **Effective At** and click **Submit**.

    **Note:** You can set **Effective At** to specify the time when the **Failover** task takes effect. The following options are supported:

    -   **Effective Immediately**: specifies that the system runs the failover task immediately.
    -   **Effective Within Maintenance Window**: specifies that the system runs the failover task within the specified maintenance period. For more information, see [Specify a maintenance period](/intl.en-US/User Guide/Instance management/Specify a maintenance period.md).
7.  The instance status changes to **HA Switching**.The failover is successful when the instance status changes back to **Running**.

    **Note:** The failover takes about 1 minute. You can repeat the preceding procedure to trigger a primary/secondary failover for other shards of the same sharded cluster instance as required.


