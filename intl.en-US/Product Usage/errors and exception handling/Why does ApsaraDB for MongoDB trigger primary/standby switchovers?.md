# Why does ApsaraDB for MongoDB trigger primary/standby switchovers?

ApsaraDB for MongoDB uses high availability \(HA\) architecture. When an ApsaraDB for MongoDB instance detects that one of its nodes is unavailable, it triggers a primary/standby switchover. It also sends a Short Message Service \(SMS\) message or internal notice to inform you of the switchover.

## Internal notice

\[Alibaba Cloud\] Dear \*\*\*\*\*\*: Your ApsaraDB for MongoDB instance dds-bpxxxxxxxx \(name: xxxxxx\) has an error. A switchover is triggered to ensure stable running of your instance. Please check whether your application is still connected to your instance. We recommend that you configure your application to reconnect to the instance after it is disconnected.

## Why do I receive the internal notice?

ApsaraDB for MongoDB uses HA architecture. A replica set instance of ApsaraDB for MongoDB contains three nodes by default, and a sharded cluster instance of ApsaraDB for MongoDB has each of its shards contain three nodes. Primary and secondary nodes are used for you to connect your application, and hidden nodes are used for primary/standby switchovers, which ensures HA. For more information, see [Architecture of replica set instances](/intl.en-US/Product Introduction/System architecture/Architecture of replica set instances.md) or [Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md).

ApsaraDB for MongoDB supports node health monitoring. When the monitoring results show an unavailable node, a primary/standby switchover is triggered.

## Impact of primary/standby switchovers

-   A primary/standby switchover causes a brief disconnection of less than 30 seconds.
-   If you connect your application to a primary node, the read/write operations of your application are affected as a result of the primary/secondary switchover.

## Suggestions

-   We recommend that you configure your application to reconnect to an ApsaraDB for MongoDB instance after it is disconnected.
-   If your application runs in a production environment, we recommend that you use a connection string URI to connect your application to the instance. In this way, the read/write operations of your application remain available even if a node fails as a result of a primary/secondary switchover. For more information, see [Overview of replica set instance connections]() or [Overview of sharded cluster instance connections]().

