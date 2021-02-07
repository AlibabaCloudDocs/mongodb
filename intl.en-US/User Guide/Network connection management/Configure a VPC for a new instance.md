# Configure a VPC for a new instance

ApsaraDB for MongoDB supports two network types: classic network and VPC. This topic describes how to configure a VPC for a new ApsaraDB for MongoDB instance.

On the Apsara Stack, a classic network and a VPC network have the following differences:

-   On the classic network, cloud services are not isolated. You can configure a security group or whitelist policy for cloud services to block unauthorized access.
-   A VPC allows you to build an isolated network environment in Alibaba Cloud, where you can customize its route table, IP address range, and gateway. You can also use a physical connection or VPN to combine your self-managed data center with cloud resources in Alibaba Cloud VPC to create a virtual data center, so that you can migrate your applications to the cloud.

VPC is select for ApsaraDB for MongoDB by default. Then, you must create an ApsaraDB for MongoDB instance and a VPC in the same region in the following ways:

-   If you have not created an ApsaraDB for MongoDB instance, you can create a VPC first and create an ApsaraDB for MongoDB instance in the VPC by using the method described in this topic.
-   If you have created an ApsaraDB for MongoDB instance, you can create a VPC in the same region and add the ApsaraDB for MongoDB instance to the VPC. For more information, see [Switch the network type of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md).

1.  Create a VPC. For more information, see [Create a VPC](/intl.en-US/VPCs and VSwitches/VPC management/Create a VPC.md).

2.  Create an ApsaraDB for MongoDB instance in the same region as the VPC.

3.  Set Network Type to **VPC** after you click Create Instance.

4.  Specify **VPC** and **vSwitch** after you select **VPC**, as shown in the following figure.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7045298951/p21127.png)

5.  Configure other parameters on the page. For more information, see

    -   [Create a standalone instance](/intl.en-US/Quick Start/Create an instance/Create a standalone instance.md)
    -   [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md)
    -   [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md)

