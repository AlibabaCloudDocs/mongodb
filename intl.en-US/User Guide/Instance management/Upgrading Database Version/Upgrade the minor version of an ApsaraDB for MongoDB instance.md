# Upgrade the minor version of an ApsaraDB for MongoDB instance

This topic describes how to upgrade the minor version of an ApsaraDB for MongoDB instance to the latest in the ApsaraDB for MongoDB console.

-   The instance is a replica set or sharded cluster instance.
-   The instance is not running the latest minor version. When you use the latest minor version, the ApsaraDB for MongoDB console does not display the **Upgrade Minor Version** button for the instance.

## Precautions

-   You cannot downgrade an instance after you upgrade it.
-   When an instance undergoes a minor version upgrade, it is restarted and has a brief disconnection of less than 30 seconds. We recommend that you perform the upgrade during off-peak hours or make sure that your application is configured to reconnect to the instance after it is disconnected.
-   To ensures better performance and stability of the instance, the system will upgrade the minor version to the latest version by default If the minor version of your instance expires or is not included in the maintenance list and the instance is [upgraded](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md), [migrated](/intl.en-US/User Guide/Data migration and synchronization/Overview.md), [changed](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md), [Created from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Created by point-in-time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), or performed [Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md).

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the region where the target instance resides.

3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances**.

4.  Find the target instance and click its ID.

5.  On the Basic Information page, click **Upgrade Minor Version**.

    ![Click Upgrade Minor Version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4735298951/p58729.png)

    **Note:** When you use the latest minor version, the console does not display the **Upgrade Minor Version** button for the instance.

6.  In the Upgrade Minor Version message that appears, view the version release log and determine whether to upgrade the instance.

    ![View the version release log](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5735298951/p58731.png)

    **Note:** If you want to upgrade the instance, click **Submit**. Otherwise, click **Close**.

7.  Wait until the instance status changes from **Upgrading** to **Running**.


