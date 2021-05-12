# Switch node roles

You can switch the node roles of an ApsaraDB for MongoDB instance in the ApsaraDB for MongoDB console based on your business deployment.

## Typical scenario

When an Elastic Compute Service \(ECS\) instance and an ApsaraDB for MongoDB instance are in the same zone and connected over an internal network, the latency is minimal. If they are connected across different zones, the latency increases and the performance of ApsaraDB for MongoDB instances and your business is affected.

![Environment for role switching](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5835298951/p54423.png)

In this example, the ECS instance to which the application belongs is in Zone 2. If the primary node of the ApsaraDB for MongoDB instance is in Zone 1, the ECS instance needs to connect to the primary node across zones.

To optimize the business deployment architecture, you can switch the roles of the primary and secondary nodes. In this example, you can change the role of the node in Zone 2 to primary and the role of the node in Zone 1 to secondary. Only the node roles are changed, whereas the zones and role IDs of nodes remain unchanged. ECS and ApsaraDB for MongoDB instances can be connected in the same zone.

## Prerequisites

The instance is a replica set or sharded cluster instance.

## Precautions

-   Each time you switch node roles, the instance may be disconnected within 30 seconds. Perform this operation during off-peak hours or make sure that your application has a reconnection mechanism.
-   Each time you switch node roles, only the node roles are changed, whereas the zones and role IDs of nodes remain unchanged. ECS and ApsaraDB for MongoDB instances can be connected in the same zone.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Service Availability**.

6.  On the **Service Availability** page, perform the following steps based on instance types.

    -   Replica set instance
        1.  In the upper-right corner of the page, click **Switch Role**.
        2.  In the **Switch Role** panel, select the role that you want to switch.

            ![Switch Role](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5835298951/p50552.png)

        3.  Set **Effective At**.
            -   **Effective Immediately**: The system immediately switches the roles of the nodes.
            -   **Effective Within Maintenance Window**: The system switches the roles of the nodes in a maintenance window. You can view the current maintenance window and use one of the following methods to change the maintenance window:
                -   Select a maintenance window from the **Change Maintenance Window** drop-down list.
                -   In the **Specification Information** section, change the maintenance window. For more information, see [Specify a maintenance period](/intl.en-US/User Guide/Instance management/Specify a maintenance period.md).
    -   Sharded cluster instance

        **Note:** For sharded cluster instances, you can manage only the zone distribution of the shard and Configserver nodes.

        1.  In the upper-right corner of the **Zone Distribution for Shards** or **Zone Distribution for Configservers** section, click **Switch Role**.
        2.  In the **Switch Role** panel, select the role that you want to switch.

            ![Switch Role](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5835298951/p50552.png)

        3.  Set **Effective At**.
            -   **Effective Immediately**: The system immediately switches the roles of the nodes.
            -   **Effective Within Maintenance Window**: The system switches the roles of the nodes in a maintenance window. You can view the current maintenance window and use one of the following methods to change the maintenance window:
                -   Select a maintenance window from the **Change Maintenance Window** drop-down list.
                -   In the **Specification Information** section, change the maintenance window. For more information, see [Specify a maintenance period](/intl.en-US/User Guide/Instance management/Specify a maintenance period.md).
7.  Click **Submit**.


