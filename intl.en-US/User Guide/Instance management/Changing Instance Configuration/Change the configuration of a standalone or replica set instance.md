# Change the configuration of a standalone or replica set instance

You can change the configuration of a standalone or replica set instance if the configuration is excessive or cannot meet the performance requirements of your application.

## Precautions

-   When you change the configuration, the new storage space must be larger than the storage space occupied by the current instance.
-   If the billing method is subscription, the interval between two configuration downgrades cannot be less than 60 days.
-   When the billing method is subscription, you cannot downgrade the storage space. You can use other methods to reduce the storage space. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).
-   You cannot change the storage engine or the instance type. For example, you can change a standalone instance to a replica set instance. You can use other methods to change these items. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Billing rules

For more information, see [Configuration change fees](/intl.en-US/Purchase Guide/Configuration change fees.md).

## Impacts

-   Configuration changes do not cause data loss.
-   Pre-operations for configuration changes to an instance do not affect the running of the instance. However, when configuration changes are formally executed on the instance, most operations related to databases, accounts, and network cannot be performed. One or two transient connections of up to 30 seconds may occur. For more information, see [Select the switching time](#section_usx_gsk_d99).
-   The duration of a configuration change depends on multiple factors such as network conditions, task queues, and data volume. We recommend that you change configurations during off-peak hours and make sure that your applications are configured with automatic reconnection policies.

## Select the switching time

On the [Change Configuration](#step_ouf_3i9_xep) page, you can specify the switching time. The following table describes details about switching time.

|Parameter|Instance status|Impact|
|---------|---------------|------|
|**Switch Within Maintenance Window**|The instance immediately changes to the **Changing Configuration** state.|The system performs pre-operations, which do not affect the running of the instance or cause transient connections. Configuration changes are formally executed within the maintenance period you set.

For example, if the preset maintenance period is 2:00 to 3:00, configuration changes are performed during this window. Most operations related to databases, accounts, and network cannot be performed. One or two transient connections of up to 30 seconds may occur.

**Note:** For more information about how to modify a maintenance window, see [Specify a maintenance period](/intl.en-US/User Guide/Instance management/Specify a maintenance period.md). |
|**Switch Immediately After Data Migration**|Configuration changes are immediately performed. Most operations related to databases, accounts, and network cannot be performed. One or two transient connections of up to 30 seconds may occur. |

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Change the configuration of the instance.

    If the billing method of the instance is pay-as-you-go, perform the following operations:

    1.  Find the instance and click its ID.

    2.  In the **Basic Information** section, click **Change Configuration**.

    If the billing method of the instance is subscription, perform the following operations:

    1.  Find the instance and click its ID.

    2.  In the **Basic Information** section, click **Upgrade** or **Downgrade**.

5.  On the Configuration Upgrade page, specify **Replication Factor**, **Plan**, **Storage Space**, and **Switching Time** of the instance.

    For more information about instance specifications, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

    **Note:**

    -   For more information about the limits on the parameters, see [Precautions](#section_lqr_nhm_8sg).
    -   For more information about the selection and impacts of **Switching Time**, see [Select the switching time](#section_usx_gsk_d99).
6.  Read and select ApsaraDB for MongoDB Agreement of Service and complete the payment.


When the instance status changes to **Running**, the configuration is changed.

