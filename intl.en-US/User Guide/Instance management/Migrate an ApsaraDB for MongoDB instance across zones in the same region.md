# Migrate an ApsaraDB for MongoDB instance across zones in the same region

This topic describes how to migrate an ApsaraDB for MongoDB instance across zones in the same region. After the instance is migrated, its attributes, specifications, and connection addresses remain unchanged.

## Prerequisites

-   A replica set or sharded cluster instance is created.
-   The destination and source zones are in the same region.
-   If the instance is in a VPC, make sure that a vSwitch is created in the destination zone before you start migration. For more information about how to create a vSwitch, see [Create a VSwitch](https://www.alibabacloud.com/help/zh/doc-detail/65387.htm).
-   The instance does not have a public endpoint. If you have applied for a public endpoint, you must release it before migration. For more information, see [Release a public connection string](/intl.en-US/User Guide/Network connection management/Public IP Connection/Release a public connection string.md).

## Precautions

-   If the instance is in a VPC, you cannot change the VPC when the instance is in the migration process.
-   The time required varies based on factors such as the network conditions, task queue status, and data volume. We recommend that you migrate the instance across zones during off-peak hours.
-   During the migration, a transient connection of 30 seconds occurs. Make sure that your application is configured to reconnect to the instance after it is disconnected.
-   The virtual IP addresses \(VIPs\) of the instance, such as 172.16.88.60, are changed when the instance is migrated across zones. If your application uses the original VIP, the application cannot connect to the instance after the migration.

    **Note:** We recommend that you use a connection string URI to connect to the instance, which ensures high availability. For more information, see [Overview of replica set instance connections]() or [Overview of sharded cluster instance connections]().


## Supported migration types and scenarios

|Migration type|Scenario|
|:-------------|:-------|
|Migrate an ApsaraDB for MongoDB instance from one zone to another|The ApsaraDB for MongoDB instance is migrated to the zone where an ECS instance resides. Then, the ECS instance can connect to the ApsaraDB for MongoDB instance over an internal network with lower network latency.|
|Migrate an ApsaraDB for MongoDB instance from one zone to multiple zones|The ApsaraDB for MongoDB instance provides disaster recovery across data centers. The three nodes of a replica set instance are deployed to three different zones in the same region. This enables the instance to tolerate disasters at higher levels. For example, a replica set instance in a single zone can tolerate only server- and rack-level faults, whereas a replica set instance in multiple zones can tolerate server-, rack-, and data center-level faults.

**Note:** For more information about the node deployment policy of a replica set instance or a sharded cluster instance in multiple zones, see [Node deployment policies](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone replica set instance.md) or [Figure 1](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone sharded cluster instance.md). |
|Migrate an ApsaraDB for MongoDB instance from multiple zones to one zone|Special user requirements are met.|

## Migrate a replica set instance across zones in the same region

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the **Basic Information** section, click **Change Zone**.

    ![Click Change Zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2835298951/p44911.png)

6.  In the Migrate Instance to Other Zone panel, configure parameters based on the network type of the instance.

    -   If the instance is in a VPC or is in hybrid network access mode, perform the following operations:
        1.  Select the destination zone and vSwitch.

            ![Migrate an ApsaraDB for MongoDB instance in a VPC across zones](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2835298951/p94218.png)

        2.  Specify Migration Time and select the check box of the warning message.
    -   If the instance is in the classic network, perform the following operations:
        1.  Select the destination zone.

            ![Migrate an ApsaraDB for MongoDB instance in the classic network across zones](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2835298951/p94219.png)

        2.  Specify Migration Time and select the check box of the warning message.
    **Note:**

    -   **Migrate Now**: The migration immediately starts. When the instance status changes to **Running**, the migration is complete.
    -   **Migrate at Scheduled Time**: The migration starts during the specified period. You can click **Edit** to change the period.

        After you select this option, the system prepares for the migration task, changes the instance status to **Migrating**, and then starts the task in the specified period.

7.  Click **Submit**.


## Migrate a sharded cluster instance across zones in the same region

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the **Basic Information** section, click **Change Zone**.

    ![Click Change Zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2835298951/p44911.png)

6.  In the Migrate Instance to Other Zone panel, configure parameters based on the network type of the instance.

    -   If the instance is in a VPC or is in hybrid network access mode, perform the following operations:
        1.  Select the destination zone and vSwitch.

            ![Migrate an ApsaraDB for MongoDB instance in a VPC across zones](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2835298951/p94220.png)

        2.  Specify Migration Time and select the check box of the warning message.
    -   If the instance is in the classic network, perform the following operations:
        1.  Select the destination zone.

            ![Migrate an ApsaraDB for MongoDB instance in the classic network across zones](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2835298951/p94221.png)

        2.  Specify Migration Time and select the check box of the warning message.
    **Note:**

    -   **Migrate Now**: The migration immediately starts. When the instance status changes to **Running**, the migration is complete.
    -   **Migrate at Scheduled Time**: The migration starts during the specified period. You can click **Edit** to change the period.

        After you select this option, the system prepares for the migration task, changes the instance status to **Migrating**, and then starts the task in the specified period.

7.  Click **Submit**.


