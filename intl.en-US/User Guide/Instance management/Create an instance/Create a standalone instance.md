# Create a standalone instance

This topic describes how to create a standalone instance in the ApsaraDB for MongoDB console.

-   An Alibaba Cloud account is created. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/zh/doc-detail/50482.htm).
-   Your account balance is sufficient if you want to create a pay-as-you-go instance.

## Billing

For more information, see [Billing items and pricing](/intl.en-US/Purchase Guide/Billing items and pricing.md).

## Procedure

After you perform the following operations, ApsaraDB for MongoDB automatically creates your instance. You do not need to manually install or deploy an instance.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  On the **Replica Set Instances** page, click **Create Instance**.

5.  Click **Replica Set \(Pay-as-you-go\)**.

6.  Configure the instance parameters. The following table describes the related parameters.

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |**Basic Configuration**|**Region**|The region where the ApsaraDB for MongoDB instance is deployed. Standalone instances can be created only in the following regions: China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), China \(Shenzhen\), and Japan \(Tokyo\).

**Note:**

    -   After an instance is created, you cannot change the region. Exercise caution when you select the region.
    -   An ECS instance and a standalone ApsaraDB for MongoDB instance in the same zone can be connected over an internal network. |
    |**Zone**|Select a zone from the region. Zones are geographic locations within a region. Each zone contains independent power supply and network resources. For more information about zones, see [Zones](https://www.alibabacloud.com/help/zh/doc-detail/40654.htm).

**Note:** An ECS instance and a standalone ApsaraDB for MongoDB instance in the same zone can be connected over an internal network with the minimum network latency. |
    |**Database Version**|The MongoDB version of the standalone instance. Standalone instances support only MongoDB 3.4. Set the value to **MongoDB 3.4**. |
    |**Storage Engine**|The storage engine of the instance, which is fixed as **WiredTiger**. |
    |**Replication Factor**|The number of nodes in the standalone instance. Set the value to **Single Node**.|
    |**Network Type**|**VPC**|An isolated network with higher security and performance than the classic network. **Note:** You must create a VPC in advance. For more information, see [Create a VPC](/intl.en-US/VPCs and vSwitchs/Work with VPCs.md). |
    |**Specifications**|**Plan**|    -   The CPU and memory occupied by the instance.
    -   The maximum number of connections and the maximum input/output operations per second \(IOPS\) vary based on specifications. The maximum IOPS is separately measured for read and write operations, and the maximum sum of read and write operations can be twice the maximum IOPS. For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md). |
    |**Storage Space**|The storage capacity of the instance. **Note:** The storage capacity stores your data, system, and log files. |
    |**Set Password**|    -   **Set Now**
    -   **Set Later**
|The password of the root user. You can set a password immediately or during the running of the instance. For more information, see [Set a password](/intl.en-US/Quick Start/Single-node quick start/Set a password for a standalone ApsaraDB for MongoDB instance.md).

    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include ! @ \# $ % ^ & \* \( \) \_ + - =
    -   The password must be 8 to 32 characters in length. |
    |**Purchase quantity**|**Quantity**|The number of the pay-as-you-go instances that you want to purchase. You can set an integer in the range of 1 to 10.|

7.  Click **Buy Now** to go to the **Confirm Order** page.

8.  On the Confirm Order page, read and select **ApsaraDB for MongoDB Agreement of Service**, and complete the payment.


## View the created instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.


## Troubleshoot if you cannot find the instance

|Possible cause|Solution|
|--------------|--------|
|You selected a wrong region in the console.|Select the region where the instance is deployed. For more information, see [View the created instance](#section_p39_06d_838).|
|You opened an incorrect page.|Select the correct instance list. Perform the following operations:1.  View the created instance. For more information, see [View the created instance](#section_p39_06d_838).
2.  Select the correct instance list. For more information, see **Replica Set Instances**. |
|The instance list in the ApsaraDB for MongoDB console is not updated or updated before the instance is created.|Wait several minutes and then update the instance list to check whether the instance is added to the list.|
|Resources are insufficient.|The system may fail to create the instance due to insufficient resources. In this case, your payment is refunded. You can check the refund on the [Orders](https://expense.console.aliyun.com/#/order/list/) page.

After you confirm the refunded fees, you can try one of the following methods:

-   Create an instance in another zone.
-   Submit a ticket. For more information, see [Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex). |

After you create an instance, perform the following operations:

-   Set a password if you do not set a password when you create the instance. For more information, see [Reset the password](/intl.en-US/Quick Start/Quick Start of Replica Set/Reset the password.md).
-   Configure a whitelist for the instance to allow external devices to access the instance. For more information, see [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Quick Start of Replica Set/Configure a whitelist for an ApsaraDB for MongoDB instance.md).
-   Apply for a public endpoint if you want to connect to the instance over the Internet. For more information, see [Apply for a public endpoint for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Quick Start of Replica Set/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md).

For more information about instance connection methods and connection scenarios, see [Connect to an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance.md).

