# Configure a whitelist

This topic describes how to configure a whitelist after you create the instance. Only the devices whose IP addresses are added to the whitelists of the instance are allowed access to the instance. The default whitelist only contains the IP address 127.0.0.1, which indicates that no devices can connect to the instance.

-   You must configure a whitelist upon the first use of an instance. After the whitelist is configured, the connection address of the instance is displayed on the **Basic Information** and **Database Connection** pages.
-   Proper configuration of the whitelists can enhance access security of ApsaraDB for MongoDB. We recommend that you regularly maintain the whitelist.

## Standalone or Replica Set instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Settings**.

6.  Click the ![More](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7023797951/p13206.png) icon in the **Actions** column, and select **Manually Modify** or **Import ECS Intranet IP**.

    -   Click **Manually Modify**. In the dialog box that appears, enter an IP address or CIDR block, and click **OK**.
    -   Click **Import ECS Intranet IP**. In the dialog box that appears, the internal IP addresses of the ECS instances of your Alibaba Cloud account are displayed. You can select the desired IP addresses, add them to a whitelist, and click **OK**.

        ![Add internal network IP address of the ECS instance to a whitelist](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8023797951/p13209.png)

    **Note:**

    -   If a whitelist contains more than one IP address, separate them with commas \(,\). Every IP address in a whitelist must be unique. A whitelist can contain a maximum of 1,000 IP addresses.

        Supported formats include 0.0.0.0/0, 10.23.12.24 \(single IP address\), and 10.23.12.24/24. 10.23.12.24/24 is a CIDR notation \(for more information, see [CIDR blocks](~~54484~~)\), in which the suffix /24 indicates the number of bits for the prefix of the IP address. The prefix consists of 1 to 32 bits.

    -   If the value is 0.0.0.0/0 or empty, the ApsaraDB for MongoDB instance can be accessed by all IP addresses. In this situation, the database is at high security risk.

## Sharded cluster instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Settings**.

6.  Click the ![More](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7023797951/p13206.png) icon in the **Actions** column, and select **Manually Modify** or **Import ECS Intranet IP**.

    -   Click **Manually Modify**. In the dialog box that appears, enter an IP address or CIDR block, and click **OK**.
    -   Click **Import ECS Intranet IP**. In the dialog box that appears, the internal IP addresses of the ECS instances of your Alibaba Cloud account are displayed. You can select the desired IP addresses, add them to a whitelist, and click **OK**.

        ![Add internal network IP address of the ECS instance to a whitelist](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8023797951/p13209.png)

    **Note:**

    -   If a whitelist contains more than one IP address, separate them with commas \(,\). Every IP address in a whitelist must be unique. A whitelist can contain a maximum of 1,000 IP addresses.

        Supported formats include 0.0.0.0/0, 10.23.12.24 \(single IP address\), and 10.23.12.24/24. 10.23.12.24/24 is a CIDR notation \(for more information, see [CIDR blocks](~~54484~~)\), in which the suffix /24 indicates the number of bits for the prefix of the IP address. The prefix consists of 1 to 32 bits.

    -   If the value is 0.0.0.0/0 or empty, the ApsaraDB for MongoDB instance can be accessed by all IP addresses. In this situation, the database is at high security risk.

## Common connection scenarios

-   [Connect a local client to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account.md)

