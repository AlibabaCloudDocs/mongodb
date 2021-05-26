# 云数据库MongoDB版-单节点实例

通过本文您可以了解云数据库MongoDB版的单节点实例的监控项。

当您调用云监控的API接口时，需要获取当前云产品的**Namespace**和**Period**，具体取值如下：

-   **Namespace**为**acs\_mongodb**。
-   **Period**默认为60秒，也可以为60的整数倍。

当前云产品的**MetricName**和**Dimensions**的取值如下表所示。

|监控项|单位|MetricName|Dimensions|Statistics|
|---|--|----------|----------|----------|
|（单节点）磁盘使用率|%|SingleNodeDiskUtilization|userId、instanceId|Average、Maximum、Minimum|
|（单节点）网络入流量|Bytes|SingleNodeIntranetIn|userId、instanceId|Average、Maximum、Minimum|
|（单节点）网络出流量|Bytes|SingleNodeIntranetOut|userId、instanceId|Average、Maximum、Minimum|
|（单节点）内存使用率|%|SingleNodeMemoryUtilization|userId、instanceId|Average、Maximum、Minimum|
|（单节点）请求数|Count|SingleNodeNumberRequests|userId、instanceId|Average、Maximum、Minimum|
|（单节点）CPU使用率|%|SingleNodeCPUUtilization|userId、instanceId|Average、Maximum、Minimum|
|（单节点）连接数使用量|Count|SingleNodeConnectionAmount|userId、instanceId|Average、Maximum、Minimum|
|（单节点）连接数使用率|%|SingleNodeConnectionUtilization|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Command操作次数|Count|SingleNodeOpCommand|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Delete操作次数|Count|SingleNodeOpDelete|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Getmore操作次数|Count|SingleNodeOpGetmore|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Insert操作次数|Count|SingleNodeOpInsert|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Query操作次数|Count|SingleNodeOpQuery|userId、instanceId|Average、Maximum、Minimum|
|（单节点）Update操作次数|Count|SingleNodeOpUpdate|userId、instanceId|Average、Maximum、Minimum|
|（单节点）QPS|Count|SingleNodeQPS|userId、instanceId|Average、Maximum、Minimum|
|（单节点）数据占用磁盘空间量|Bytes|SingleNodeDateDiskAmount|userId、instanceId|Average、Maximum、Minimum|

