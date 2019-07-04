# Connect the local client to ApsaraDB for MongoDB instances through an SSL VPN tunnel {#concept_185604 .concept}

You can build an SSL VPN tunnel between the management terminal and the VPC in which ApsaraDB for MongoDB instances are deployed. This enables a safe and secure connection to ApsaraDB for MongoDB instances.

## Scenario {#section_fnd_jrq_ggb .section}

-   The environment in which the client that manages the ApsaraDB for MongoDB database has no static public IP address. In this case, you are required to frequently adjust the IP addresses in the whitelist through the ApsaraDB for MongoDB console. If you fail to delete expired IP addresses, security risks may arise.
-   The environment in which the client runs requires high network security. A higher-level of security is required when you connect to AsparaDB for MongoDB instances through a public network.
-   When database administrators use a public network to log on to the ApsaraDB for MongoDB database through ECS, they threaten to expose management permissions. Therefore, you are required to separate ECS management permissions from ApsaraDB for MongoDB database permissions.

## Billing information {#section_vhc_dxq_ggb .section}

Certain fees occur when you create a VPN gateway. For more information, see [Pricing](https://www.alibabacloud.com/help/doc-detail/72351.htm).

## Prerequisites {#section_jg1_tvq_ggb .section}

-   The network type of the ApsaraDB for MongoDB instances is VPC. For more information about how to switch from the classic network to the VPC, see [Switch from a classic network to a VPC](intl.en-US/User Guide/Network connection management/Switch the network type of an instance.md#section_tp1_1sl_2fb).
-   Ensure that the IP address range of the local client and that of an ApsaraDB for MongoDB instance is different.
-   Ensure that the local client can access the public network.

## Example of environment preparation {#section_yf2_jdr_ggb .section}

![Environment preparation of the SSL connection ](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/159808/156223066544679_en-US.png)

## Step 1 Create a VPN gateway {#section_xxd_vwq_ggb .section}

1.  Log on to the [VPC console](https://vpc.console.aliyun.com).
2.  In the upper-left corner of the homepage, select the region.
3.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
4.  On the VPN Gateways page, click **Create VPN Gateway**.
5.  Configure the specifications of the VPN gateway as needed.

    |Parameter|Description|
    |:--------|:----------|
    |Region|The region in which the VPN gateway is located. Select the region that is the same as that of the ApsaraDB for MongoDB instance.|
    |VPC|Select the VPC to which the ApsaraDB for MongoDB instance belongs.|
    |Peak Bandwidth|Select the bandwidth specifications for the VPN gateway. The bandwidth is that of the public network which is used for the VPN gateway.|
    |IPSec-VPN| Specify whether to enable the IPSec-VPN. You can enable this function as needed. You can access the VPN through the terminal. Therefore, select **Disable IPSec-VPN**.

 The IPSec-VPN function provides site-to-site connections. You can create an IPSec tunnel to connect an on-premises IDC to a VPC, or connect two VPCs.

 |
    |SSL VPN| Specify whether to enable the SSL VPN function. You can enable this function as needed. In this case, you need to access the VPN through the terminal. Therefore, select **Enable SSL VPN**.

 SSL VPN provides point-to-site VPN connections. You do not need to configure the client gateway. You can access the VPN directly through the terminal.

 |
    |Billing Cycle|Select the duration of subscription-based instances. The subscription duration can be one to nine months on a monthly basis or one to three years on a yearly basis.|
    |Auto Renewal|Specify whether to enable auto renewal for the instance.     -   By Month: The auto renewal period is one month.
    -   By Year: The auto renewal period is one year.
 |

6.  Click **Purchase Now**, and follow the instructions to complete the payment.

## Step 2 Create an SSL server {#section_qxs_y2r_ggb .section}

1.  Log on to the [VPC console](https://vpc.console.aliyun.com).
2.  In the upper-left corner of the homepage, select the region.
3.  In the left-side navigation pane, choose **VPN** \> **SSL Servers**.
4.  On the SSL Servers page, click **Create SSL Server**.
5.  In the Create SSL Server dialog box, configure parameters of the SSL server.

    |Parameter|Description|
    |:--------|:----------|
    |Name| The name of the SSL server.

 The name must be 2 to 128 characters in length and must start with a letter. It can contain letters, digits, underscores \(\_\), and hyphens \(-\).

 |
    |VPN Gateway| The associated VPN gateway. Select the VPN gateway created in [Step 1 Create a VPN gateway](#section_xxd_vwq_ggb).

 |
    |Local Network Segment| The local network segment which is the address range to be accessed by the client through the SSL VPN. It can be the network segment of a VPC, a VSwitch, or the network segment of an IDC that is connected with a VPC through a leased line, or a cloud service such as RDS or OSS.

 The network segment you enter is the network segment address of the VSwitch in a VPC to which an ApsaraDB for MongoDB instance belongs: **172.16.1.0/24**.

 **Note:** The subnet mask of the local network segment must be 16-bit to 29-bit.

 |
    |Client Network Segment| The client network segment is the address segment that assigns access addresses to the virtual NICs of a client. When the client accesses the local network through an SSL VPN connection, a VPN gateway assigns an IP address from the specified client network segment to the client.

 In this case, enter **192.168.100.0/24**.

 **Note:** Make sure that the client network segment and the **Local Network Segment** are different.

 |

6.  Click **OK**.

## Step 3 Create an SSL client {#section_oxb_dfr_ggb .section}

1.  Log on to the [VPC console](https://vpc.console.aliyun.com).
2.  In the upper-left corner of the homepage, select the region.
3.  In the left-side navigation pane, choose **VPN** \> **SSL Clients**.
4.  On the SSL Clients page, click **SSL Client Certificate**.

    |Parameter|Description|
    |:--------|:----------|
    |Name| The name of the SSL client certificate.

 The name must be 2 to 128 characters in length and must start with a letter. It can contain letters, digits, underscores \(\_\), and hyphens \(-\).

 |
    |SSL Server|Select the SSL server created in [Step 2 Create an SSL server](#section_qxs_y2r_ggb).|

5.  Click **OK**.

## Log on to the ApsaraDB for MongoDB database on the client through an SSL VPN tunnel {#section_ds2_jhr_ggb .section}

This topic uses Windows as an example. For more information about other operating systems, see the following topics: [Connect SSL VPN in the Linux system](https://www.alibabacloud.com/help/doc-detail/65075.htm)and [Connect SSL VPN in the Mac system](https://www.alibabacloud.com/help/doc-detail/65068.htm).

1.  Log on to the [VPC console](https://vpc.console.aliyun.com).
2.  In the upper-left corner of the homepage, select the region.
3.  In the left-side navigation pane, choose **VPN** \> **SSL Clients**.
4.  To the right of the SSL client instance you have created, click **Download** to download the generated client certificate.
5.  Download and install an OpenVPN client on the client to which you need to connect through the SSL VPN tunnel.
6.  Decompress the client certificate that you downloaded in the preceding step and copy it to the config folder of the OpenVPN installation directory.
7.  Click **Connect** to initiate a connection.

    ![Initiate an SSL connection](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/159808/156223066544665_en-US.png)

8.  Add the IP address of the VPC to which the ApsaraDB for MongoDB instance belongs to the whitelist of the ApsaraDB for MongoDB instance. The IP address **172.16.1.0/24** is added to the whitelist of the ApsaraDB for MongoDB instance.
9.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
10. Obtain the private IP address of the ApsaraDB for MongoDB instance. For more information, see [Connect to a replica set instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to an replica set instance through the mongo shell.md#).

    ![Private IP address of ApsaraDB for MongoDB instances](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/159808/156223066644701_en-US.png)

11. Use the [mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Log on to the MongoDB instance through the mongo shell.md#) or other management tools to log on to the ApsaraDB for MongoDB database.

    **Note:** Log on using the private IP address of the ApsaraDB for MongoDB instance.


