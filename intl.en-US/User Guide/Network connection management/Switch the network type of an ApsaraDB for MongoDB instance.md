# Switch the network type of an ApsaraDB for MongoDB instance

This topic describes how to switch the network type of an ApsaraDB for MongoDB instance between classic network and VPC in the ApsaraDB for MongoDB console.

## Prerequisites

A replica set or sharded cluster instance is used.

**Note:** For a standalone instance, its network type is always VPC and cannot be changed.

## Precautions

When you switch the network type of an instance, a transient connection error will occur to the instance. We recommend that you perform this operation during off-peak hours or make sure that your application is configured to reconnect to the instance after it is disconnected. This protects your business from being affected.

**Note:** You can choose to retain the internal endpoints on the classic network. This way, you can switch the network type without a transient connection error. For more information, see [Configure a hybrid access solution to switch the network type of an ApsaraDB for MongoDB instance from classic network to VPC](/intl.en-US/User Guide/Network connection management/Configure a hybrid access solution to switch the network type of an ApsaraDB for MongoDB
         instance from classic network to VPC.md).

## Internal connection strings

-   Intranet Connection - Classic Network: Cloud services on a classic network are not isolated. Unauthorized access can only be blocked by the security groups or whitelists of the cloud services.
-   Intranet Connection - VPC: A VPC is an isolated network with higher security and performance than a classic network. By default, an ApsaraDB for MongoDB instance provides internal endpoints on a VPC.

## Switch from classic network to VPC

1.  Create a VPC in the same region as the target ApsaraDB for MongoDB instance. For more information, see [Work with VPCs](/intl.en-US/VPCs and vSwitchs/Work with VPCs.md).

2.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

3.  In the upper-left corner of the page, select the resource group and the region of the target instance.

4.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

5.  Find the target instance and click its ID.

6.  In the left-side navigation pane, click **Database Connections**.

7.  In the Intranet Connection - Classic Network section, click **Switch to VPC**.

8.  In the **VPC** dialog box, specify **VPC** and **VSwitch**.

    **Note:**

    -   You can turn on the **Retain the connection address of the classic network** switch to generate new internal endpoints on the VPC and keep the existing internal endpoints on the classic network within a specified period. When an internal endpoint on the classic network expires, it is automatically released.
    -   If you do not turn on the **Retain the connection address of the classic network** switch, a transient connection error may occur while you switch the network type. In this case, Alibaba Cloud services such as ECS on the classic network cannot connect to this instance.
9.  Click **OK**.


## Switch from VPC to classic network

After you switch the network type of the instance to classic network, the internal endpoints on the VPC are released and ECS instances in the VPC can no longer connect to this instance with these endpoints. ApsaraDB for MongoDB generates new internal endpoints on the classic network and retains the same public endpoints. You must modify the connection information for your application.

**Note:** After you switch the network type of the instance to classic network, ECS instances in the VPC can no longer connect to this instance. While you switch the network type of the instance, a transient connection error may occur. We recommend that you perform this operation during off-peak hours or make sure that your application is configured to reconnect to the instance after it is disconnected. This protects your business from being affected.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connections**.

6.  In the Intranet Connection - Classic Network section, click **Switch to Classic Network**.

7.  In the message that appears, click **OK**.


