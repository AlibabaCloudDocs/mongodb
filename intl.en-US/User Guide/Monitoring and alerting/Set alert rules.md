# Set alert rules

ApsaraDB for MongoDB provides the instance status monitoring and alerting feature. You can set alert rules for important metrics to help detect abnormal data in a timely manner and quickly locate and handle faults.

## Procedure

1.  Log on to the [Cloud Monitor console](https://cloudmonitor.console.aliyun.com/#/cloud/alarmrules/mongodb//-----all-----/).

    **Note:** On this tab, you can view existing alert rules.

2.  On the Alarm Rules tab of the Cloud Monitor console, click **Create Alarm Rule** in the upper-right corner.
3.  On the Create Alarm Rule page, configure related resource parameters.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6345298951/p21142.png)

    |Parameter|Description|
    |:--------|:----------|
    |Product|The architecture of the instance. Valid values:     -   ApsaraDB for MongoDB-Instance Copy
    -   ApsaraDB for MongoDB-Cluster Instance
    -   ApsaraDB for MongoDB-Single Node Instance
**Note:** If you select **ApsaraDB for MongoDB-Cluster Instance**, you must specify the **mongos** and **shard** nodes to be monitored. |
    |Resource Range|    -   **All Resources**: The alert rule is applicable to all ApsaraDB for MongoDB instances.
    -   **Instances**: The alert rule is applicable to the specified ApsaraDB for MongoDB instances. |
    |Region|The region where the instance is deployed.|
    |Instances|The ID of the instance. You can select multiple instance IDs.|

4.  Set alert rules and the notification method. For more information about the parameters, see [Manage alert rules](/intl.en-US/Alarm service/Alarm rules/Manage alarm rules.md).

    **Note:** To create alert contacts in the Cloud Monitor console, see [Create an alert contact or alert group](/intl.en-US/Alarm service/Alert contacts/Create an alert contact or alert group.md).

5.  Click **Confirm**. Alert rules automatically take effect.

For more information about the metrics, see links below:

-   [ApsaraDB for MongoDB-Single Node Instance](/intl.en-US/Appendix 1: Metrics/Databases/NoSQL databases/ApsaraDB for MongoDB-Single Node Instance.md)
-   [ApsaraDB for MongoDB-Instance Copy](/intl.en-US/Appendix 1: Metrics/Databases/NoSQL databases/ApsaraDB for MongoDB-Instance Copy.md)
-   [ApsaraDB for MongoDB-Cluster Instance](/intl.en-US/Appendix 1: Metrics/Databases/NoSQL databases/ApsaraDB for MongoDB-Cluster Instance.md)

