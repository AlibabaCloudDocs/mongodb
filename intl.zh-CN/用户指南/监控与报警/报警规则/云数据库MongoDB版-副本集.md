# 云数据库MongoDB版-副本集

通过本文您可以了解云数据库MongoDB版的副本集的监控项。

当您调用云监控的API接口时，需要获取当前云产品的**Namespace**和**Period**，具体取值如下：

-   **Namespace**为**acs\_mongodb**。
-   **Period**默认为60秒，也可以为60的整数倍。

当前云产品的**MetricName**和**Dimensions**的取值如下表所示。

|监控项|单位|MetricName|Dimensions|Statistics|
|---|--|----------|----------|----------|
|（副本集）CPU使用率|%|CPUUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）连接数使用量|Count|ConnectionAmount|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）连接数使用率|%|ConnectionUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）数据占用磁盘空间量|Byte|DataDiskAmount|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）磁盘使用率|%|DiskUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）IOPS使用率|%|IOPSUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）实例占用磁盘空间量|Byte|InstanceDiskAmount|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）内网网络入流量|Byte|IntranetIn|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）内网网络出流量|Byte|IntranetOut|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）日志占用磁盘空间量|Byte|LogDiskAmount|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）内存使用百分比|%|MemoryUtilization|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）请求数|Count|NumberRequests|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Command操作次数|Frequency|OpCommand|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Delete操作次数|Frequency|OpDelete|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Getmore操作次数|Frequency|OpGetmore|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Insert操作次数|Count|OpInsert|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Query操作次数|Frequency|OpQuery|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）Update操作次数|Frequency|OpUpdate|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）每秒请求数|Count|QPS|userId、instanceId、role|Maximum、Minimum、Average|
|（副本集）复制延迟|Seconds|ReplicationLag|userId、instanceId、role|Maximum、Minimum、Average|

