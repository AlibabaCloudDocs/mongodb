# Configure alert rules

ApsaraDB for MongoDB provides the instance status monitoring and alerting feature. You can configure alert rules for important metrics to help detect abnormal data in a timely manner and quickly identify and troubleshoot faults.

## Procedure

1.  Log on to the [Cloud Monitor console](https://cms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Alerts** \> **Alert Rules**.
3.  On the **Alert Rules** page, click the **Threshold Value Alert** tab.
4.  Click **Create Alert Rule**.
5.  On the **Create Alert Rule** page, configure the parameters for an alert rule.
    -   Related Resource

        |Parameter|Description|
        |---------|-----------|
        |Product|The architecture type of the instance. Valid values:         -   ApsaraDB for MongoDB-Instance Copy
        -   ApsaraDB for MongoDB-Cluster Instance
        -   ApsaraDB for MongoDB-Single Node Instance
**Note:** If you select **ApsaraDB for MongoDB-Cluster Instance**, you must specify the **mongos** and **shard** nodes that you want to monitor. |
        |Resource Range|        -   **All Resources**: The alert rule is applicable to all resources of the specified service.
        -   **Instances**: The alert rule is applicable to the specified ApsaraDB for MongoDB instances. |

    -   Set Alert Rules

        For information about parameters, see [Manage alert rules](/intl.en-US/Alarm service/Alarm rules/Manage alert rules.md).

    -   Notification Mode

        For information about parameters, see [Manage alert rules](/intl.en-US/Alarm service/Alarm rules/Manage alert rules.md).

        **Note:** Before you configure an alert rule, you must create an alert contact or contact group in the Cloud Monitor console. For more information, see [Create an alert contact or alert group](/intl.en-US/Alarm service/Alert contacts/Create an alert contact or alert group.md).

6.  Click **Confirm**. The alert rule automatically takes effect.

## References

For more information about the metrics, see the following topics:

-   [ApsaraDB for MongoDB-Single Node Instance](/intl.en-US/Appendix 1: Metrics/Databases/NoSQL databases/ApsaraDB for MongoDB-Single Node Instance.md)
-   [ApsaraDB for MongoDB-Instance Copy](/intl.en-US/Appendix 1: Metrics/Databases/NoSQL databases/ApsaraDB for MongoDB-Instance Copy.md)
-   [ApsaraDB for MongoDB-Cluster Instance](/intl.en-US/Appendix 1: Metrics/Databases/NoSQL databases/ApsaraDB for MongoDB-Cluster Instance.md)

