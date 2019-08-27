# Migrate instances across zones {#concept_uh2_skz_lhb .concept}

You can migrate instances to other zones within the same region. After the instances are migrated to other zones, the attributes, specifications, and connection addresses of the instances remain unchanged.

## Prerequisites {#section_ufy_pmz_lhb .section}

-   The instance is a replica set instance.
-   The destination zone and the current zone where the instance is located must be in the same region.
-   Before you migrate instances in VPCs, ensure that the destination zone has corresponding VSwitches created. For more information about VSwitch creation, see [Create a VSwitch](https://www.alibabacloud.com/help/zh/doc-detail/65387.htm).
-   Before you migrate instances with a public connection address, release the public connection address. For more information, see [Release a public address](intl.en-US/User Guide/Network connection management/Release a public address.md#).

## Precautions {#section_n2v_zkz_lhb .section}

-   The VPC of instances whose network type is VPC cannot be changed when you migrate the instances to other zones.
-   The period for migration is related to several factors such as the network, task queue, and the amount of data to be migrated. We recommend that you modify configurations during off-peak hours.
-   Services may be disconnected for 30 seconds during migration across zones. Ensure that your application is configured to reconnect to the database after the application is disconnected.
-   Migration across zones causes the changes to virtual IP addresses \(VIPs\), such as 172.16.88.60. If the application is connected to the VIP of the database, the connection with the database is disconnected. We recommend that you use the following URI: mongodb://root:\*\*\*\*@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717/admin? replicaSet=mgset-132xxx. This guarantees the high availability of connections. For more information, see [Connect to an replica set instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to an replica set instance through the mongo shell.md#).

## Supported migration types and scenarios {#section_gcn_mmz_lhb .section}

|Supported migration type|Scenario|
|:-----------------------|:-------|
|Migrate instances from one zone to another zone|Migrate ApsaraDB for MongoDB instances to the zone to which the ECS instances belong. In the same zone, the ECS instances connect to the ApsaraDB for MongoDB instances through the intranet, which minimizes network latency.|
|Migrate instances from one zone to multiple zones|Improve the disaster recovery capability of instances to achieve disaster recovery across data centers. Deploy the three nodes of a replica set instance to three zones within the same region. This method helps the instances tolerate disasters at higher levels. For example, instances in a single zone can tolerate server- and rack-related faults, whereas instances in multiple zones can tolerate data center-related faults.

**Note:** For information about the node deployment strategy of replica set instances in multiple zones, see [Node deployment policies of a replica set instance](intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone replica set instance.md#section_wjr_qpj_wgb).

 |
|Migrate instances from multiple zones to a single zone|Meet the needs of specific functions.|

## Procedure {#section_d1s_4pz_lhb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#mongodb/list).
2.  In the upper-left corner of the page, select the region of the instance.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the instance and click the instance ID.
5.  On the Basic Information page, locate the Basic Information section, and click **Change Zone**.

    ![Click Change Zone](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/160284/156324429744911_en-US.png)

6.  In the Migrate Instance to Other Zone dialog box that appears, configure parameters based on the network type of the instance.

    -   When the network type of the instance is VPC or is a hybrid network of VPC and classic network:

        1.  Select the destination zone for migration.
        2.  Select the VSwitch of the destination zone.
        3.  Set the time to migrate the instance.
        ![Migrate instances in a VPC to another zone](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/160284/156324429844913_en-US.png)

    -   When the network type of the instance is classic network:

        1.  Select the destination zone for migration.
        2.  Set the time to migrate the instance.
        ![Migrate instances in a classic network to another zone](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/160284/156324429844912_en-US.png)

    **Note:** 

    -   **Migrate Now**: The instance is immediately migrated to another zone. The instance is migrated if the instance is in the **Running** state.
    -   **Migrate at Scheduled Time**: Select the period during which the instance can be migrated to another zone. You can click **Edit** to change the maintenance period.

        The premigration task is performed for the instance and the instance status is changed to **Changing Configuration**. Perform the migration task within the specified period.

7.  Click **OK**.

