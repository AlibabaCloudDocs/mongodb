# ApsaraDB for MongoDB-Single Node Instance

This topic describes the metrics of standalone ApsaraDB for MongoDB instances .

When you call an API operation provided by Cloud Monitor, you may need to set the **Namespace** and **Period** parameters. Set the parameters for the current service in the following way:

-   Set the **Namespace** parameter to **acs\_mongodb**.
-   Set the **Period** parameter to an integral multiple of 60s. The default value is 60s.

The following table describes the valid values of the **MetricName** and **Dimensions** parameters for the current service.

|Metric|Unit|MetricName|Dimensions|Statistics|
|------|----|----------|----------|----------|
|\(Single node\) SingleNodeDiskUtilization|%|SingleNodeDiskUtilization|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeIntranetIn|Bytes|SingleNodeIntranetIn|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeIntranetOut|Bytes|SingleNodeIntranetOut|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeMemoryUtilization|%|SingleNodeMemoryUtilization|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeNumberRequests|Count|SingleNodeNumberRequests|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeCPUUtilization|%|SingleNodeCPUUtilization|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeConnectionAmount|Count|SingleNodeConnectionAmount|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeConnectionUtilization|%|SingleNodeConnectionUtilization|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeOpCommand|Count|SingleNodeOpCommand|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeOpDelete|Count|SingleNodeOpDelete|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeOpGetmore|Count|SingleNodeOpGetmore|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeOpInsert|Count|SingleNodeOpInsert|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeOpQuery|Count|SingleNodeOpQuery|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeOpUpdate|Count|SingleNodeOpUpdate|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeQPS|Count|SingleNodeQPS|userId and instanceId|Average, Maximum, and Minimum|
|\(Single node\) SingleNodeDataDiskAmount|Bytes|SingleNodeDateDiskAmount|userId and instanceId|Average, Maximum, and Minimum|

