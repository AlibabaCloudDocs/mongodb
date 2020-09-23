# Comparison between ApsaraDB for MongoDB and user-created databases

Compared with user-created databases, ApsaraDB for MongoDB has outstanding advantages in terms of service availability, data reliability, security, and O&M cost. ApsaraDB for MongoDB helps you quickly start your business and reduce O&M costs.

|Item|ApsaraDB for MongoDB|User-created database|
|----|--------------------|---------------------|
|Service availability|High availability.|You must ensure security and build primary/secondary replication and RAID.|
|High availability disaster recovery in one or three zones in the same city.|Local disaster recovery requires self-deployment and maintenance. The dual-zone conditions are difficult to implement, and database-level availability is not guaranteed.|
|Allows you to create geo-disaster recovery instances.|You must use a third-party tool to create disaster recovery instances.|
|Data reliability|-   High reliability.
-   The recovery point objective \(RPO\) of single- and three-zone replica set instances is 0.

|You must ensure security and build primary/secondary replication and RAID.|
|System security|Pre-protection: DDoS attack protection, automatic repair of various database security vulnerabilities, [whitelist-based access control](/intl.en-US/User Guide/Data security/Configure a whitelist for an ApsaraDB for MongoDB instance.md), and [VPC isolation](/intl.en-US/Quick Start for Replica Set/Connect to an instance/Overview of replica set instance connections.md).|Pre-protection: requires additional security hardware or software to fix security vulnerabilities at high costs.|
|In-process protection: [SSL encryption](/intl.en-US/User Guide/Data security/Configure SSL encryption for an ApsaraDB for MongoDB instance.md) and [Transparent data encryption](/intl.en-US/User Guide/Data security/Configure TDE for an ApsaraDB for MongoDB instance.md).|In-process protection: You must build SSL encryption and TDE systems.|
|Event auditing: [Database log auditing](/intl.en-US/User Guide/Data security/Audit logs (previous version)/Configure audit logging for an ApsaraDB for MongoDB instance.md).|Event auditing: You must purchase an additional auditing system.|
|Backup and recovery|-   Complete kernel enables both physical backup and logical backup to be performed in [manual backup](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md) and increases backup efficiency three times.
-   [Single-database recovery](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md).

|-   The open-source version supports only logical backup and is inefficient.
-   Single-database recovery is unavailable and recovery efficiency is low.
-   You must ensure the accuracy of data recovery in the distributed architecture. |
|System hosting|No hosting fee.|You need to pay additional server hosting fees. The more complex the architecture, the more servers you need to host and the higher the hosting fees.|
|O&M cost|No additional O&M costs.|Requires dedicated maintenance personnel and high O&M costs.|
|[Performance monitoring in seconds](/intl.en-US/User Guide/Monitoring and alerting/Set the monitoring granularity.md) and [CloudDBA](/intl.en-US/User Guide/CloudDBA/Index optimization of ApsaraDB for MongoDB.md).|Conducts performance monitoring in minutes without any diagnosis. It is complex to troubleshoot slow queries.|
|Deployment and scaling|Supports real-time activation and elastic scaling.|Requires hardware procurement, hosting of data centers, and machine deployment, which takes rather a long period. You must maintain the node relationship when adding new nodes.|
|Kernel optimization|-   Optimizes oplog synchronization performance and short-lived connection performance for general scenarios.
-   Ensures data consistency with technologies such as logical snapshots. This reduces costs by 50% in long-time data import scenarios.


|The open-source version does not provide optimization and cannot be used in some scenarios.|

