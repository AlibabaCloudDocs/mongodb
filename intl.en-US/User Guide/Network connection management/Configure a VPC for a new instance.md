# Configure a VPC for a new instance {#task_ksr_mpp_mfb .task}

ApsaraDB for MongoDB supports two network types: classic network and VPC. This topic describes how to configure a VPC for a new ApsaraDB for MongoDB instance.

On the Alibaba Cloud platform, a classic network and a VPC have the following differences:

-   On the classic network, cloud services are not isolated. You can configure a security group or whitelist policy for them to block unauthorized access.
-   A VPC helps you build an isolated network environment in Alibaba Cloud, where you can customize its routing table, IP address range, and gateway. In addition, you can use a physical connection or VPN to combine your user-created IDC with cloud resources in Alibaba Cloud VPC to create a virtual IDC, so that you can smoothly migrate your applications to the cloud.

ApsaraDB for MongoDB uses VPC by default. To this end, you need to create an ApsaraDB for MongoDB instance and a VPC in the same region as follows:

-   If you have not created an ApsaraDB for MongoDB instance, you can create a VPC first and create an ApsaraDB for MongoDB instance in the VPC following the procedure described in this topic.
-   If you have created an ApsaraDB for MongoDB instance, you can create a VPC in the same region and add the ApsaraDB for MongoDB instance to the VPC. For more information, see [Switch the network type of an instance](intl.en-US/User Guide/Network connection management/Switch the network type of an instance.md#).

1.  Create a VPC. For more information, see [Create a VPC](https://www.alibabacloud.com/help/doc-detail/27710.html).
2.  Create an ApsaraDB for MongoDB instance in the same region as the VPC.
3.  When creating the ApsaraDB for MongoDB instance, select **VPC** as the network type on the instance creation page.
4.  Under **VPC**, select the configured VPC and VSwitch for **VPC** and **VSwitch**, respectively, as shown in the following figure. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6716/155617227921127_en-US.png)

5.  On the instance creation page, specify other configuration items as required. For more information, see the following links. 
    -   [Create a standalone instance](../../../../intl.en-US/Quick Start for Standalone/Create an instance.md#)
    -   [Create a replica set instance](../../../../intl.en-US/Quick Start for Replica Set/Create an instance.md#)
    -   [Create a sharded cluster instance](https://www.alibabacloud.com/help/doc-detail/55137.htm)

