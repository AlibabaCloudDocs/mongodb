# Change the configuration of a sharded cluster instance

You can change the configuration of a sharded cluster instance if the configuration is excessive or cannot meet the performance requirements of an application.

## Precautions

-   To ensure data security, you can add shard nodes but cannot delete shard nodes.
-   When you add a shard node, the specifications of the shard node must be the same as or higher than the specifications of the shard node that has the highest specifications in the current instance.
-   When you change the configuration of a shard node, the new storage space must be larger than the storage space occupied by the current shard node.
-   You cannot change the instance type or the storage engine of a sharded cluster instance. You may create an instance to change the instance type or storage engine of a sharded cluster instance. However, this causes a long downtime and affects your business. We do not recommend this method.

## Billing rules

For more information, see [Configuration change fees](/intl.en-US/Purchase Guide/Configuration change fees.md).

## Impacts

-   Configuration changes do not cause data loss.
-   You cannot specify switching time for the changed configuration of a sharded cluster instance. After you change the configuration in the console, the instance state immediately changes to **Changing Configuration**. When the instance is in this state, most operations related to databases, accounts, and network cannot be performed. This results in one or two transient connection errors of up to 30 seconds.
-   The durationrequired for a configuration change varies based on multiple factors such as network conditions, task queues, and data volume. We recommend that you change configurations during off-peak hours and make sure that your applications are configured with automatic reconnection policies.
-   To ensure better performance and stability of the instance, the system will upgrade the minor version to the latest version by default. If the minor version of your instance expires or is not included in the maintenance list and the instance is [upgraded](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md), [migrated](/intl.en-US/User Guide/Data migration and synchronization/Overview.md), [changed](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md), [Created from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Created by point-in-time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), or performed [Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md).

## Add a node

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  On the **Basic Information** page, perform the following operations.

    To add a mongos node, perform the following operations:

    1.  In the **Mongos List** section, click **Add Mongos**.

    2.  On the Add Mongos page, specify **Specification** of the mongos node.

    To add a shard node, perform the following operations:

    1.  In the **Shard List** section, click **Add Shard**.

    2.  In the Add Shard panel, specify **Specifications** and **Storage Capacity** for the shard node.

6.  Select **ApsaraDB for MongoDB Terms of Service** and complete the payment.


## Change the configuration of an existing node

For more information about instance specifications, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  On the **Basic Information** page, change the required of the corresponding node.

    To change the configuration of a mongos node, perform the following operations:

    1.  In the **Mongos List** section, find the mongos node for which you want to change the configuration and choose **![More icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Change Configuration**.

        ![Change the configuration of a mongos node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3735298951/p21057.png)

    2.  On the Change Configuration Mongos page, specify **Specification** of the mongos node.

    To change the configuration of a shard node, perform the following operations:

    1.  In the **Shard List** section, find the shard node for which you want to change the configuration and choose **![More icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Change Configuration**.

        ![Change the configuration of a shard node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4735298951/p21056.png)

    2.  In the Change Configuration panel, specify **Specifications** and **Storage** of the shard node.

        **Note:** You cannot downgrade the storage space of the shard node when the configuration is changing. You can use other methods to downgrade the storage space. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

6.  Select **ApsaraDB for MongoDB Terms of Service** and complete the payment.


When the instance state changes to **Running**, the configuration is changed.

