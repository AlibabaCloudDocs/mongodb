# Restore data to a new ApsaraDB for MongoDB instance by point in time

This topic describes how to restore data to a new ApsaraDB for MongoDB instance by point in time. This method is ideal for data restoration and verification.

-   The source instance is a replica set or sharded cluster instance.
-   You can only select a point in time from the last seven days.

## Precaution

To ensures better performance and stability of the instance, the system will upgrade the minor version to the latest version by default If the minor version of your instance expires or is not included in the maintenance list and the instance is [upgraded](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md), [migrated](/intl.en-US/User Guide/Data migration and synchronization/Overview.md), [changed](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md), [Created from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Created by point-in-time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), or performed [Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md).

## Billing

This method creates an instance and you are charged for the new instance. For more information, see [Billing items and pricing](/intl.en-US/Purchase Guide/Billing items and pricing.md).

**Note:** If you want to restore data to a pay-as-you-go instance, make sure that your account has sufficient balance.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Backup and Recovery**.

6.  On the **Backup and Recovery** page, click **Create Instance By Time Point**.

7.  In the **Create Instance By Time Point** dialog box that appears, configure the following parameters.

    -   **All Databases**: If you select this option, all databases in the source instance are restored.
    -   **Select Databases**: If you select this option, only selected databases are restored.

        You can directly select the databases you want to restore, or click **Enter Databases** to enter the names of the databases.

        **Note:**

        -   If you want to restore more than one database, separate the database names with commas \(,\) when you enter them.
        -   To ensure data integrity and accuracy, do not select the latest point in time \(usually the latest hour\) if the instance is a sharded cluster instance. Otherwise, restoration fails.
        -   After the database version is upgraded, the backup files of the original version cannot be used to restore data of the new version.
8.  Click **OK**.

9.  On the Instance Purchase page that appears, select a billing method for the new instance.

    **Note:**

    -   Subscription: You must pay for the subscription when you create an instance. We recommend that you select this billing method for long-term use, because it is more cost-effective than pay-as-you-go billing. Longer subscription periods have larger discounts.
    -   Pay-as-you-go: A pay-as-you-go instance is billed at an hourly rate based on your actual resource usage. We recommend that you select this billing method for short-term use. You can reduce costs by releasing your pay-as-you-go instance after you no longer need it.
10. Configure the new instance. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md) or [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md).

    **Note:**

    -   Replica set instance: The storage capacity of the new instance must be greater than or equal to that of the source instance.
    -   Sharded cluster instance:
        -   The number of shards in the new instance must be greater than or equal to that in the source instance.
        -   The storage capacity of each shard in the new instance must be greater than or equal to those in the source instance.
11. Click **Buy Now**.

12. Read and select **ApsaraDB for MongoDB Agreement of Service**, and complete the payment as prompted.

    **Note:** The time required to restore data to a new instance by backup set varies depending on factors such as the data volume, task queue status, and network conditions. When the status of the new instance changes to **Running**, the restoration is complete.


