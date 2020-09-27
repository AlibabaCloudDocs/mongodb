# Release a public connection string

To ensure data security, you can release a public connection string that is no longer needed in the console.

## Precautions

-   You can release one or more public connection strings of the Mongos, shard, and Configserver nodes for a sharded cluster instance.
-   After the public connection string is released for an instance or node, you cannot connect to the instance or node through the original public connection string.
-   After the public connection string is released, we recommend that you delete the corresponding public IP address from the whitelist to ensure data security. For more information, see [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist for an ApsaraDB for MongoDB instance.md).

## Standalone and replica set instances

**Note:** After the public connection string of a replica set instance is released, the public connection strings of the primary and secondary nodes are released.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  In the **Public IP Connection** section, click **Release Public Connection String**.

    ![Release a public connection string](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2045298951/p37322.png)

7.  In the dialog box that appears, click **OK**.


## Sharded cluster instances

You can release one or more public connection strings of the Mongos, shard, and Configserver nodes for a sharded cluster instance.

**Note:**

-   For more information about node types, see [Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md).
-   After the public connection string of a shard or Configserver node is released, the public connection strings of the primary and secondary nodes are released.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  In the **Public IP Connection** section, find the Mongos, shard, or Configserver node for which you want to release the public connection string.

7.  In the **Actions** column corresponding to the instance, click **Release**.

    ![Release a public connection string](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2045298951/p13376.png)

    |Node type|Description|
    |---------|-----------|
    |**db**|The shard node.|
    |**cs**|The Configserver node.|
    |**mongos**|The Mongos node.|

    **Note:** You can repeat this step to release the public connection strings of other nodes as needed. To release the public connection string of the next node, you must wait until the public connection string of the current node is released or the status of the current node becomes **Running**.

8.  In the dialog box that appears, click **OK**.


## Serverless instances

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Serverless Instances**

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**。

6.  In the **Public IP Connection** section, click **Release** under the **Actions** column。

    ![释放公网地址](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4516711061/p170497.png)

7.  In the dialog box that appears, click **OK**.


