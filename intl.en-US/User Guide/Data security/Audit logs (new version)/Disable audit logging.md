# Disable audit logging

This topic describes how to disable audit logging for an ApsaraDB for MongoDB instance.

ApsaraDB for MongoDB does not support disabling the audit log feature. To reduce the number of audit logs and save storage space, you can disable audit logging for specific operation types.

## Impacts

If you disable audit logging for a specific operation type, the system ignores the operation type in future auditing. However, the audit logs generated before you modify the settings are retained. You can use the audit logs for backtracking. For more information, see [Query audit logs](/intl.en-US/User Guide/Data security/Audit logs (new version)/Query audit logs.md).

## Disable audit logging

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane of the **Instance** page, choose **Data Security** \> **Audit Logs**.

6.  In the upper-left corner of the page, click **Audit Log Filter Setting**.

7.  In the **Audit Log Filter Setting** dialog box, clear the target operation types, and click **Submit**.

    **Note:** We recommend that you select `admin` and `slow`. The log size of the two operation types is small. You can use these audit logs for troubleshooting. For more information, see [Operation types](/intl.en-US/User Guide/Data security/Audit logs (new version)/Modify audit settings.md).


**Related topics**  


[Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md)

[Overview](/intl.en-US/User Guide/Log management/Overview.md)

[Slow query logs](/intl.en-US/User Guide/CloudDBA/Slow query logs.md)

