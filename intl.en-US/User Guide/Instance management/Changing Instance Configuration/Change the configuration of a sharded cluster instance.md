# Change the configuration of a sharded cluster instance

You can change the configuration of a sharded cluster instance if the configuration is excessive or cannot meet the performance requirements of an application.

## Precautions

-   To ensure data security, you can add shard nodes but cannot delete them.
-   When you change the configuration of a shard node, the new storage space must be larger than the storage space occupied by the current shard node.
-   If the billing method is subscription, you can only upgrade the configuration.

    **Note:** You can use other methods to downgrade the configuration. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

-   You cannot change the instance type or storage engine of a sharded cluster instance. Creating a new instance will cause a long-period shutdown and have a great impact on the business. Therefore, we do not recommend this method.

## Billing rules

For more information, see [Configuration change fees](/intl.en-US/Purchase Guide/Configuration change fees.md).

## Impacts

-   Changing configurations does not cause data loss.
-   You cannot specify switching time for the changed configuration of a sharded cluster instance. After you change the configuration in the console, the instance status changes to **Changing Configuration** immediately. When the instance is in this state, most operations related to databases, accounts, and network cannot be performed. One or two transient disconnections of up to 30 seconds will occur.
-   The duration of a configuration change depends on various factors such as network conditions, task queues, and data volume. We recommend that you change configurations during off-peak hours and make sure that your applications have automatic reconnection mechanisms.
-   To ensures better performance and stability of the instance, the system will upgrade the minor version to the latest version by default If the minor version of your instance expires or is not included in the maintenance list and the instance is [upgraded](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md), [migrated](/intl.en-US/User Guide/Data migration and synchronization/Overview.md), [changed](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md), [Created from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Created by point-in-time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), or performed [Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md).

## Add a node

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  On the **Basic Information** page, click the corresponding button to add a node.

    ![Add a node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3735298951/p37266.png)

    To add a Mongos node, perform the following steps:

    1.  In the **Mongos List** section, click **Add Mongos**.

    2.  On the Add Mongos page, specify **Specifications** of the Mongos node.

    To add a shard node, perform the following steps:

    1.  In the **Shard List** section, click **Add Shard**.

    2.  On the Add Shard page, specify **Specifications** and **Storage** of the shard node.

6.  Select **ApsaraDB for MongoDB Terms of Service** and make the payment as prompted.


## Change the configuration of an existing node

For more information about instance specifications, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  On the **Basic Information** page, change the configuration of the corresponding node.

    To change the configuration of a Mongos node, perform the following steps:

    1.  In the **Mongos List** section, find the Mongos node and choose **![More icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Change Configuration**.

        ![Change the configuration of a Mongos node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3735298951/p21057.png)

    2.  On the Change Mongos Configuration page, specify **Specifications** of the Mongos node.

    To change the configuration of a shard node, perform the following steps:

    1.  In the **Shard List** section, choose **![More icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Change Configuration**.

        ![Change the configuration of a shard node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4735298951/p21056.png)

    2.  On the Change Shard Configuration page, specify **Specifications** and **Storage** of the shard node.

        **Note:** If the billing method of the instance is subscription, you cannot downgrade the storage space of the shard node. You can use other methods to reduce the storage space. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

6.  Select **ApsaraDB for MongoDB Terms of Service** and make the payment as prompted.


When the instance status changes to **Running**, the configuration has been changed.

