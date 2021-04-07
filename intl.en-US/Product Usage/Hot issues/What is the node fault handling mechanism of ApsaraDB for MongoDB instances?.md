# What is the node fault handling mechanism of ApsaraDB for MongoDB instances?

This topic describes the node fault handling mechanism of ApsaraDB for MongoDB instances.

## Standalone instances

A standalone instance has only one node. If the node is faulty, the system troubleshoots the node. The relevant services become unavailable during troubleshooting.

**Note:** Standalone instances are applicable to test, training, and non-core business scenarios. If your application is in a production environment, we recommend that you use replica set or sharded cluster instances to ensure high availability \(HA\).

## Replica set instances

![](../images/p39716.png "Architecture of replica set instances")

A replica set instance provides multiple nodes. If one of the nodes is faulty, the system switches over to the secondary or hidden node without interruption and then troubleshoots the faulty node. The entire process is transparent to you. A transient connection error of less than 30 seconds may occur during the process. We recommend that you configure your application to automatically reconnect to the replica set instance after a transient connection error occurs.

**Note:** If your application is in a production environment, we recommend that you do not use the connection string of the primary node but use a connection string URI to connect your application to a replica set instance. When you use the connection string URI, the read/write operations of your application remain available even if a node of the instance is faulty. For more information, see [Overview of replica set instance connections]().

## Sharded cluster instances

![](../images/p39656.png "Architecture of sharded cluster instances")

In a sharded cluster instance, both the shard and Configserver nodes use three-node replica set architecture. When a node is faulty, the system switches over to the hidden node without interruption and then troubleshoots the faulty node. The entire process is transparent to you. A transient connection error of less than 30 seconds may occur during the process. We recommend that you configure your application to automatically reconnect to the sharded cluster instance after a transient connection error occurs.

**Note:**

-   A mongos node uses a single-node architecture. If a mongos node is faulty, the relevant services become unavailable.
-   If your application is in a production environment, we recommend that you do not use the connection string of a mongos node but use a connection string URI to connect your application to a sharded cluster instance. When you use the connection string URI, your client automatically redirects requests to the mongos node in the normal status if the connected mongos node is faulty. For more information, see [Overview of sharded cluster instance connections]().

