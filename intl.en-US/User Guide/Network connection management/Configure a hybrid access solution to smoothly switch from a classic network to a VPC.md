# Configure a hybrid access solution to smoothly switch from a classic network to a VPC {#concept_ysg_ngz_lgb .concept}

To meet the increasing network switchover requirements, ApsaraDB for MongoDB provides a hybrid network access feature to help you smoothly switch from a classic network to a VPC without intermittent disconnection or network disconnection.

## Prerequisites {#section_kvs_c3z_lgb .section}

The target instance must be a replica set or sharded cluster instance.

## Constraints {#section_zlb_rgz_lgb .section}

In hybrid access mode, you cannot switch the network type to classic network.

## Solution {#section_kmf_qgz_lgb .section}

When you switch the network type of an ApsaraDB for MongoDB instance from classic network to VPC, ApsaraDB for MongoDB immediately releases the intranet addresses on the classic network. In this case, the instance is disconnected for 30s once and cloud products \(such as [ECS](https://www.alibabacloud.com/help/doc-detail/25367.htm)\) on the classic network cannot be connected to this instance.

Using the hybrid access solution, you can connect ECS instances on the classic network and in the VPC to the ApsaraDB for MongoDB instance at the same time to smoothly switch its network type. When you switch its network type from classic network to VPC, you can enable ApsaraDB for MongoDB to generate new intranet addresses in the VPC and keep the existing intranet addresses on the classic network within a specified period, a maximum of which is 120 days. Within the specified period, this ApsaraDB for MongoDB instance can be accessed by ECS instances on the classic network and in the VPC.

In hybrid access mode, you can gradually switch the network type or migrate ECS and other cloud products from the classic network to the VPC until all products can be interconnected through the securer VPC on the intranet.

## Procedure {#section_u3z_rgz_lgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Database Connection**.
6.  In the Intranet Connection - Classic area, click **Switch to VPC**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6717/155617371637277_en-US.png)

7.  In the VPC dialog box that appears, set related parameters.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6718/155617371637314_en-US.png)

    1.  Specify **VPC** and **VSwitch**.

        **Note:** For more information about how to create a VPC or VSwitch, see [Create a VPC and VSwitch](https://www.alibabacloud.com/help/doc-detail/65398.htm).

    2.  Turn on the **Retain the connection address of the classic network** switch.
    3.  Select a period for **Expiration Time \(Days\)**.
8.  Click **OK**.

