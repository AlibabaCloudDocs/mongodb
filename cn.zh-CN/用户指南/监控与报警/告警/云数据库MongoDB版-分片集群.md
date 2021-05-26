# 云数据库MongoDB版-分片集群

通过本文您可以了解云数据库MongoDB版的分片集群的监控项。

当您调用云监控的API接口时，需要获取当前云产品的**Namespace**和**Period**，具体取值如下：

-   **Namespace**为**acs\_mongodb**。
-   **Period**默认为60秒，也可以为60的整数倍。

当前云产品的**MetricName**和**Dimensions**的取值如下表所示。

|监控项|单位|MetricName|Dimensions|Statistics|
|---|--|----------|----------|----------|
|（分片集群）Command操作次数|Count|ShardingOpCommand|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）Delete操作次数|Count|ShardingOpDelete|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）日志磁盘使用量|Bytes|ShardingLogDiskAmount|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）内存使用率|%|ShardingMemoryUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）请求数|Count|ShardingNumberRequests|userId、instanceId、subinstanceId、role|Average|
|（分片集群）IOPS使用率|%|ShardingIOPSUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）内网入流量|Bytes|ShardingIntranetIn|userId、instanceId、subinstanceId、role|Average|
|（分片集群）内网出流量|Bytes|ShardingIntranetOut|userId、instanceId、subinstanceId、role|Average|
|（分片集群）数据占用磁盘空间量|Bytes|ShardingDataDiskAmount|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）CPU使用率|%|ShardingCPUUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）连接数量|Count|ShardingConnectionAmount|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）连接使用率|%|ShardingConnectionUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）实例占用磁盘空间量|Bytes|ShardingInstanceDiskAmount|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）磁盘使用率|%|ShardingDiskUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）Getmore操作次数|Count|ShardingOpGetmore|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）ShardingOpInsert|Count|ShardingOpInsert|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）Query操作次数|Count|ShardingOpQuery|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）Update操作次数|Count|ShardingOpUpdate|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）QPS|Count/s|ShardingQPS|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）ShardingDataDiskAmountOriginal|无|ShardingDataDiskAmountOriginal|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）复制延迟|Seconds|ShardingReplicationLag|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|

