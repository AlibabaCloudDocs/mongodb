# Apply for a public IP address {#concept_p2z_ycq_kgb .concept}

ApsaraDB for MongoDB allows you to apply for a public IP address to connect to an instance over the Internet. You can use the console to apply for a public IP address. Allowing access through a public IP address may incur security risks to the associated instance. To ensure data security, you must [release public IP addresses](../../../../intl.en-US/User Guide/Network connection management/Release a public address.md#) in a timely manner when they are not needed.

## Address types {#section_v4t_pl1_mfb .section}

You can connect to ApsaraDB for MongoDB internally through a VPC or classic network, or externally over the Internet.

|Address type|Description|
|:-----------|:----------|
|Internal IP address – VPC| -   Virtual Private Cloud \(VPC\) is an isolated network environment with higher security and performance than the classic network. VPCs must be created in advance. For more information, see [Configure VPC for a new instance](../../../../intl.en-US/User Guide/Network connection management/Configure a VPC for a new instance.md#).
-   If your applications are deployed in an ECS instance, and the ECS instance is in the same region and has the same network type as the MongoDB instance, the two instances can access to each other through the internal network.
-   Accessing an instance through the VPC is more secure and offers better performance.

 |
|Internal IP address – classic|Cloud services in a classic network are not isolated. Unauthorized access to cloud services is blocked only by the security group or whitelist policy. For more information about modifying the network type to VPC, see [Modify the instance network type](../../../../intl.en-US/User Guide/Network connection management/Switch the network type of an instance.md#).|
|Public IP address| -   You must apply for and release public IP addresses manually.
-   If you cannot access a MongoDB instance through the internal network, you must apply for a public IP address. Some scenarios include:
    -   You want to access a MongoDB instance from an ECS instance, but they are in different regions or have different network types.
    -   You want to access a MongoDB instance from a device that is not a public offering on Alibaba Cloud.

 **Note:** Access to a MongoDB instance through a public IP address may incur security risks. We recommend that you migrate your applications to an ECS instance that is in the same region and has the same network type as the MongoDB instance. Then you can use the VPC internal network.

 |

## Procedure {#section_nmm_bdq_kgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the homepage, select the region of the instance.
3.  In the left-side navigation pane, click **Sharding instances**.
4.  Locate the target instance, and then click the instance ID.
5.  On the Basic Information page that appears, click **Database Connection** in the left-side navigation pane.
6.  On the Database Connection page that appears, click **Apply for Public Connection String** on the right of Public IP Connection.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23846/155920736537037_en-US.png)

7.  In the Apply for Public Connection String dialog box that appears, select **Mongos** and click **OK**.

    **Note:** 

    You can repeat this step to apply for public IP addresses for multiple mongos based on your business needs. You can only apply for another public IP address after the current requested public IP address has been created.

    After you obtain the public IP address, you must add it to the whitelist before you can use this address to access the instance. For more information, see [Configure a whitelist](intl.en-US/Quick Start for Cluster/Configure a whitelist.md#).

8.  When the application is completed, the public IP address and its associated connection string URI are added to the mongos in the instance details page. For more information, see [Connect to a MongoDB sharded cluster instance](intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance.md#).

