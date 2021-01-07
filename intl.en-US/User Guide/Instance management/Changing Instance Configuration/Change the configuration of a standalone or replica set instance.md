# Change the configuration of a standalone or replica set instance

You can change the configuration of a standalone or replica set instance if the configuration is excessive or cannot meet the performance requirements of your application.

## Precautions

-   When you change the configuration, the new storage space must be larger than the storage space occupied by the current instance.
-   If the billing method is subscription, the interval between two configuration downgrades cannot be less than 60 days.
-   When the billing method is subscription, you cannot downgrade the storage space. You can use other methods to reduce the storage space. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).
-   You cannot change the instance type \(such as from a standalone instance to a replica set instance\) or the storage engine. You can use other methods to change these items. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Billing rules

For more information, see [Configuration change fees](/intl.en-US/Purchase Guide/Configuration change fees.md).

## Impacts

-   Changing configurations does not cause data loss.
-   Pre-operations for configuration changes to an instance do not affect the running of the instance. However, when configuration changes are formally executed on the instance, most operations related to databases, accounts, and network cannot be performed. One or two transient disconnections of up to 30 seconds will occur. For more information, see [Select switching time](#section_usx_gsk_d99).
-   The duration of a configuration change depends on various factors such as network conditions, task queues, and data volume. We recommend that you change configurations during off-peak hours and make sure that your applications have automatic reconnection mechanisms.
-   To ensures better performance and stability of the instance, the system will upgrade the minor version to the latest version by default If the minor version of your instance expires or is not included in the maintenance list and the instance is [upgraded](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md), [migrated](/intl.en-US/User Guide/Data migration and synchronization/Overview.md), [changed](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md), [Created from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Created by point-in-time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), or performed [Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md).

## Select switching time

On the [Change Configuration](#step_ouf_3i9_xep), you can specify switching time. The following table describes details about switching time.

|Item|Instance status|Impact|
|----|---------------|------|
|**Switch Within Maintenance Window**|The instance immediately enters the **Changing Configuration** state.|The system performs pre-operations, which do not affect the running of the instance or cause transient disconnections. Configuration changes are formally executed within the maintenance period you set.

For example, if the preset maintenance period is 2:00 to 3:00, configuration changes will be performed during this period. Most operations related to databases, accounts, and network cannot be performed. One or two transient disconnections of up to 30 seconds will occur.

**Note:** For more information about how to modify a maintenance period, see [Specify a maintenance period](/intl.en-US/User Guide/Instance management/Specify a maintenance period.md). |
|**Switch Immediately After Data Migration**|Configuration changes are performed immediately. Most operations related to databases, accounts, and network cannot be performed. One or two transient disconnections of up to 30 seconds will occur. |

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Change the configuration of the instance.

    If the billing method of the instance is pay-as-you-go, perform the following steps:

    1.  Find the instance and click its ID.

    2.  In the **Basic Information** section, click **Change Configuration**.

    If the billing method of the instance is subscription, perform the following steps:

    1.  Find the instance and click its ID.

    2.  In the **Basic Information** section, click **Upgrade** or **Downgrade**.

5.  On the Change Configuration page, specify **Replication Factor**, **Specifications**, **Storage**, and **Migration Time** of the instance.

    For more information about instance specifications, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

    **Note:**

    -   For more information about the limits on parameters, see [Precautions](#section_lqr_nhm_8sg).
    -   For more information about the selection and impacts of **Migration Time**, see [Select switching time](#section_usx_gsk_d99).
6.  Select Terms of Service and make the payment as prompted.


When the instance status changes to **Running**, the configuration has been changed.

