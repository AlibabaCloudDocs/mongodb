# Trigger a primary/secondary failover for a replica set instance {#task_phh_vjh_kfb .task}

An ApsaraDB for MongoDB replica set instance consists of three nodes by default. ApsaraDB for MongoDB provides addresses for you to connect to the primary node and a secondary node. The other secondary node is hidden as a backup to guarantee high availability. If a node is faulty, the high availability system of ApsaraDB for MongoDB automatically triggers a primary/secondary failover to guarantee the availability of the instance. In addition, you can manually trigger a primary/secondary failover for an ApsaraDB for MongoDB instance in scenarios such as routine disaster recovery drills.

After you log on to the ApsaraDB for MongoDB console or call the SwitchDBInstanceHA operation to trigger a primary/secondary failover for a replica set instance, ApsaraDB for MongoDB interchanges the roles of the primary and secondary nodes.

**Note:** 

-   You can trigger a primary/secondary failover only for replica set and sharded cluster instances, but not for standalone instances due to their single-node architecture.
-   After you trigger a primary/secondary failover for an instance, the instance may be disconnected for 30s once. You need to ensure that your applications can automatically re-establish a connection.
-   You can trigger a primary/secondary failover only for instances in the normal running status.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the **Node List** area, click **Failover**, as shown in the following figure. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6740/155617805713848_en-US.png)

6.  In the Failover dialog box that appears, click **OK**.
7.  The instance enters the **HA Switching** status. The failover is successful when the instance status changes to **Running**. 

    The failover takes about 1 minute. Then, the instance returns to normal.

    **Note:** If you have used the address of the primary node to connect to an instance, you are connecting to a secondary node after a failover and you have no write permission on the instance. In this case, you need to use the address of the new primary node to connect to the instance to obtain read and write permissions. For more information, see [Obtain the replica set instance connection information](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Obtain the replica set instance connection information.md#).


