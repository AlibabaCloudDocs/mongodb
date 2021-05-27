# ApsaraDB for MongoDB-Cluster Instance

This topic describes the metrics for ApsaraDB for MongoDB of the sharded cluster architecture.

When you call an API operation provided by Cloud Monitor, you may need to set the **Namespace** and **Period** parameters. Set the parameters for the current service in the following way:

-   Set the **Namespace** parameter to **acs\_mongodb**.
-   Set the **Period** parameter to an integral multiple of 60s. The default value is 60s.

The following table describes the valid values of the **MetricName** and **Dimensions** parameters for the current service.

|Metric|Unit|MetricName|Dimensions|Statistics|
|------|----|----------|----------|----------|
|\(Cluster\) Number of Command Operations|count|ShardingOpCommand|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Number of Delete Operations|count|ShardingOpDelete|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Log Disk Usage|byte|ShardingLogDiskAmount|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Memory Usage|%|ShardingMemoryUtilization|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Number of Requests|count|ShardingNumberRequests|userId, instanceId, subinstanceId, and role|Average|
|\(Cluster\) IOPS Usage|%|ShardingIOPSUtilization|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Intranet Inbound Traffic|byte|ShardingIntranetIn|userId, instanceId, subinstanceId, and role|Average|
|\(Cluster\) Intranet Outbound Traffic|byte|ShardingIntranetOut|userId, instanceId, subinstanceId, and role|Average|
|\(Cluster\) Data Disk Usage|byte|ShardingDataDiskAmount|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) CPU Usage|%|ShardingCPUUtilization|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Total Connections|count|ShardingConnectionAmount|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Connection Usage|%|ShardingConnectionUtilization|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Instance Disk Usage|byte|ShardingInstanceDiskAmount|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Disk Usage|%|ShardingDiskUtilization|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Number of Getmore Operations|count|ShardingOpGetmore|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) ShardingOpInsert|count|ShardingOpInsert|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Number of Query Operations|count|ShardingOpQuery|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) Number of Update operations|count|ShardingOpUpdate|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) QPS|count/s|ShardingQPS|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) ShardingDataDiskAmountOriginal|N/A|ShardingDataDiskAmountOriginal|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|
|\(Cluster\) ShardingReplicationLag|s|ShardingReplicationLag|userId, instanceId, subinstanceId, and role|Average, Maximum, and Minimum|

