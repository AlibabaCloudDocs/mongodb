# Configure a whitelist for an ApsaraDB for MongoDB instance

This topic describes how to configure a whitelist for an ApsaraDB for MongoDB instance. After you create an ApsaraDB for MongoDB instance, you must configure an IP whitelist or add an ECS security group to allow access from authorized devices only. The default IP whitelist contains only the IP address 127.0.0.1, which indicates that no devices can access the ApsaraDB for MongoDB instance.

When you add an ECS security group, make sure that the ApsaraDB for MongoDB instance has the same network type as the ECS instances in the ECS security group. If both the ApsaraDB for MongoDB instance and ECS instances have the VPC network type, make sure that they reside in the same VPC.

-   Before the first time you use an ApsaraDB for MongoDB instance, you must configure a whitelist for it. After you configure the whitelist, the connection addresses of the instance appear on the **Basic Information** and **Database Connection** pages.
-   Whitelists make your ApsaraDB for MongoDB instance more secure. We recommend that you maintain the whitelists on a regular basis.

## Configure an IP whitelist

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, **Sharded Cluster Instances**, or **Serverless Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Settings**.

6.  Configure an IP whitelist.

    To manually modify an IP whitelist, follow these steps:

    1.  Find the target IP whitelist, and choose ![more](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9545298951/p13851.png) \> **Manually Modify** in the **Actions** column.

        ![Manually modify an IP whitelist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5145298951/p70091.png)

    2.  Enter IP addresses or Classless Inter-Domain Routing \(CIDR\) blocks.

        **Note:**

        -   Separate multiple IP addresses with commas \(,\). You can add a maximum of 1,000 different IP addresses to an IP whitelist. Supported formats are IP addresses such as 0.0.0.0/0 and 10.23.12.24, or [CIDR blocks](~~54484~~) such as 10.23.12.24/24. /24 indicates the length of the IP address prefix. An IP address prefix can contain 1 to 32 bits.
        -   If the IP whitelist is empty or only contains 0.0.0.0/0, all devices are granted access. This is risky for your ApsaraDB for MongoDB instance. We recommend that you only add the IP addresses or CIDR blocks of your own web servers to the IP whitelist.
    3.  Click **OK**.

    To load the private IP addresses of ECS instances to an IP whitelist, follow these steps:

    1.  Find the target IP whitelist, and choose ![more](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9545298951/p13851.png) \> **Import ECS Intranet IP** in the **Actions** column.

        ![Load the private IP addresses of ECS instances](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5145298951/p70092.png)

    2.  From the displayed private IP addresses of ECS instances created by the current account, select the target IP and add them to the IP whitelist.

        ![Select the private IP addresses of ECS instances](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5145298951/p37240.png)

    3.  Click **OK**.

        **Note:** For easy O&M and access control, we recommend that you add an ECS security group. For more information, see [Add an ECS security group](#section_fwu_oit_4dc).


## Add an ECS security group

An ECS security group relieves you from the tedious work of adding IP addresses or CIDR blocks. It makes database O&M easier.

**Note:** After you add an ECS security group, all its ECS instances can access the ApsaraDB for MongoDB instance either over an internal network or over the Internet. For access over an internal network, the two types of instances must have the same network type. If the network type is VPC, they must be in the same VPC. For access over the Internet, you must have applied for a public endpoint for the ApsaraDB for MongoDB instance.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, **Sharded Cluster Instances**, or **Serverless Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Settings**.

6.  Click **Add Security Group**.

7.  In the dialog box that appears, select the target ECS security group.

    ![Add a security group](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5145298951/p70088.png)

    **Note:**

    -   Each ApsaraDB for MongoDB instance can be added in up to 10 security group. After you add an ECS security group, all its ECS instances can access the ApsaraDB for MongoDB instance either over an internal network or over the Internet. For access over an internal network, the two types of instances must have the same network type. If the network type is VPC, the two types of instances must be in the same VPC. For access over the Internet, you must have applied for a public endpoint for the ApsaraDB for MongoDB instance.
    -   If you move your pointer over an ECS security group, you can view its name and description. If you move your pointer over **VPC**, you can view the VPC ID. This way, you can quickly find the target ECS security group.

## Delete an IP whitelist or an ECS security group

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, **Sharded Cluster Instances**, or **Serverless Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Settings**.

6.  Delete an IP whitelist or an ECS security group.

    To delete an IP whitelist, follow these steps:

    1.  Find the target IP whitelist, and choose **![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Delete Whitelist Group** in the **Actions** column.

        ![Delete an IP whitelist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5145298951/p67412.png)

        **Note:** You cannot delete the default IP whitelist.

    2.  In the message that appears, click **OK**.

    To delete an ECS security group, follow these steps:

    1.  Click **Clear**.

        ![Clear an ECS security group](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6145298951/p70152.png)

    2.  In the message that appears, click **OK**.


## Common connection scenarios

-   [Connect a local client to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account.md)

