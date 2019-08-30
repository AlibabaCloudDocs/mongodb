# Restore a database in ApsaraDB for MongoDB {#concept_kvp_mrg_fhb .concept}

ApsaraDB for MongoDB supports database restoration. You can restore the data of a certain database or databases back to a specific point in time in a newly-created instance.

## Instruction {#section_orh_qqh_fhb .section}

Instances created after March 26, 2019 support database restoration. This function will be open to existing instances in the future. Follow the official website for update information.

## Prerequisites {#section_zgq_r3b_fhb .section}

-   The instance is created after March 26, 2019.
-   The instance is located in China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou-Beijing Winter Olympics\), China \(Hohhot\), China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), or Singapore. Other regions are not supported.
-   The instance type is replica set. Standalone and sharded cluster instances are not supported.
-   The instance version is 3.4 or 4.0. V3.2 is not supported.
-   The storage engine of the instance is WiredTiger. RocksDB and TerarkDB are not supported.
-   The backup file in the instance backup list contains the database to be restored.

## Precautions {#section_y5t_vsg_fhb .section}

-   You can only restore databases from physical backups. Restoring databases from logical backups is not supported.
-   You can only restore databases to newly-created instances. Restoring databases to each original instance is not supported.

    **Note:** An instance will be created during database restoration. For the billing method of the instance, see [Billing items and pricing](https://help.aliyun.com/document_detail/54285.html#concept-jww-bny-32b).


## Procedure {#section_ghm_m5b_fhb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the page, select the region of the instance.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the instance to be restored and click the instance ID.
5.  In the left-side navigation pane, click **Backup and Recovery**.
6.  On the Backup and Recovery page, click **Create Instance By Time Point**.
7.  In the dialog box that appears, set the parameters listed in the following table.

    ![Restore a database in ApsaraDB for MongoDB](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149680/156714562441591_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Select recovery time point|Select a point in time that you want to restore the database to. You can restore the database to any point within the past seven days.**Note:** The time must be earlier than the current time, and must be later than the time when the database was created.

|
    |Select recovery database|     -   All Databases
    -   Select Databases: Restore certain databases in the instance. You can select the databases that you want to restore or click **Enter Databases** to enter databases manually.

**Note:** If you want to restore more than one database, separate the multiple database names with commas \(,\).

 |

8.  Click **OK**. The Instance Purchase page appears.
9.  Configure the new instance.

    **Note:** In the **Basic Configuration** area, do not configure **Region**, **Database Version**, **Storage Engine**, and **Node Number**.

    |Category|Parameter|Description|
    |:-------|:--------|:----------|
    |**Basic Configuration**|**Zone**| A zone indicates a physical area in a region with independent power grids and networks. For more information, see [Regions and zones](https://www.alibabacloud.com/help/zh/doc-detail/40654.htm).

 ApsaraDB for MongoDB and ECS instances between different zones in the same region can be connected through the internal network. For more information, see [Connect to an ApsaraDB for MongoDB instance through a cross-zone intranet](intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance through a cross-zone intranet.md#).

 **Note:** When the ECS instance and the ApsaraDB for MongoDB instance in the same zone are connected through the internal network, the network latency is the minimum.

 |
    |**Network Type**|-|     -   **Classic Network**: Cloud services on a classic network are not isolated, and unauthorized access to a cloud service is blocked only by the security group or whitelist policy of the service.
    -   **VPC** \(recommended\): A Virtual Private Cloud \(VPC\) is an isolated network with higher security and performance than the traditional classic network. The VPC is to be created before creating an instance. For more information, see [Configure a VPC for a new instance](intl.en-US/User Guide/Network connection management/Configure a VPC for a new instance.md#).
 |
    |**Specification Configuration**|**Specification**|     -   The CPU and memory occupied by the instance.
    -   The maximum number of connections and maximum IOPS vary depending on different specifications. The maximum IOPS is measured respectively under the read and write permissions, and can double under the mixed read/write permissions.
 |
    |**Storage Space**|The storage space exclusive to each node in the replica set instance.**Note:** The storage space of a node stores your data, system, and log files.

|
    |**Password Settings**|     -   **Set Now**
    -   **Set Later**
 |Set the password of the MongoDB database. You can [set the password](intl.en-US/Quick Start for Replica Set/Set a password.md#) when creating or running the instance.    -   The password must contain characters from at least three of the following categories: uppercase letters, lowercase letters, digits, and special characters. Special characters include !\#$%^&\*\(\)\_+-=
    -   The password must be 8 to 32 characters in length.
|
    |**Quantity Purchased**|**Duration**|Subscription: Set the duration and quantity of the subscription instance. The subscription duration can be one to nine months or one to three years.**Note:** This parameter is required only for subscription instances.

|
    |**Quantity**|Set the number of instances with the same specifications. It can be set to an integer of 1 to 10.|

10. Click **Buy Now**. The Confirm Order page appears.
11. On the Confirm Order page, read and select **ApsaraDB for MongoDB Agreement of Service**, and make the payment as prompted.

