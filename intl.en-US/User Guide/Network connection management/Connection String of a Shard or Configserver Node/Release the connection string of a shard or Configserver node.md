# Release the connection string of a shard or Configserver node

When you no longer need to connect to a shard or Configserver node, you can release its connection string.

## Precautions

-   The connection string of a Mongos node cannot be released.
-   After the connection string of a shard or Configserver node is released, the connection strings of the primary and secondary nodes are released and you cannot use this connection string to connect to the released node. Proceed with caution.
-   This operation releases the internal connection string of the node. If the node also has a public connection string and the connection string is no longer needed, you can [Release a public connection string](/intl.en-US/User Guide/Network connection management/Public IP Connection/Release a public connection string.md).

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  Find the node and click **Release** in the **Actions** column.

    **Note:** **Shard** indicates a shard node. **CS** indicates a Configserver node.

7.  In the dialog box that appears, click **OK**.

8.  Wait until the instance status changes from **Releasing Network Connection** to **Running**.


