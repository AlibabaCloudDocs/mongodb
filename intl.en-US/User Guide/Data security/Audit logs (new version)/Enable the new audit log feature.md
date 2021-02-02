# Enable the new audit log feature

The new audit log feature integrates the features of Log Service with ApsaraDB for MongoDB. The audit log feature allows you to filter log data, analyze logs online, and export logs. This helps you discover security and performance issues of your ApsaraDB for MongoDB instances at the earliest opportunity.

If you want to enable the new audit log feature as a RAM user, the RAM user must be granted the AliyunLogFullAccess permissions. For more information, see [Grant permissions](~~121945~~).

Alibaba Cloud Log Service is an all-in-one service and has been used in big data analytics scenarios. Log Service allows you to collect, consume, ship, search, and analyze log data without the need for extra code resources. This service greatly improves O&M efficiency. ApsaraDB for MongoDB integrates the features of Log Service to provide the new audit log feature, which is characterized by stability, ease of use, flexibility, and high efficiency.

This topic describes how to enable the new audit log feature.

## Notes

After you enable the new audit log feature, Log Service records operations on ApsaraDB for MongoDB instances in logs to facilitate troubleshooting.

## Billing

The trial edition has been available. The official edition will be available at a later date.

**Note:** In the trial edition, audit logs can be stored for one day with a maximum storage capacity of 100 GB.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Audit Logs**.

6.  Click **Enable Audit Logs**.

    ![Enable Audit Logs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3245298951/p102028.png)

7.  Click **OK**.


-   [Query audit logs](/intl.en-US/User Guide/Data security/Audit logs (new version)/Query audit logs.md)
-   [Download audit logs](/intl.en-US/User Guide/Data security/Audit logs (new version)/Download audit logs.md)
-   [Modify audit settings](/intl.en-US/User Guide/Data security/Audit logs (new version)/Modify audit settings.md)
-   [Subscribe to audit log reports](/intl.en-US/User Guide/Data security/Audit logs (new version)/Subscribe to audit log reports.md)
-   [Disable audit logging](/intl.en-US/User Guide/Data security/Audit logs (new version)/Disable audit logging.md)

**Related topics**  


[Overview](/intl.en-US/User Guide/Log management/Overview.md)

[Slow query logs](/intl.en-US/User Guide/CloudDBA/Slow query logs.md)

