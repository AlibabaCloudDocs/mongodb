# Modify the expiration time for the classic network {#task_eqg_gy1_ffb .task}

In hybrid network access mode, you can modify the expiration time for the classic network.

When you switch the network type of an instance from classic network to VPC, you can choose to keep the intranet addresses on the classic network within a specified period. When generating new intranet addresses in the VPC, ApsaraDB for MongoDB can keep the existing intranet addresses on the classic network within the specified period. In this case, you can use the hybrid network access solution to smoothly switch from the classic network to the VPC without intermittent disconnection. When the period expires, the intranet addresses on the classic network are automatically released.

ApsaraDB for MongoDB allows you to modify the expiration time for the classic network within the previously specified period to shorten or prolong the period for keeping the intranet addresses on the classic network.

1.   Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list). 
2.  In the upper-left corner of the home page, select the region where the target instance is located. 
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance. 
4.  Locate the target instance and click its instance ID. 
5.  In the left-side navigation pane, click **Database Connection**. 
6.  In the Retained Classic Network Address area, click **Change Expiration Time**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21697/155617448312541_en-US.png)

7.  In the Change Expiration Time dialog box that appears, select a period for **Expiration Time \(Days\)**. 

    **Note:** You can set the expiration time to 14 days, 30 days, 60 days, or 120 days for the classic network.

8.  Click **OK**. 

