---
keyword: mongodb shard address apply for a connection string of nodes
---

# Apply for a connection string of a shard or Configserver node

A sharded cluster instance consists of Mongos, shard, and Configserver nodes. Typically, you need only to connect to the Mongos node to read and write data. In some special scenarios such as data synchronization between clusters, you must read the oplog of a shard node or the configuration information of a Configserver node. You can apply for a connection string of the corresponding node.

Sharded cluster instances must be used.

## Usage notes

-   After you apply for a connection string, two connection strings are allocated to each node, one for the primary node and one for the secondary node.
-   The network type of the connection strings must be the same as that of the current Mongos node.
-   You cannot modify the connection string of a shard or Configserver node.
-   The connection strings allocated here can only be used to access the node over the internal network. If you want to access the node over the Internet, you can apply for a public endpoint for a sharded cluster instance. For more information, see [Apply for a public endpoint for a sharded cluster instance]().

## Introduction to the sharded cluster architecture and nodes

For more information, see [Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md).

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  In the upper-right corner, choose **More** \> **Apply for Shard or ConfigServer Connection String**.

7.  In the dialog box that appears, apply for a connection string for the shard or Configserver node.

    ![Apply for a connection string](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9935298951/p58471.png)

    |Parameter|Description|
    |---------|-----------|
    |**Node Type**|    -   **Shard**: the shard node.
    -   **CS**: the Configserver node. |
    |**Select Node ID**|Select a check box corresponding to the ID of the node for which you want to create a connection string.|
    |**Account**|The account name must be 4 to 16 characters in length and can contain lowercase letters, digits, and underscores \(\_\). It must start with a lowercase letter. **Note:**

    -   You must set the account and password only when you apply for the connection string of a shard or Configserver node for the first time. The account and password are required for all shard and Configserver nodes.
    -   The permissions of this account are fixed to read-only. |
    |**Password**|    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include

! \#$%^&\*\(\)\_+-=

    -   The password must be 8 to 32 characters in length.
**Note:** If you forget your password, you can reset the password. For more information, see [Reset the password for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Account management/Reset the password for an ApsaraDB for MongoDB instance.md). |
    |**Confirm Password**|Enter the account password again.|

8.  Click **Submit**.

9.  Wait until the instance status changes from **Creating Connection** to **Running**.


## Node types

After you apply for the connection string of a shard or Configserver node, you can view the connection string on the **Database Connection** page. The following table describes node types.

|Node type|Description|
|---------|-----------|
|**Shard**|The shard node.|
|**CS**|The Configserver node.|
|**Mongos**|The mongos node.|

## References

If the connection string of a shard or Configserver node is no longer needed, you can [Release the connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Release the connection string of a shard or Configserver node.md).

