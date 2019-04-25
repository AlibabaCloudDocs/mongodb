# Set alert rules {#concept_fql_tfd_ggb .concept}

ApsaraDB for MongoDB provides an instance status monitoring and alerting feature. You can set alert rules for important metrics to help you detect abnormal data in a timely manner and quickly locate and handle faults.

## Procedure {#section_vlf_vfd_ggb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  Locate the target instance and click its instance ID.
4.  In the left-side navigation pane, click **Alarm Rules**.
5.  Click **Set Alarm Rule** to jump to the CloudMonitor console.
6.  In the upper-right corner of the CloudMonitor console, click **Create Alarm Rule**.
7.  On the Create Alarm Rule page that appears, specify related resources.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6733/155617701121142_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |Products|The architecture of the instance.     -   ApsaraDB for MongoDB-Instance Copy
    -   ApsaraDB for MongoDB-Cluster Instance
    -   ApsaraDB for MongoDB-Single node instance
 **Note:** If you select **ApsaraDB for MongoDB-Cluster Instance**, you need to select the mongos nodes and shards to be monitored for **Mongos** and **Shard**, respectively.

 |
    |Resource Range|     -   If you select **All Resources**, the alerting service sends an alert notification when any ApsaraDB for MongoDB instances match alert rules.
    -   If you select **Instances**, the alerting service sends an alert notification when any selected ApsaraDB for MongoDB instances match alert rules.
 |
    |Region|The region where the instance is located.|
    |Instances|The ID of the instance to be monitored. You can select multiple instance IDs.|

8.  Set alert rules and configure notification methods. For more information about parameters, see [Manage alert rules](https://www.alibabacloud.com/help/doc-detail/28610.htm).

    **Note:** If you have not created alert contacts in CloudMonitor, see [Manage alert contacts and alert contact groups](https://www.alibabacloud.com/help/doc-detail/28609.htm).

9.  Click **Confirm**. Alert rules automatically take effect.

For more information about metrics, see [ApsaraDB for MongoDB in Cloud service monitoring](https://www.alibabacloud.com/help/doc-detail/35259.htm).

