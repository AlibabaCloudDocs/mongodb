# Restore data to the current ApsaraDB for MongoDB instance

This topic describes how to restore data to the current ApsaraDB for MongoDB instance. This helps minimize the data loss caused by incorrect operations.

## Prerequisite

The instance is a replica set instance with three nodes.

## Background information

-   The time required to restore data to your current instance varies depending on factors such as the data volume, task queue status, and network conditions. When the status of the instance changes to **Running**, the restoration is complete.
-   If you restore data to your current instance, all existing data is overwritten and cannot be restored.

    **Warning:** This operation is risky. We recommend that you restore data to a new ApsaraDB for MongoDB instance by point in time or backup set. Then, verify the data, and migrate the data back to the source instance by using Data Transmission Service \(DTS\). For more information, see [Restore data to a new ApsaraDB for MongoDB instance by point in time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md) or [Create an instance from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md).


## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Backup and Recovery**.

6.  On the **Backup and Recovery** page, find the backup set and choose **![More icon](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Data Rollback** in the Actions column.

    **Note:** If you have upgraded the database version, you cannot use the backup files of the earlier database version to restore data.

7.  In the **Roll Back Instance** message, click **OK**.

    **Note:** The instance status becomes **Restoring from Backup** after you click **OK**. You can click **Refresh** in the upper-right corner of the **Backup and Recovery** page to update the instance status. The restoration is complete when the instance status changes to **Running**.


