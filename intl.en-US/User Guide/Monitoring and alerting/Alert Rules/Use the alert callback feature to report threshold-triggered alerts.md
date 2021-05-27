# Use the alert callback feature to report threshold-triggered alerts

CloudMonitor can report alerts by using emails and DingTalk chatbots. CloudMonitor can also report alerts by using the alert callback feature. This allows to you to handle alerts in a more flexible way. This topic describes how to use the alert callback feature to send notifications about threshold-triggered alerts to your existing operations and maintenance \(O&M\) or notification system.

The callback URL that can be accessed over the Internet is prepared. Use the URL of the O&M or notification system as the callback URL.

CloudMonitor pushes alert notifications to the specified URL by sending HTTP POST requests. You must add the following IP addresses to the whitelist of your firewall: 47.74.206.0/26, 47.74.206.64/26, 47.74.206.128/26, and 47.74.206.192/26. You can take actions based on the received notifications.

If an alert callback fails, three retries are performed. Each callback request times out after 5 seconds.

1.  Log on to the [CloudMonitor console](https://cms-intl.console.aliyun.com).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Rules**.

3.  On the **Threshold Value Alert** tab of the Alert Rules page, find the threshold-triggered alert rule that you want to modify and click **Modify** in the **Actions** column.

    **Note:** You can also create a threshold-triggered alert rule. For more information, see [Create a threshold-triggered alert rule](/intl.en-US/Alarm service/Alarm rules/Create a threshold-triggered alert rule.md).

4.  On the Create Alert Rule page, enter the callback URL.

5.  Click **Confirm**.


If an alert is triggered based on the alert rule, CloudMonitor sends an HTTP POST request that contains alert information to the callback URL. The following table describes the parameters of the HTTP POST request.

|Parameter|Type|Description|
|---------|----|-----------|
|alertName|String|The name of the alert.|
|alertState|String|The status of the alert. Valid values: -   OK: The alert rule has no active alert.
-   ALERT: Alerts are triggered based on the alert rule.
-   INSUFFICIENT\_DATA: The alert rule has no data. |
|curValue|String|The value of the metric when the alert was triggered or cleared.|
|dimensions|String|The object for which the alert was triggered. Example: `{userId=12****, instanceId=i-12****}`.|
|expression|String|The conditions that triggered the alert.|
|instanceName|String|The name of the instance.|
|metricName|String|The name of the metric. For more information about metric names, see [Appendix 1: Metrics](/intl.en-US/Appendix 1: Metrics/Overview.md).|
|metricProject|String|The name of the service. The value of this parameter is the same as that of the namespace parameter. For more information about service names, see [Appendix 1: Metrics](/intl.en-US/Appendix 1: Metrics/Overview.md).|
|namespace|String|The namespace of the service. The value of this parameter is the same as that of the metricProject parameter. For more information about the namespaces of services, see [Appendix 1: Metrics](/intl.en-US/Appendix 1: Metrics/Overview.md).|
|preTriggerLevel|String|The level of the alert that was triggered last time. Valid values:-   CRITICAL
-   WARN
-   INFO |
|ruleId|String|The ID of the alert rule based on which the alert was triggered.|
|timestamp|String|The timestamp when the alert was triggered.|
|triggerLevel|String|The level of the alert that was triggered this time. Valid values:-   CRITICAL
-   WARN
-   INFO |
|userId|String|The ID of the user.|

Sample HTTP POST request:

```
Content-Type: application/x-www-form-urlencoded; charset=UTF-8

expression=$Average>=95&metricName=Host.mem.usedutilization&instanceName=instance-name-****&signature=eEq1zHuCUp0XSmLD8p8VtTKF****&metricProject=acs_ecs&userId=12****&curValue=97.39&alertName=Basic monitoring-ECS-memory usage&namespace=acs_ecs&triggerLevel=WARN&alertState=ALERT&preTriggerLevel=WARN&ruleId=applyTemplateee147e59-664f-4033-a1be-e9595746****&dimensions={userId=12****), instanceId=i-12****}&timestamp=1508136760
```

