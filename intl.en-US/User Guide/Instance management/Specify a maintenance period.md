# Specify a maintenance period {#task_tng_h4t_j2b .task}

To guarantee stability, Alibaba Cloud maintains ApsaraDB for MongoDB instances at irregular intervals. You can specify a maintenance period in which you allow Alibaba Cloud to maintain your instances. We recommend that instances be maintained during off-peak hours to avoid an impact on business.

Before maintenance, Alibaba Cloud sends an SMS message and an email to the respective phone number and email address that you have specified for your Alibaba Cloud account. Please check in a timely manner.

On the day of maintenance, instances enter the **Instance being maintained** status ahead of the specified maintenance period to guarantee the stability of the maintenance process. You can still connect to instances in this status. In the ApsaraDB for MongoDB console, you cannot change these instances, for example, upgrade or downgrade their configuration or restart them. However, you can manage accounts, manage ApsaraDB for MongoDB instances, or configure IP address whitelists for these instances. You can also use query features, such as performance monitoring, in the console.

During the maintenance period, instances may be disconnected transiently once or twice. You need to ensure that your applications can automatically re-establish a connection. After intermittent disconnection, instances can immediately return to normal.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list). 
2.  In the upper-left corner of the home page, select the region where the target instance is located. 
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances**. 
4.  Locate the target instance and click its instance ID. 
5.  In the Specification Information area, click **Edit** to the right of **Maintenance Period**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15432/15561688396827_en-US.png)

6.  Specify a maintenance period for the instance and click **OK**. 

