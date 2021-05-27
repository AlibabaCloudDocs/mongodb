# ApsaraDB for MongoDB-Instance Copy

This topic describes the metrics for ApsaraDB for MongoDB of the replica set architecture.

When you call an API operation provided by Cloud Monitor, you may need to set the **Namespace** and **Period** parameters. Set the parameters for the current service in the following way:

-   Set the **Namespace** parameter to **acs\_mongodb**.
-   Set the **Period** parameter to an integral multiple of 60s. The default value is 60s.

The following table describes the valid values of the **MetricName** and **Dimensions** parameters for the current service.

|Metric|Unit|MetricName|Dimensions|Statistics|
|------|----|----------|----------|----------|
|\(Host&Slave\) CPU Usage|%|CPUUtilization|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Connection Usage|count|ConnectionAmount|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Connection Usage|%|ConnectionUtilization|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Disk Size Occupied by Data|byte|DataDiskAmount|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Disk Usage|%|DiskUtilization|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) IOPS Usage|%|IOPSUtilization|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Disk Size Occupied by Instances|byte|InstanceDiskAmount|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Cache Inbound Bandwidth|byte|IntranetIn|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Cache Outbound Bandwidth|byte|IntranetOut|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Disk Size Occupied by Logs|byte|LogDiskAmount|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Memory Usage|%|MemoryUtilization|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Number of Requests|count|NumberRequests|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Number of Command Operations|frequency|OpCommand|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Number of Delete Operations|frequency|OpDelete|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Number of Getmore Operations|frequency|OpGetmore|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Number of Insert Operations|count|OpInsert|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Number of Query Operations|frequency|OpQuery|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) Number of Update Operations|frequency|OpUpdate|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) QPS|count|QPS|userId, instanceId, and role|Maximum, Minimum, and Average|
|\(Host&Slave\) ReplicationLag|s|ReplicationLag|userId, instanceId, and role|Maximum, Minimum, and Average|

