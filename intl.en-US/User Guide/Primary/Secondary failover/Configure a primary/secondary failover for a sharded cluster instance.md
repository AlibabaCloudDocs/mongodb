# Configure a primary/secondary failover for a sharded cluster instance

By default, each shard of an ApsaraDB for MongoDB sharded cluster instance contains three nodes. When a node fails, the high availability system of ApsaraDB for MongoDB automatically triggers a primary/secondary failover to ensure the overall availability. You can also manually trigger a primary/secondary failover for an ApsaraDB for MongoDB instance in scenarios such as routine disaster recovery drills.

## Usage notes

ApsaraDB for MongoDB provides connection strings for you to connect to the primary node and a secondary node. The other secondary node is hidden as a backup to ensure high availability. After you log on to the ApsaraDB for MongoDB console or call the [SwitchDBInstanceHA](/intl.en-US/API Reference/Instance management/SwitchDBInstanceHA.md) operation to trigger a primary/secondary failover for a shard of a sharded cluster instance, ApsaraDB for MongoDB switches the roles of the primary and secondary nodes.

**Note:**

-   You can trigger a primary/secondary failover for replica set and sharded cluster instances, but not for standalone instances due to their single-node architecture.
-   You can trigger a primary/secondary failover only for shards in the running state.
-   Each time you trigger a primary/secondary failover for an instance, the instance may encounter a transient connection error of about 30 seconds. We recommend that you perform this operation during off-peak hours and make sure that your applications can automatically re-establish a connection.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the **Shard List** section, find the shard node and choose **![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Failover**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6511715061/p13849.png)

    You can trigger a primary/secondary failover separately for each shard node. The failover operation takes effect only for the current shard node and does not affect other shard nodes of the same sharded cluster instance.

6.  In the **Failover**dialog box, select **Effective At** and click **Submit**.

    **Note:** **Failover** supports two types of **Effective At**:

    -   **Effective Immediately**: The system immediately performs a primary/secondary failover.
    -   **Maintenance Window**:The system performs a primary/secondary failover within the specified maintenance window. For more information about how to set the maintenance time, see [Specify a maintenance period](/intl.en-US/User Guide/Instance management/Specify a maintenance period.md).
7.  The instance status changes to **HA Switching**.The failover is successful when the instance status changes back to **Running**.

    **Note:** The failover operation is complete in about 1 minute. You can repeat the preceding procedure to trigger a primary/secondary failover for other shards of the same sharded cluster instance.


