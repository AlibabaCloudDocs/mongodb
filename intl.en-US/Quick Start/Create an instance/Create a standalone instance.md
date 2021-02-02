# Create a standalone instance

This topic describes how to create a standalone instance in the ApsaraDB for MongoDB console.

-   An Alibaba Cloud account is registered. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/zh/doc-detail/50482.htm).
-   Your account balance is sufficient if you want to create a pay-as-you-go instance.

## Billing

For more information, see [Billing items and pricing](/intl.en-US/Purchase Guide/Billing items and pricing.md).

## Procedure

After you perform the following operations, ApsaraDB for MongoDB automatically creates an instance. You do not need to manually install or deploy an instance.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  On the **Replica Set Instances** page, click **Create Instance**.

5.  Clickthe **Replica Set \(Pay-as-you-go\)** tab.

6.  Configure the instance. The following table describes related parameters.

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |**Basic Configuration**|**Region**|The region where the ApsaraDB for MongoDB instance is deployed. Standalone instances can be created only in the following regions: Japan \(Tokyo\),China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), and China \(Shenzhen\).

**Note:**

    -   After an instance is created, you cannot change its region. Use caution when you select the region.
    -   We recommend that you set the same region as that of the [ECS](https://www.alibabacloud.com/help/zh/doc-detail/25367.htm) instance where your business is deployed. Otherwise, the ECS and standalone ApsaraDB for MongoDB instances cannot communicate with each other over an internal network. |
    |**Zone**|Geographic areas in a region with independent power grids and networks. For more information, see [Regions and zones](https://www.alibabacloud.com/help/zh/doc-detail/40654.htm).

**Note:** An ECS instance and a standalone ApsaraDB for MongoDB instance in the same zone can be interconnected over an internal network with the minimum network latency. |
    |**Database Version**|The MongoDB version of the instance. Standalone instances support only MongoDB 3.4. Set the value to **MongoDB 3.4**. |
    |**Storage Engine**|The storage engine is **WiredTiger**. |
    |**Replication Factor**|Set the value to **Single Node**.|
    |**Network Type**|**VPC**|An isolated network with higher security and performance than the classic network. **Note:** You must create a VPC in advance. For more information, see [Create a VPC](/intl.en-US/VPCs and VSwitches/VPC management/Create a VPC.md). |
    |**Specifications**|**Specification**|    -   The CPU and memory occupied by the instance.
    -   The maximum number of connections and maximum IOPS varies based on different specifications. The maximum IOPS is separately measured for read and write operations, and the maximum sum of read and write operations can be twice the maximum IOPS. For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md). |
    |**Storage Space**|The storage space of the instance. **Note:** The storage space stores your data, system files, and log files. |
    |**Set Password**|    -   **Set up immediately**
    -   **Set up after created**
|The password of the root user. You can immediately set a password or reset it during the running of the instance. For more information, see [Set a password for a standalone ApsaraDB for MongoDB instance]().

    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include ! \# $ % ^ & \* \( \) \_ + - =
    -   The password must be 8 to 32 characters in length. |
    |**Purchase quantity**|**Duration**|Pay-as-you-go: Select the quantity for pay-as-you-go instances to be purchased with the same configuration. You can select an integer in the range of 1 to 10.

**Note:** The billing method of standalone instances must be pay-as-you-go. |
    |**Quantity**|

7.  Click **Buy Now** to go to the **Confirm Order** page.

8.  On the Confirm Order page, read and select **ApsaraDB for MongoDB Agreement of Service** and complete the payment.


## View the created instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.


## Troubleshoot if you cannot find the instance

|Possible cause|Solution|
|--------------|--------|
|You selected a wrong region in the console.|Select the region where the instance is deployed. For more information, see [View the created instance](#section_p39_06d_838).|
|You opened an incorrect page.|In the left-side navigation pane, click **Replica Set Instances**. For more information, see [View the created instance](#section_p39_06d_838).|
|The instance list in the ApsaraDB for MongoDB console is not updated or updated before the instance is created.|Wait several minutes and update the instance list to check whether the instance is added to the list.|
|Resources are insufficient.|The system may fail to create the instance due to insufficient resources. In this case, your payment is refunded. You can check the refund on the [Orders](https://expense.console.aliyun.com/#/order/list/) page.

After you confirm the refunded fees, you can try to create your instance in another zone. You can also [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex). |

After you create an instance, you must configure a whitelist. For more information, see [Configure a whitelist for a standalone ApsaraDB for MongoDB instance](). If you want to connect to the instance over the Internet, you must apply for a public endpoint. For more information, see [Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance]().

For more information about instance connection methods and connection scenarios, see [Connect to an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance.md).

