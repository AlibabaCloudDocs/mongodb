# View error logs

You can query the error logs of an instance in the console.

## Prerequisites

A replica set instance with more than three nodes or a sharded cluster instance is created.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Logs** \> **Error Logs**.

6.  Perform the following operations based on instance types:

    -   Replica set instances: You can select the node role and time range to query the corresponding error logs.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5445298951/p32718.png)

    -   Sharded cluster instances: You can query error logs of Mongos or shard nodes.

        **Note:** Mongos nodes have IDs prefixed with `s-`. Shard nodes have IDs prefixed with `d-`.

        -   Query the error logs of a Mongos node.

            You can select the Mongos node ID and time range to query the error logs.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5445298951/p32719.png)

        -   Query the error logs of a shard node.

            You can select the shard node ID, role, and time range to query the error logs.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5445298951/p32720.png)


**Related topics**  


[Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md)

[Overview](/intl.en-US/User Guide/Log management/Overview.md)

[Slow query logs](/intl.en-US/User Guide/CloudDBA/Slow query logs.md)

