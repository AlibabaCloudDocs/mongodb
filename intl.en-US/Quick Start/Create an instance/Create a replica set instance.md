# Create a replica set instance

This topic describes how to create a replica set instance in the ApsaraDB for MongoDB console.

-   An Alibaba Cloud account is created. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/zh/doc-detail/50482.htm).
-   Your account balance is sufficient if you want to create a pay-as-you-go instance.

## Billing information

For more information, see [Billing items and pricing](/intl.en-US/Purchase Guide/Billing items and pricing.md).

## Procedure

After you perform the following operations, ApsaraDB for MongoDB creates an instance. You do not need to manually install or deploy an instance.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  On the **Replica Set Instances** page, click **Create Instance**.

5.  Click **Replica Set \(Subscription\)** or **Replica Set \(Pay-as-you-go\)**.

    **Note:**

    -   Subscription: You must pay for an instance when you create the instance. This method is more cost-effective than the pay-as-you-go method. We recommend that you select this method for long-term use. A longer subscription period enables a larger discount.
    -   Pay-as-you-go: You are billed on an hourly basis based on the used resources. We recommend that you select this billing method for short-term use. You can release your pay-as-you-go instance if you no longer need the instance, which reduces costs.
6.  Configure the instance parameters. The following table describes the related parameters.

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |**Basic Configuration**|**Region**|The region to create the instance. After an instance is created, you cannot change its region. Exercise caution when you select the region.

Instances in the same region, such as an [ECS](~~25367~~) instance and an ApsaraDB for MongoDB instance, can be connected with each other over an internal network. |
    |**Zone**|A [zone](~~40654~~) is a geographic area that has an independent power supply and network. An ECS instance and an ApsaraDB for MongoDB instance in the same zone can be connected over an internal network with minimum network latency.

**Note:** To implement zone-disaster recovery, you can deploy the replica set instance across multiple zones. For more information, see [Create a multi-zone replica set instance](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone replica set instance.md). |
    |**Database Version**|The MongoDB version of the replica set instance. Valid values:4.2, 4.0, and 3.4. For more information about versions, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

**Note:**

    -   ApsaraDB for MongoDB 3.2 is no longer available. For more information, see [Notice: ApsaraDB for MongoDB has phased MongoDB 3.2 out and released MongoDB 4.2 since February 4](/intl.en-US/Product Notification/Notice: ApsaraDB for MongoDB has phased MongoDB 3.2 out and released MongoDB 4.2 since
         February 4.md).
    -   You can manually upgrade the database version when an instance is running. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md). |
    |**Storage Engine**|The storage engine of the instance, which is set to **WiredTiger**. |
    |**Replication Factor**|The number of nodes in the replica set instance. Select the number of nodes on demand. For example, you can select more nodes for business scenarios where more reads are processed than writes.|
    |**Network Type**|**Classic**|Cloud services in the classic network are not isolated. You can configure security groups or whitelist policies to block unauthorized access to the cloud services.|
    |**VPC**|A virtual private cloud \(VPC\) is an isolated network that has higher security and performance than the classic network. **Note:**

    -   You must create a VPC in advance. For more information, see [Work with VPCs](/intl.en-US/VPCs and vSwitchs/Work with VPCs.md).
    -   You can change the network type after you create an instance. For more information, see [Switch the network type of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md).
    -   If you want to migrate your applications to the cloud, you can build a virtual data center by connecting your self-managed data center to the resources in a VPC over a leased line or a virtual private network \(VPN\). For more information, see [Configure a hybrid access solution to switch the network type of an ApsaraDB for MongoDB instance from classic network to VPC](/intl.en-US/User Guide/Network connection management/Configure a hybrid access solution to switch the network type of an ApsaraDB for MongoDB
         instance from classic network to VPC.md). |
    |**Specifications**|**Plan**|    -   The CPU and memory that are occupied by the instance.
    -   The maximum number of connections and the maximum input/output operations per second \(IOPS\) vary based on different specifications. The maximum IOPS is separately measured for read and write operations, and the maximum sum of read and write operations can be twice the maximum IOPS. For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md). |
    |**Storage Space**|The dedicated storage capacity of each node in the replica set instance. **Note:** The storage capacity of a node stores your data, system, and log files. |
    |**Set Password**|    -   **Set Now**
    -   **Set Later**
|The password of the root user. The password of the root user. You can immediately set a password or set a password when the instance is running. For more information, see [Set a password for an ApsaraDB for MongoDB instance]().

    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! @ # $ % ^ & * ( ) _ + - =`
    -   The password must be 8 to 32 characters in length. |
    |**Purchase quantity** \(Available only for subscription instances\)|**Duration**|You can select one to nine months for the subscription period on a monthly basis,or one to three years for the subscription period on a yearly basis.|
    |**Quantity**|The number of subscription instances that you want to purchase. You can set an integer in the range of 1 to20.|
    |**Purchase quantity** \(Available only for pay-as-you-go instances\)|**Quantity**|The number of the pay-as-you-go instances that you want to purchase. You can set an integer in the range of 1 to 10.|

7.  Click **Buy Now**.

8.  On the **Confirm Order** page, read and select ApsaraDB for MongoDB Agreement of Service, and complete the payment.


## View the created instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.


## Troubleshoot if you cannot find the instance

|Possible cause|Solution|
|--------------|--------|
|You selected a wrong region in the console.|The region to create the instance. For more information, see [View the created instance](#section_egw_cbh_blu).|
|You improperly navigated to the Sharded Cluster Instances page.|In the left-side navigation pane, click **Replica Set Instances**. For more information, see [View the created instance](#section_egw_cbh_blu).|
|The instance list in the ApsaraDB for MongoDB console was not updated or was updated before the instance is created.|Wait several minutes and update the instance list to check whether the instance is added to the list.|
|Resources are insufficient.|The system may fail to create the instance due to insufficient resources. In this case, your payment is refunded. You can check the refund on the [Orders](https://expense.console.aliyun.com/#/order/list/) page.

After you confirm the refunded fees, you can try to create your instance in another region or zone. You can also[submit a ticket](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex). |

After you create an instance, you must configure a whitelist. For more information, see [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md). If you want to connect to the instance over the Internet, you must apply for a public endpoint. For more information, see [Apply for a public endpoint for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md).

For more information about instance connection methods and scenarios, see [Connect to an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance.md).

