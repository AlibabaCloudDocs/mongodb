# Apply for a public endpoint

This topic describes how to apply for a public endpoint when you want to connect to this instance over the Internet.

The following table describes the connections supported by ApsaraDB for MongoDB.

|Connection type|Description|
|:--------------|:----------|
|Intranet Connection - VPC|-   A VPC is an isolated network with higher security and performance than a classic network.
-   By default, ApsaraDB for MongoDB provides endpoints on a VPC. |
|Intranet Connection - Classic Network|Cloud services on a classic network are not isolated. Unauthorized access can only be blocked by using security groups or whitelists. You can switch the network type to VPC. For more information, see [Switch the network type of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md).|
|Public IP Connection|-   Connecting to a instance over the Internet is risky. Therefore, ApsaraDB for MongoDB does not provide public endpoints.
-   If you want to connect to a MongoDB instance from a device outside Alibaba Cloud \(for example, a local client\), you must apply for a public endpoint. |

## Standalone or Replica Set Instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  In the **Public IP Connection** section, click **Apply for Public Connection String**.

    ![Apply for a public endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9023797951/p37042.png)

7.  In the **Apply for Public Connection String** message that appears, click **OK**.

    **Note:** If you want to connect to a replica set instance by using a public endpoint, you must add the public IP address of your client to a whitelist of this instance. For more information, see [Configure a whitelist for a replica set instance](/intl.en-US/Quick Start/Configure a Whitelist.md).


After the application is complete, the replica set instance generates new endpoints for both the primary and secondary nodes and the corresponding connection string URI. For more information, see [Overview of replica set instance connections]().

## Sharded Cluster Instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  In the upper-right corner of the **Public IP Connection** section, click **Apply for Public Connection String**.

    ![Apply for a public endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8278317951/p37037.png)

7.  In the dialog box that appears, specify **Node Type** and **Node ID**, and click **OK**.

    ![Select a node type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8278317951/p59647.png)

    |Parameter|Value|Description|
    |:--------|:----|:----------|
    |**Node Type**|**shard**|A shard. Before you apply for a public endpoint for a shard, you must apply for an internal endpoint for it. For more information, see [Apply for a connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Apply for a connection string of a shard or Configserver node.md). If you want to read the oplog data of a shard over the Internet when you perform certain operations such as data synchronization between clusters, you must apply for a public endpoint for the shard. |
    |**cs**|The config server. Before you apply for a public endpoint for the config server, you must apply for an internal endpoint for it. For more information, see [Apply for a connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Apply for a connection string of a shard or Configserver node.md). If you want to read the configuration information of the config server over the Internet when you perform certain operations such as data synchronization between clusters, you must apply for a public endpoint for the config server. |
    |**mongos**|A mongos. This is the default option because your application is connected to a mongos in most cases.|
    |**Node ID**|The ID of the component for which you want to apply for a public endpoint.|None|

    **Note:**

    -   For more information about component types, see [Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md).
    -   To apply for a public endpoint for other mongos, repeat this step. You can only apply for a new public endpoint after the current one is created.

