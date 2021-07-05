# Notice on updating the audit log feature on June 6

The audit log feature of ApsaraDB for MongoDB is updated. To view the slow query logs of ApsaraDB for MongoDB instances that are purchased after June 6, 2021, you must enable the audit log feature, click **Audit Log Filter Setting**, and then select the operation types. You must select both the **admin** and **slow** operation types.

## Update Date

June 6, 2021

## Impact

To view the slow query logs of ApsaraDB for MongoDB instances that are purchased after June 6, 2021, you must enable the audit log feature, and then select the operations types by clicking **Audit Log Filter Setting**. You must select both the **admin** and **slow** operation types.

## Procedure

To view the slow query logs of ApsaraDB for MongoDB instances that are purchased after June 6, 2021, perform the following steps:

1.  Enable the audit log feature. For more information, see [Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md).
2.  Set the operation types that you want to audit. You must select both the **admin** and **slow** operation types. For more information, see [Modify audit settings](/intl.en-US/User Guide/Data security/Audit logs (new version)/Modify audit settings.md).
3.  View the slow query logs of instances. For more information, see [Slow query logs](/intl.en-US/User Guide/CloudDBA for performance diagnostics and optimization/Slow query logs.md).

