# Trigger a primary/secondary failover for a replica set instance

An ApsaraDB for MongoDB replica set instance consists of three nodes by default. ApsaraDB for MongoDB provides connection strings for you to connect to the primary node and a secondary node. The other secondary node is hidden as a backup to ensure high availability. If a node is faulty, the high availability system of ApsaraDB for MongoDB automatically triggers a primary/secondary failover to ensue the availability of the instance. You also can manually trigger a primary/secondary failover for an ApsaraDB for MongoDB instance in scenarios such as routine disaster recovery drills.

After you log on to the ApsaraDB for MongoDB console or call the [SwitchDBInstanceHA](/intl.en-US/API Reference/Instance management/SwitchDBInstanceHA.md) operation to trigger a primary/secondary failover for a replica set instance, ApsaraDB for MongoDB interchanges the roles of the primary and secondary nodes.

**Note:**

-   You can trigger a primary/secondary failover only for replica set and sharded cluster instances, but not for standalone instances due to their single-node architecture.
-   After you trigger a primary/secondary failover for an instance, a transient connection error of up to 30 seconds will occur to the instance. Ensure that your applications can automatically re-establish a connection.
-   You can trigger a primary/secondary failover only for instances in the running state.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the **Node List** section, click **Failover**, as shown in the following figure.

    ![Primary/secondary failover](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0445298951/p13848.png)

6.  In the **Failover** dialog box, select **Effective At** and click **Submit**.

    **Note:** Valid values for the **Effective At** parameter in the **Failover** dialog box:

    -   **Effective Immediately**: specifies that the system runs the failover task immediately.
    -   **Effective Within Maintenance Window**: specifies that the system runs the failover task within the specified maintenance period. For more information, see [Specify a maintenance period](/intl.en-US/User Guide/Instance management/Specify a maintenance period.md).
7.  The instance status changes to **HA Switching**. The failover is successful when the instance status changes back to **Running**.

    The failover takes about one minute. Then the instance returns to normal.

    **Note:** If you have connected to the connection string of the primary node for an instance, you are connecting to a secondary node after a failover and you have no write permissions on the instance. In this case, you must connect to the connection string of the new primary node and obtain read and write permissions. For more information, see [Overview of replica set instance connections]().


