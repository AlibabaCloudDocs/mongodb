# 云数据库MongoDB版-分片集群

本文介绍云数据库MongoDB分片集群实例的监控项及其对应的监控指标。

当您调用云监控的API接口时，需要获取当前云产品的**Namespace**和**Period**，具体取值如下：

-   **Namespace**为**acs\_mongodb**。
-   **Period**默认为60秒，也可以为60的整数倍。

当前云产品的**MetricName**和**Dimensions**的取值如下表所示。

|报警规则中监控项|监控信息中监控指标|单位|MetricName|Dimensions|Statistics|
|--------|---------|--|----------|----------|----------|
|（分片集群）Command操作次数|command|Count/s|ShardingOpCommand|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）Delete操作次数|delete|Count/s|ShardingOpDelete|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）日志磁盘使用量|log\_size|Bytes|ShardingLogDiskAmount|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）内存使用率|mem\_usage|%|ShardingMemoryUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）请求数|num\_requests|Count|ShardingNumberRequests|userId、instanceId、subinstanceId、role|Average|
|（分片集群）IOPS使用率|iops\_usage|%|ShardingIOPSUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）内网入流量|bytes\_in|Bytes|ShardingIntranetIn|userId、instanceId、subinstanceId、role|Average|
|（分片集群）内网出流量|bytes\_out|Bytes|ShardingIntranetOut|userId、instanceId、subinstanceId、role|Average|
|（分片集群）数据占用磁盘空间量|data\_size|Bytes|ShardingDataDiskAmount|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）CPU使用率|cpu\_usage|%|ShardingCPUUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）连接数量|current\_conn|Count|ShardingConnectionAmount|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）连接使用率|conn\_usage|%|ShardingConnectionUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）实例占用磁盘空间量|ins\_size|Bytes|ShardingInstanceDiskAmount|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）磁盘使用率|disk\_usage|%|ShardingDiskUtilization|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）Getmore操作次数|getmore|Count/s|ShardingOpGetmore|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）ShardingOpInsert|insert|Count/s|ShardingOpInsert|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）Query操作次数|query|Count/s|ShardingOpQuery|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）Update操作次数|update|Count/s|ShardingOpUpdate|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）QPS|insert+delete+updte+query+getmore+command|Count/s|ShardingQPS|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|
|（分片集群）复制延迟|repl\_lag|Seconds|ShardingReplicationLag|userId、instanceId、subinstanceId、role|Average、Maximum、Minimum|

