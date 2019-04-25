# Switch the network type of an instance {#concept_f3s_fys_2fb .concept}

ApsaraDB for MongoDB allows you to create an instance whose network type is classic network or VPC. You can log on to the ApsaraDB for MongoDB console or call the ModifyDBInstanceNetworkType operation to switch between the two network types.

## Network types {#section_fn2_3yt_lgb .section}

-   On a classic network, instances are not isolated. You can configure a whitelist policy for them to block unauthorized access.
-   A VPC is an isolated network environment that is securer and recommended.

    You can customize the routing table, IP address range, and gateway in the VPC. In addition, you can use a physical connection or VPN to combine your user-created IDC with cloud resources in Alibaba Cloud VPC to create a virtual IDC, so that you can smoothly migrate your applications to the cloud.


## Notes {#section_nnp_1ws_2fb .section}

You can switch the network type for replica set and sharded cluster instances, but not for standalone instances.

During the switchover, the target instance may be disconnected transiently once. We recommend that you switch the network type during off-peak hours or ensure that your applications can automatically re-establish a connection to avoid an impact of intermittent disconnection.

## Switch from a classic network to a VPC {#section_tp1_1sl_2fb .section}

You can choose to keep the intranet addresses on the classic network to smoothly switch the network type without intermittent disconnection. For more information, see [Configure a hybrid access solution to smoothly switch from a classic network to a VPC](intl.en-US/User Guide/Network connection management/Configure a hybrid access solution to smoothly switch from a classic network to a VPC.md#).

1.  Create a VPC in the same region as the target ApsaraDB for MongoDB instance. For more information, see [Create a VPC](https://www.alibabacloud.com/help/doc-detail/27710.htm).
2.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
3.  In the upper-left corner of the home page, select the region where the target instance is located.
4.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
5.  Locate the target instance and click its instance ID.
6.  In the left-side navigation pane, click **Database Connection**.
7.  In the Intranet Connection - Classic area, click **Switch to VPC**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6717/155617279737277_en-US.png)

8.  In the VPC dialog box that appears, specify **VPC** and **VSwitch**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6717/155617279737278_en-US.png)

    **Note:** 

    -   You can enable **Retain the connection address of the classic network** to generate new intranet addresses in the VPC and keep the existing intranet addresses on the classic network within a specified period. When the period expires, the intranet addresses on the classic network are automatically released.
    -   If you do not enable **Retain the connection address of the classic network**, the target ApsaraDB for MongoDB instance may be disconnected transiently once when its network type is switched to VPC. Cloud products, such as ECS, on the classic network cannot be connected to this instance. We recommend that you switch the network type during off-peak hours or ensure that your applications can automatically re-establish a connection to avoid an impact of intermittent disconnection.
9.  Click **OK**.

## Switch from a VPC to a classic network {#section_wjx_2yl_2fb .section}

After the network type of an ApsaraDB for MongoDB instance is switched to classic network, intranet addresses in the VPC are released and ECS instances in the VPC cannot access this instance through the intranet. ApsaraDB for MongoDB generates intranet addresses on the classic network and remains public addresses unchanged. You need to modify the connection information in your applications.

**Note:** After the network type of an ApsaraDB for MongoDB instance is switched to classic network, ECS instances in the VPC cannot be connected to this instance. During the switchover, the target instance may be disconnected transiently once. We recommend that you switch the network type during off-peak hours or ensure that your applications can automatically re-establish a connection to avoid an impact of intermittent disconnection.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Database Connection**.
6.  In the Intranet Connection - VPC area, click **Switch to Classic Network**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6717/155617279737286_en-US.png)
7.  In the Switch to Classic Network dialog box that appears, click **OK**.

