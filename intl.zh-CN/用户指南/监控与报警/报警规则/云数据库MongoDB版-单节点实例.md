# 云数据库MongoDB版-单节点实例

本文介绍云数据库MongoDB的单节点实例的监控项及其对应监控指标。

当您调用云监控的API接口时，需要获取当前云产品的**Namespace**和**Period**，具体取值如下：

-   **Namespace**为**acs\_mongodb**。
-   **Period**默认为60秒，也可以为60的整数倍。

当前云产品的**MetricName**和**Dimensions**的取值如下表所示。

|报警规则中监控项|监控信息中监控指标|单位|MetricName|Dimensions|Statistics|
|--------|---------|--|----------|----------|----------|
|（单节点）磁盘使用率|disk\_usage|%|SingleNodeDiskUtilization|userId、instanceId|Average、Maximum、Minimum|
|（单节点）网络入流量|bytes\_in|Bytes|SingleNodeIntranetIn|userId、instanceId|Average、Maximum、Minimum|
|（单节点）网络出流量|bytes\_out|Bytes|SingleNodeIntranetOut|userId、instanceId|Average、Maximum、Minimum|
|（单节点）内存使用率|mem\_usage|%|SingleNodeMemoryUtilization|userId、instanceId|Average、Maximum、Minimum|
|（单节点）请求数|num\_requests|Count|SingleNodeNumberRequests|userId、instanceId|Average、Maximum、Minimum|
|（单节点）CPU使用率|cpu\_usage|%|SingleNodeCPUUtilization|userId、instanceId|Average、Maximum、Minimum|
|（单节点）连接数使用量|current\_conn|Count|SingleNodeConnectionAmount|userId、instanceId|Average、Maximum、Minimum|
|（单节点）连接数使用率|conn\_usage|%|SingleNodeConnectionUtilization|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Command操作次数|command|Count/s|SingleNodeOpCommand|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Delete操作次数|delete|Count/s|SingleNodeOpDelete|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Getmore操作次数|getmore|Count/s|SingleNodeOpGetmore|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Insert操作次数|insert|Count/s|SingleNodeOpInsert|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Query操作次数|query|Count/s|SingleNodeOpQuery|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Update操作次数|update|Count/s|SingleNodeOpUpdate|userId、instanceId|Average、Maximum、Minimum|
|（单节点）QPS|insert+delete+updte+query+getmore+command|Count/s|SingleNodeQPS|userId、instanceId|Average、Maximum、Minimum|
|（单节点）数据占用磁盘空间量|data\_size|Bytes|SingleNodeDateDiskAmount|userId、instanceId|Average、Maximum、Minimum|

