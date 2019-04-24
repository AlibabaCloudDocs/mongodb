# Apply for a public address {#concept_hfy_gj1_mfb .concept}

ApsaraDB for MongoDB allows you to apply for a public address to connect to an instance through the Internet.

## Connection types {#section_v4t_pl1_mfb .section}

ApsaraDB for MongoDB supports two network types for connecting to an instance: Intranet Connection - VPC and Public IP Connection.

|Connection type|Description|
|:--------------|:----------|
|Intranet Connection - VPC| -   ApsaraDB for MongoDB supports Intranet Connection - VPC by default.
-   If your applications are deployed on an ECS instance that is in the same region and configured with the same network type as your ApsaraDB for MongoDB instance to be connected, the two instances can be interconnected through an intranet. You do not need to apply for a public address.
-   The connection type of Intranet Connection - VPC can provide you with enhanced security and optimal performance.

 |
|Public IP Connection| -   You need to apply for and release a public address.
-   In the following scenarios where your ApsaraDB for MongoDB instance cannot be connected through an intranet, you need to apply for a public address:

    -   You use an ECS instance to access an ApsaraDB for MongoDB instance, but the two instances are in different regions or configured with different network types.
    -   You use a non-Alibaba Cloud device to access an ApsaraDB for MongoDB instance.
**Note:** Considering certain security risks for using a public address, we recommend that you migrate your applications to an ECS instance that is in the same region and configured with the same network type as your ApsaraDB for MongoDB instance and select Intranet Connection - VPC.


 |

## Apply for a public address {#section_gsy_tl1_mfb .section}

There are certain security risks for connecting to an instance through the Internet. To guarantee data security, you need to [release a public address](../../../../intl.en-US/User Guide/Network connection management/Release a public address.md#) in a timely manner after using it.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  Click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155608720613206_en-US.png)** \> **Manage** in the Operation column corresponding to the target instance.
4.  On the Basic Information page that appears, click **Database Connection** in the left-side navigation pane.
5.  On the Database Connection page that appears, click **Apply for Public IP** to the right of Public IP Connection.
6.  In the Apply for Public IP dialog box that appears, click **OK**.

    **Note:** After the application procedure, you can use the obtained public address to access the target instance. Before that, you need to add the public IP address of the terminal that you use to connect to the instance to the whitelist. For more information, see [Configure a whitelist](intl.en-US/Quick Start for Standalone/Configure a whitelist.md).


