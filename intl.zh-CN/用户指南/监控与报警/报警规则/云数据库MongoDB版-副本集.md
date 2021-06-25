# 云数据库MongoDB版-副本集

本文介绍云数据库MongoDB副本集实例的监控项及其对应监控指标。

当您调用云监控的API接口时，需要获取当前云产品的**Namespace**和**Period**，具体取值如下：

-   **Namespace**为**acs\_mongodb**。
-   **Period**默认为60秒，也可以为60的整数倍。

当前云产品的**MetricName**和**Dimensions**的取值如下表所示。

|报警规则中监控项|监控信息中监控指标|单位|MetricName|Dimensions|Statistics|
|--------|---------|--|----------|----------|----------|
|（副本集）CPU使用率|cpu\_usage|%|CPUUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）连接数使用量|current\_conn|Count|ConnectionAmount|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）连接数使用率|conn\_usage|%|ConnectionUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）数据占用磁盘空间量|data\_size|Byte|DataDiskAmount|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）磁盘使用率|disk\_usage|%|DiskUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）IOPS使用率|iops\_usage|%|IOPSUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）实例占用磁盘空间量|ins\_size|Byte|InstanceDiskAmount|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）内网网络入流量|bytes\_in|Byte|IntranetIn|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）内网网络出流量|bytes\_out|Byte|IntranetOut|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）日志占用磁盘空间量|log\_size|Byte|LogDiskAmount|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）内存使用百分比|mem\_usage|%|MemoryUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）请求数|num\_requests|Count|NumberRequests|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Command操作次数|command|Count/s|OpCommand|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Delete操作次数|delete|Count/s|OpDelete|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Getmore操作次数|getmore|Count/s|OpGetmore|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Insert操作次数|insert|Count/s|OpInsert|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Query操作次数|query|Count/s|OpQuery|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Update操作次数|update|Count/s|OpUpdate|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）每秒请求数|insert+delete+updte+query+getmore+command|Count/s|QPS|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）复制延迟|repl\_lag|Seconds|ReplicationLag|userId、instanceId、role|Maximum、Minimum、Average|

