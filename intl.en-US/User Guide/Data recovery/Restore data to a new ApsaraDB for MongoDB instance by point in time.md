# Restore data to a new ApsaraDB for MongoDB instance by point in time

This topic describes how to restore data to a new ApsaraDB for MongoDB instance by point in time. This method is ideal for data restoration and verification.

-   The source instance is a replica set or sharded cluster instance.
-   You can select a point in time only from the last seven days.

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

7.  In the **Create Instance By Time Point** panel, select a time point for restoration and select one of the following options:

    -   **All Databases**: restores data of all databases in the source instance to the destination instance.
    -   **Select Databases**: restores data of some databases in the source instance to the destination instance.

        You can select the databases that you want to restore or click **Enter Databases** to enter the names of the databases.

        **Note:**

        -   If you enter the names of the databases, separate the database names with commas \(,\).
        -   To ensure data integrity and accuracy, do not select the latest point in time \(usually the latest hour\) if the instance is a sharded cluster instance. Otherwise, restoration fails.
        -   After the database version is upgraded, the backup files of the original version cannot be used to restore data of the new version.
8.  Click **OK**.

9.  On the instance buy page, select a billing method for the new instance.

    **Note:**

    -   Subscription: You must pay for the subscription when you create an instance. This method is more cost-effective than the pay-as-you-go method. We recommend that you select this method for long-term use. A longer subscription period enables a larger discount.
    -   Pay-as-you-go: You are billed on an hourly basis based on the used resources. We recommend that you select this billing method for short-term use. You can reduce costs by releasing your pay-as-you-go instance after you no longer need it.
10. Configure the new instance. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md) or [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md).

    **Note:**

    -   Replica set instance: The storage capacity of the new instance must be larger than or equal to that of the source instance.
    -   Sharded cluster instance:
        -   The number of shard nodes in the new instance must be larger than or equal to that in the source instance.
        -   The storage capacity of each shard node in the new instance must be larger than or equal to those in the source instance.
11. Click **Buy Now**.

12. Read and select **ApsaraDB for MongoDB Agreement of Service** and complete the payment.

    **Note:** The time required to restore data to a new instance by backup set varies based on factors such as the data volume, task queue status, and network conditions. When the status of the new instance changes to **Running**, the restoration is complete.


