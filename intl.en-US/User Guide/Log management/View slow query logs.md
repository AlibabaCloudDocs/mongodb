# View slow query logs

You can view the slow query logs of a database in the console and optimize the database accordingly by analyzing slow query logs.

## Prerequisites

A replica set instance with more than three nodes or a sharded cluster instance is used.

## Precautions

The retention period for slow logs is 72 hours.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Logs** \> **Slow Query Logs**.

6.  View slow query logs based on instance types:

    -   Replica set instances: You can select the database name and time range to query the corresponding slow query logs.

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4445298951/p32678.png)

    -   Sharded cluster instances: You can select the database name, shard node ID and time range to view the corresponding slow query logs.

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4445298951/p32679.png)


**Related topics**  


[Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md)

[Overview](/intl.en-US/User Guide/Log management/Overview.md)

[Slow query logs](/intl.en-US/User Guide/CloudDBA/Slow query logs.md)

