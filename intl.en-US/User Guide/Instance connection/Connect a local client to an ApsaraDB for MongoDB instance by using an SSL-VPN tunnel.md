# Connect a local client to an ApsaraDB for MongoDB instance by using an SSL-VPN tunnel

This topic describes how to connect a local client to a VPC-type ApsaraDB for MongoDB instance by using an SSL-VPN tunnel. The SSL-VPN tunnel helps helps you manage the ApsaraDB for MongoDB instance from the local client with ease.

## Scenarios

-   The public IP address of the local client dynamically changes. As a result, you must frequently update the IP address whitelist that contains the public IP address of the local client in the ApsaraDB for MongoDB console. If you do not delete expired IP addresses at the earliest opportunity, security risks may arise.
-   A high level of security is required when you connect to an ApsaraDB for MongoDB instance over the Internet.
-   You need to log on to the ApsaraDB for MongoDB instance from an ECS instance over the Internet. This may cause security risks. Therefore, you must separate ECS management permissions from ApsaraDB for MongoDB database permissions.

## Billing

Fees occur when you create a VPN gateway. For more information, see [Pay-as-you-go](https://www.alibabacloud.com/help/zh/doc-detail/72351.htm).

## Prerequisites

-   The network type of the ApsaraDB for MongoDB instance is VPC. For more information about how to switch the network type from classic network to VPC, see [Switch from classic network to VPC](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md).
-   The Classless Inter-Domain Routing \(CIDR\) block of the local client is different from that of the ApsaraDB for MongoDB instance.
-   The local client can access the Internet.

## Networking

![SSL-VPN tunnel between a local client and an ApsaraDB for MongoDB instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2335298951/p44679.png)

## Step 1: Create a VPN gateway

For more information, see [Create a VPN gateway](/intl.en-US/User Guide/Manage a VPN Gateway/Create a VPN gateway.md).

## Step 2: Create an SSL server

For more information, see [Create an SSL server](/intl.en-US/User Guide/Configure SSL-VPN/Manage an SSL server/Create an SSL server.md).

## Step 3: Create an SSL client

For more information, see [Create an SSL client certificate](/intl.en-US/User Guide/Configure SSL-VPN/Manage an SSL client certificate/Create an SSL client certificate.md).

## Log on to the ApsaraDB for MongoDB instance from the client by using the SSL-VPN tunnel

Windows is used in this example. For more information about other operating systems, see [Remote access from a Linux client](https://www.alibabacloud.com/help/zh/doc-detail/65075.htm#title-60o-ywt-7cz) and [Remote access from a Mac client](https://www.alibabacloud.com/help/zh/doc-detail/65068.htm#d7e230).

1.  Log on to the [VPC console](https://vpc.console.aliyun.com).
2.  In the upper-left corner of the page, select the region.
3.  In the left-side navigation pane, choose **VPN** \> **SSL Clients**.
4.  On the right of the SSL client that you created, click **Download** to download the generated client certificate package.
5.  Download the OpenVPN software package and install OpenVPN on the client to which you want to connect by using the SSL-VPN tunnel.
6.  Decompress the client certificate package that you downloaded and copy the client certificate file to the config folder of the OpenVPN installation directory.
7.  Click **Connect**.

    ![Initiate an SSL connection.](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2335298951/p44665.png)

8.  Add the CIDR block of the VPC to which the ApsaraDB for MongoDB instance belongs to an IP address whitelist of this instance. In this example, add the IP address 172.16.1.0/24 to the whitelist.
9.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
10. Obtain the internal endpoints of the ApsaraDB for MongoDB instance. For more information, see [Overview of replica set instance connections]().

    ![VPC of an ApsaraDB for MongoDB instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2335298951/p44701.png)

11. Use the [mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a replica set instance by using the mongo shell.md) or other management tools to log on to the ApsaraDB for MongoDB instance.

    **Note:** Log on by using an internal endpoint of the ApsaraDB for MongoDB instance.


