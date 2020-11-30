# Notice on changing the monitoring data collection interval to 60 seconds as November 19, 2020

As of November 19, 2020, the collection interval of ApsaraDB for MongoDB monitoring data changes to 60 seconds.

## Background information

A collection interval indicates how often the system automatically collects resource information. In earlier versions, ApsaraDB for MongoDB supports collection intervals of 5 seconds and 300 seconds. The 5-second interval is too high a frequency and the 300-second interval is too low a frequency. Both cannot meet customer requirements. To solve this problem, Alibaba Cloud changes the collection interval of ApsaraDB for MongoDB monitoring data to 60 seconds. This allows you to find problems such as resource exceptions and fix them in a timely manner.

## Effective date

November 19, 2020

## Changes

-   The collection interval of 60 seconds becomes available.
-   The feature of adjusting collection intervals becomes unavailable.
-   The collection intervals of 5 seconds and 300 seconds become unavailable.

## Effects

|Instance|Effect|
|--------|------|
|Existing instance|-   The collection interval cannot be adjusted.
-   The collection interval is set to 60 seconds. |
|New instance|The collection interval is set to 60 seconds and cannot be adjusted.|

We apologize for the inconvenience. If you have any questions, [submit a ticket](https://selfservice.console.aliyun.com/ticket/category/dds/today) to contact after-sales support engineers.

**Related topics**  


[View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md)

