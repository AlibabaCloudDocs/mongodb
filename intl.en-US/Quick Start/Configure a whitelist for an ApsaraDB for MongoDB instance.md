# Configure a whitelist for an ApsaraDB for MongoDB instance

This topic describes how to configure an IP address whitelist for an ApsaraDB for MongoDB instance. After you create an ApsaraDB for MongoDB instance, you must configure an IP address whitelist to allow access only from authorized devices. The default whitelist contains only the IP address 127.0.0.1, which indicates that no devices can access the ApsaraDB for MongoDB instance.

-   Before you use an ApsaraDB for MongoDB instance for the first time, you must configure a whitelist for the instance. After you configure the whitelist, the endpoints of the instance appear on the **Basic Information** and **Database Connection** pages.
-   Whitelists make your ApsaraDB for MongoDB instances more secure. We recommend that you maintain the whitelists on a regular basis.

## Configure an IP address whitelist for a standalone instance, replica set instance, or sharded cluster instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Settings**.

6.  Find the IP address whitelist that you want to configure, and choose ![More icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7023797951/p13206.png) \> **Manually Modify** or **Import ECS Intranet IP** in the **Actions** column.

    **Manually Modify**

    1.  In the **Manually Modify** panel, click the **IPv4** or **IPv6** tab based on your network connection.

        **Note:**

        -   Limits for **IPv4** addresses:
            -   Separate multiple IP addresses with commas \(,\). A maximum of 1,000 different IP addresses can be added.

                A whitelist can include IP addresses such as `0.0.0.0/0` and `10.23.12.24`, or [CIDR blocks](~~54484~~) such as `10.23.12.24/24`. `/24` indicates that the prefix of the CIDR block is 24-bit long. You can replace 24 with a value within the range of 1 to 32.

            -   If the whitelist is empty or contains `0.0.0.0/0`, all IP addresses can access the ApsaraDB for MongoDB instance. This may introduce security risks to the instance. Proceed with caution.
        -   Limits for **IPv6** addresses:
            -   Separate multiple IP addresses with commas \(,\). A maximum of 1,000 different IP addresses can be added.

                Supported formats include `::` and `0:0:0:0:0:0:0:1`. Only IP addresses are supported. [CIDR blocks](~~54484~~) will be supported later.

            -   If the whitelist is empty or contains only `::`, all IP addresses can access the ApsaraDB for MongoDB instance. This may introduce security risks to the instance. Proceed with caution.
            -   You can specify **IPv6** address whitelists only if the instance resides in Zone G of the China \(Hangzhou\) region.
            -   You can specify **IPv6** address whitelists only if the version of the database engine is 4.2.
        -   You cannot specify both **IPv4** and **IPv6** addresses in a single whitelist. If you want to specify both IPv4 and IPv6 addresses, specify them in separate whitelists.
    2.  Click **OK**.

    **Import ECS Intranet IP**

    1.  Click **Import ECS Intranet IP**. In the Import ECS Intranet IP panel, the internal IP addresses of ECS instances created in the current account are displayed. Select one or more IP addresses and add them to the IP address whitelist.

        ![Add internal IP addresses of ECS instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8023797951/p13209.png)

    2.  Click **OK**.

        **Note:** For easy O&M and access control, we recommend that you add an ECS security group. For more information, see [Configure an ECS security group for a standalone instance, replica set instance, or sharded cluster instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).


## Configure an ECS security group for a standalone instance, replica set instance, or sharded cluster instance

An ECS security group relieves you from the tedious work of adding IP addresses or CIDR blocks. It makes database O&M easier.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  Click **Add Security Group**.

6.  In the Add Security Group panel, select one or more ECS security groups that you want to add.

    ![Add one or more ECS security groups](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4027562061/p70088.png)

    **Note:**

    -   Each ApsaraDB for MongoDB instance can be added to up to 10 security groups. After you add an ECS security group, all its ECS instances can access the ApsaraDB for MongoDB instance either over an internal network or over the Internet. For access over an internal network, the two types of instances must have the same network type. If the network type is VPC, the two types of instances must be in the same VPC. For access over the Internet, you must have applied for a public endpoint for the ApsaraDB for MongoDB instance.
    -   If you move your pointer over an ECS security group, you can view its name and description. If you move your pointer over VPC, you can view the VPC ID. This way, you can quickly find an ECS security group.

## Common scenarios

-   [Connect to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in
         different regions.md)
-   [Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud
         account.md)

