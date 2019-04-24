# Create an instance {#task_hwt_zlx_p2b .task}

You can log on to the Alibaba Cloud [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) or call the CreateDBInstance operation to create an ApsaraDB for MongoDB instance. For more information about how to bill an instance, see Billing items and pricing. This topic describes how to create an instance in the ApsaraDB for MongoDB console.

-   You have registered an Alibaba Cloud account. If you do not have an Alibaba Cloud account, click [Register](https://account.aliyun.com/register/register.htm).
-   To create a Pay-As-You-Go instance, ensure that your account balance is sufficient.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the left-side navigation pane, click Replica Set Instances. On the page that appears, click **Create Instance** to go to the instance creation page.
3.  Select **Subscription** or **Pay-As-You-Go**. For more information about the billing methods, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#).
4.  Specify the instance configuration. The following table describes related parameters. 

    |Area|Parameter|Description|
    |:---|:--------|:----------|
    |**Basic Configuration**|**Region**| The geographical location of the instance. Instances in different regions cannot be interconnected through an intranet. Once an instance is created, you cannot change the region. Therefore, you need to select a region with caution.

 Instances in the same region \(such as an [ECS](https://www.alibabacloud.com/help/doc-detail/25367.htm) instance and an ApsaraDB for MongoDB instance\) can be interconnected through an intranet.

 |
    |**Zone**| The physical area with its power supply and network isolated from other counterparts in the same region.

 For more information about regions and zones, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

 An ApsaraDB for MongoDB instance and an ECS instance in different zones of the same region can be interconnected through an intranet. For more information, see [Connect to an ApsaraDB for MongoDB instance through a cross-zone intranet](https://www.alibabacloud.com/help/doc-detail/57139.htm).

 The network latency is minimal when an ECS instance and an ApsaraDB for MongoDB instance in the same zone are interconnected through an intranet.

 |
    |**Database Version**|The database version of the instance. Currently, ApsaraDB for MongoDB supports MongoDB 3.2, MongoDB 3.4, and MongoDB 4.0. **Note:** 

    -   You can manually upgrade the database version of an instance from MongoDB 3.2 to MongoDB 3.4 when the instance is running, but cannot downgrade the upgraded version.
    -   You cannot upgrade the database version of an existing instance from MongoDB 3.2 or MongoDB 3.4 to MongoDB 4.0. To use MongoDB 4.0, you need to select **MongoDB 4.0** for **Database Version** when you create an instance.
    -   The database version of an instance cannot be downgraded. You need to select a database version based on business requirements.
 |
    |**Storage Engine**| The storage engine of the instance. You can select WiredTiger, RocksDB, or TerarkDB.

**Note:** Supported storage engines may vary in different database versions.

 For more information about database versions and storage engines, see [Versions and storage engines](../../../../intl.en-US/Product Introduction/Versions and storage engines.md#).

 |
    |**Replication Factor**|The number of nodes that you select for the replica set instance based on business requirements. For example, you can select more nodes for business scenarios that require more read operations than write operations.|
    |**Network Type**|**Classic Network**|The classic network on which cloud services are not isolated. You can configure a security group or whitelist policy for them to block unauthorized access.|
    |**VPC**|The Virtual Private Cloud, which is recommended. A VPC is an isolated network environment that provides enhanced security and better performance than traditional classic networks. You need to create a VPC in advance. For more information about how to configure a VPC, see [Configure a VPC for a new instance](../../../../intl.en-US/User Guide/Network connection management/Configure a VPC for a new instance.md#). **Note:** 

    -   You can also change the network type of an instance after creating the instance. For more information, see [Switch the network type of an instance](../../../../intl.en-US/User Guide/Network connection management/Switch the network type of an instance.md#).
    -   You can use a physical connection or Virtual Private Network \(VPN\) to combine your on-premises IDC with cloud resources in Alibaba Cloud VPC to create a virtual IDC, so that you can smoothly migrate your applications to the cloud. For more information, see [Configure a hybrid access solution to smoothly switch from a classic network to a VPC](../../../../intl.en-US/User Guide/Network connection management/Configure a hybrid access solution to smoothly switch from a classic network to a VPC.md#).
 |
    |**Specifications**|**Specification**|The CPU and memory occupied by the instance.|
    |**Storage Space**|The maximum number of connections and maximum input/output operations per second \(IOPS\) vary depending on specifications. The maximum IOPS indicates the maximum number of read or write operations separately. The maximum sum of read and write operations can be twice the maximum IOPS.|
    |**Set Password**|     -   **Set now**
    -   **Set after purchase**
 | The password used to connect to ApsaraDB for MongoDB for the first time.

     -   The password must consist of any three types of characters, including uppercase letters, lowercase letters, digits, and special characters. Special characters include exclamation points \(!\), number signs \(\#\), dollar signs \($\), percent signs \(%\), carets \(^\), ampersands \(&\), asterisks \(\*\), parentheses \(\(\)\), underscores \(\_\), plus signs \(+\), hyphens \(-\), and equal signs \(=\). \[DO NOT TRANSLATE\]
    -   The password must be 8–32 characters in length.
 You can set a password when creating the instance. You can also set a password or [reset the password](intl.en-US/Quick Start for Replica Set/Set a password.md#) when the instance is running.

 |
    |**Purchase Quantity**|**Duration**|     -   Subscription: Select the duration and quantity for the subscription-based instance to be purchased. You can select one to nine months for the subscription period on a monthly basis, or one to three years for the subscription period on a yearly basis.
    -   Pay-As-You-Go: Select the quantity for the Pay-As-You-Go instance to be purchased with the same configuration. You can select an integer in the range of 1 to 10.
 |
    |**Quantity**|

5.  Click **Buy Now** to go to the Confirm Order page.
6.  On the Confirm Order page that appears, read and select **ApsaraDB for MongoDB Agreement of Service** and follow the instructions to complete the payment process.

