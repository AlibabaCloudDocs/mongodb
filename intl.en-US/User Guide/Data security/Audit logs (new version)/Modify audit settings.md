# Modify audit settings

This topic describes how to modify the operation types to be collected in the audit logs by modifying **Audit Log Filter Setting**.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane of the **Instance** page, choose **Data Security** \> **Audit Logs**.

6.  In the upper-left corner of the page, click **Audit Log Filter Setting**.

7.  In the **Audit Log Filter Setting** dialog box, select the operation types that you want to audit, and click **Submit**.

    **Note:** The following list describes the operation types:

    -   admin: O&M operations
    -   slow: slow queries
    -   query: queries
    -   insert: data insertion
    -   update: data updates
    -   delete: data deletion
    -   command: protocol commands, such as the aggregate method

**Related topics**  


[Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md)

[Overview](/intl.en-US/User Guide/Log management/Overview.md)

[Slow query logs](/intl.en-US/User Guide/CloudDBA/Slow query logs.md)

