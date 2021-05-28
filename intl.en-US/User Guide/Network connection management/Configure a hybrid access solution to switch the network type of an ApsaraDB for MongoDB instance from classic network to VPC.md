# Configure a hybrid access solution to switch the network type of an ApsaraDB for MongoDB instance from classic network to VPC

This topic describes how to configure a hybrid access solution to switch the network type of an ApsaraDB for MongoDB instance from classic network to Virtual Private Network \(VPC\) without network interruptions.

## Prerequisites

-   The instance is a replica set or sharded cluster instance.
-   The network type of the instance is classic network.
-   A VPC is created in the same region as the instance. For more information, see [Create a VPC](~~65398~~) and [Create a vSwitch](~~65387~~).

## Background information

-   In the hybrid network access mode, you cannot switch the network type to classic network.
-   When you switch the network type of an ApsaraDB for MongoDB instance from classic network to VPC, you can choose to retain the internal endpoints on the classic network for up to 120 days. In the hybrid network access mode, the instance supports access from ECS instances in both the classic network and VPC.
-   In the hybrid network access mode, you can switch the network types of ECS instances and other Alibaba Cloud services from classic network to VPC until all services are deployed in a VPC.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connections**.

6.  In the Intranet Connection - VPC section, click **Switch to VPC**.

7.  In the **VPC** panel, configure the parameters.

    ![Configure the VPC](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9045298951/p37314.png)

    1.  Select a **VPC** and a **VSwitch**.

    2.  Turn on **Retain the connection address of the classic network**.

    3.  Select **Expiration Time \(Days\)**.

8.  Click **OK**.


