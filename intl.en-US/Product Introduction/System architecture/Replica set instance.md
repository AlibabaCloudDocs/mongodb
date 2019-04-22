# Replica set instance {#concept_bnt_3zn_tdb .concept}

ApsaraDB for MongoDB automatically creates a three-node replica set. You can directly perform operations on the primary node and a secondary node, whereas the other secondary node is hidden. Advanced features such as disaster recovery switchover and failover are packaged to ensure that they are completely transparent to you when you use the instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6645/1555923337916_en-US.png)

ApsaraDB for MongoDB allows you to increase the number of secondary nodes as required to scale out a three-node replica set to a five-node or seven-node replica set.

For example, certain business scenarios require databases with better read performance, such as reading websites and order query systems where there are more read operations than write operations, or scenarios with burst business requirements such as temporary activities. You can add or delete secondary nodes on demand to flexibly scale out or in the read performance of ApsaraDB for MongoDB.

-   **HA control system**: acts as an instance high-availability detection module to detect and monitor the operating status of ApsaraDB for MongoDB instances. If the system determines that the primary node of an ApsaraDB for MongoDB instance is unavailable, it switches over to an operable secondary node to ensure the high availability of the instance.
-   **Log collection**: collects the running logs of ApsaraDB for MongoDB, including the slow query logs and access control logs of ApsaraDB for MongoDB instances.
-   **Monitoring system**: collects the performance monitoring information about ApsaraDB for MongoDB instances, including basic metrics, disk capacity, access requests, input/output operations per second \(IOPS\), and other core information.
-   **Online migration system**: re-creates an ApsaraDB for MongoDB instance based on backup files in the backup system when the physical machine on which the instance runs becomes faulty. This avoids business interruption.
-   **Backup system**: backs up ApsaraDB for MongoDB instances and stores the generated backup files in Object Storage Service \(OSS\). Currently, the ApsaraDB for MongoDB backup system supports custom backup settings and temporary backup. It keeps backup files for seven days.
-   **Task control**: manages and controls various tasks for ApsaraDB for MongoDB instances, for example, to create instances, change the configuration, and back up instances. The task system can follow your instructions to flexibly control tasks, track tasks, and manage errors.

