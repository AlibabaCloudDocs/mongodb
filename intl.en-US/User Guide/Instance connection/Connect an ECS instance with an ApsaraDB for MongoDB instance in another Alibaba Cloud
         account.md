# Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud account

If an ECS instance and an ApsaraDB for MongoDB instance do not belong to the same Alibaba Cloud account, you can use the methods in this topic to connect the ECS instance to the ApsaraDB for MongoDB instance over an internal network.

## Method 1: Migrate the ApsaraDB for MongoDB instance to the Alibaba Cloud account to which the ECS instance belongs

This method uses the data migration feature of [Data Transmission Service]() \(DTS\) to migrate the ApsaraDB for MongoDB database to the Alibaba Cloud account to which the ECS instance belongs.

Procedure

1.  Create an ApsaraDB for MongoDB instance in the Alibaba Cloud account to which the ECS instance belongs. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md). Skip this step if you have created an ApsaraDB for MongoDB instance.

    **Note:** When you create the ApsaraDB for MongoDB instance, select the same **region**, **zone**, and **VPC** as the ECS instance.

2.  Migrate the MongoDB database from the instance that belongs to the source Alibaba Cloud account to the instance that belongs to the destination Alibaba Cloud account. For more information, see [Migrate data between ApsaraDB for MongoDB instances created by different Alibaba Cloud accounts](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate data between ApsaraDB for MongoDB instances created by different Alibaba Cloud
         accounts.md).
3.  Add the private IP address of the ECS instance to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

    **Note:** For information about how to obtain the IP address of an ECS instance, see [How do I query IP addresses of ECS instances?](https://www.alibabacloud.com/help/zh/doc-detail/40637.htm#section-vpl-qbg-qgb)


## Method 2: Migrate the ECS instance to the Alibaba Cloud account to which the ApsaraDB for MongoDB instance belongs

This method migrates the ECS instance to the Alibaba Cloud account to which the ApsaraDB for MongoDB instance belongs by sharing the ECS instance as a custom image.

Prerequisites

The ECS instance and ApsaraDB for MongoDB instance are in the same region. Images cannot be shared across regions.

Procedure

1.  [Create a custom image from the ECS instance](~~35109~~).
2.  Share the custom image to the Alibaba Cloud account to which the ApsaraDB for MongoDB instance belongs. For more information, see [Share or unshare custom images](~~25463~~).
3.  [Create an ECS instance from the custom image](~~25465~~).

    **Note:** When you create the ECS instance, select the same VPC as the ApsaraDB for MongoDB instance.

4.  Add the private IP address of the ECS instance to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

    **Note:** For information about how to obtain the IP address of an ECS instance, see [How do I query IP addresses of ECS instances?](https://www.alibabacloud.com/help/zh/doc-detail/40637.htm#section-vpl-qbg-qgb)


## Method 3: Establish a connection between the ECS instance and ApsaraDB for MongoDB instance by using Cloud Enterprise Network

This method uses [Cloud Enterprise Network](~~59870~~) \(CEN\) to establish a connection between the VPCs that belong to different Alibaba Cloud accounts to connect the ECS instance to the ApsaraDB for MongoDB instance.

**Note:** Make sure that the CIDR blocks of the VPCs or vSwitches involved do not conflict with each other.

Procedure

1.  Switch the network type of the ApsaraDB for MongoDB instance to VPC. For more information, see [Switch the network type of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md). If the network type is VPC, skip this step.
2.  Switch the network type of the ECS instance to VPC. For more information, see [Migrate ECS instances](~~57954~~). If the network type is VPC, skip this step.
3.  Based on the running environment, select one of the following CEN-based connections over an internal network. For more information, see
    -   [Connect network instances created in the same region but by different accounts](~~65901~~).
    -   [Connect network instances created by different accounts and in different regions](~~65936~~).
4.  Add the private IP address of the ECS instance to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

    **Note:** For information about how to obtain the IP address of an ECS instance, see [How do I query IP addresses of ECS instances?](https://www.alibabacloud.com/help/zh/doc-detail/40637.htm#section-vpl-qbg-qgb)


