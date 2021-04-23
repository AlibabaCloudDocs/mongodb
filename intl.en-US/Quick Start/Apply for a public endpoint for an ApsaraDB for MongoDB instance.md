---
keyword: [enable remote connection for ApsaraDB for MongoDB instances, connect to ApsaraDB for MongoDB instances over the Internet]
---

# Apply for a public endpoint for an ApsaraDB for MongoDB instance

This topic describes how to apply for a public endpoint for an ApsaraDB for MongoDB instance so that you can connect to the instance over the Internet.

The following table describes the endpoint types supported by an ApsaraDB for MongoDB instance.

|Endpoint type|Description|
|:------------|:----------|
|VPC endpoint|-   A VPC is an isolated network with higher security and performance than the classic network.
-   By default, ApsaraDB for MongoDB provides endpoints on a VPC. |
|Classic network endpoint|Cloud services on the classic network are not isolated. Unauthorized access can be blocked only by using security groups or whitelists. You can switch the network type to VPC. For more information, see [Switch the network type of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md).**Note:** Standalone instances cannot be connected over the classic network. |
|Public endpoint|-   It is risky to connect to an ApsaraDB for MongoDB instance over the Internet. Therefore, ApsaraDB for MongoDB does not provide public endpoints.
-   If you want to connect to an ApsaraDB for MongoDB instance from a device outside Alibaba Cloud such as an on-premises client, you must apply for a public endpoint. |

## Apply for a public endpoint for a standalone or replica setinstance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connections**.

6.  In the **Public Connections** section, click **Apply for Public Connection String**.

    ![Apply for a public endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0910008061/p88063.png)

7.  In the **Apply for Public Connection String** message, click **OK**.

    **Note:** If you want to connect to an ApsaraDB for MongoDB instance by using a public endpoint, you must add the public IP address of your client to a whitelist of this instance. For more information, see [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md).


## Apply for a public endpoint for a sharded cluster instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connections**.

6.  In the **Public Connections** section, click **Apply for Public Connection String**.

    ![Apply for a public endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8278317951/p37037.png)

7.  In the dialog box that appears, specify **Node Type** and **Node ID**, and click **OK**.

    ![Select a node type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8278317951/p59647.png)

    |Parameter|Value|Description|
    |:--------|:----|:----------|
    |**Node Type**|**Shard**|A shard. Before you apply for a public endpoint for a shard, you must apply for an internal endpoint for it. For more information, see [Apply for a connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Apply for a connection string of a shard or Configserver node.md). If you want to read the oplog data of a shard over the Internet when you perform specific operations such as data synchronization between clusters, you must apply for a public endpoint for the shard. |
    |**CS**|A config server. Before you apply for a public endpoint for a config server, you must apply for an internal endpoint for it. For more information, see [Apply for a connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Apply for a connection string of a shard or Configserver node.md). If you want to read the configuration information of a config server over the Internet when you perform specific operations such as data synchronization between clusters, you must apply for a public endpoint for the config server. |
    |**Mongos**|A mongos. This is the default option because your application is connected to a mongos in most cases.|
    |**Node ID**|The ID of the current instance node|The ID of the node for which you want to apply for a public endpoint|

    **Note:**

    -   For more information about node types, see [Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md).
    -   To apply for public endpoints for multiple nodes, repeat this operation. You can apply for a new public endpoint only after the current one is created.

## Results

After the application is complete, the available public endpoints are displayed in the **Public Connections** section. For more information about endpoints, see [Overview of replica set instance connections]().

## References

-   [Connect to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance over the Internet.md).
-   To ensure data security, we recommend that you release a public endpoint if you no longer need it. For more information, see [Release a public endpoint](/intl.en-US/User Guide/Network connection management/Public IP Connection/Release a public endpoint.md).

