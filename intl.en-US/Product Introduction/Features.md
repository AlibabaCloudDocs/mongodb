# Features

ApsaraDB for MongoDB is developed based on the distributed system and high-reliability storage engine of Apsara, and is compatible with the MongoDB protocol. ApsaraDB for MongoDB uses a multi-node architecture to ensure high availability, and supports elastic scaling, disaster recovery, backup and restoration, and performance optimization. This topic describes the features of ApsaraDB for MongoDB.

## Flexible architecture

ApsaraDB for MongoDB supports flexible deployment architectures, such as [Architecture of standalone instances](/intl.en-US/Product Introduction/System architecture/Architecture of standalone instances.md), [Architecture of replica set instances](/intl.en-US/Product Introduction/System architecture/Architecture of replica set instances.md), and [Architecture of sharded cluster instances](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md) to meet requirements of different business scenarios.

## Auto scaling

You can change the configuration of an ApsaraDB for MongoDB instance, including its specifications, storage space, and number of nodes, based on your business needs. You can also set the effective time for the configuration change. We recommend that you set the effective time to off-peak hours to avoid impacts on your business. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Data security

|Security technology|Description|
|:------------------|:----------|
|Anti-DDoS|ApsaraDB for MongoDB monitors inbound traffic in real time, filters source IP addresses to scrub large amounts of malicious traffic, and triggers blackhole filtering when traffic scrubbing becomes ineffective.|
|IP address whitelist|ApsaraDB for MongoDB filters IP addresses for instance access to implement high-level security protection. You can configure up to 1,000 IP addresses in a whitelist. For more information, see [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist for an ApsaraDB for MongoDB instance.md).|
|VPC|A VPC is an isolated virtual network with higher security and better performance than the classic network. You must create a VPC in advance. For more information, see [Create a VPC](~~65402~~).|
|Disaster recovery|ApsaraDB for MongoDB provides zone-disaster recovery to further meet high-reliability and data security requirements.

When you create an instance, you can deploy it in multiple zones. For more information, see [Create a multi-zone replica set instance](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone replica set instance.md) or [Create a multi-zone sharded cluster instance](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone sharded cluster instance.md). You can also migrate a replica set instance to multiple zones. For more information, see [Migrate an ApsaraDB for MongoDB instance across zones in the same region](/intl.en-US/User Guide/Instance management/Migrate an ApsaraDB for MongoDB instance across zones in the same region.md). |
|SSL encryption|ApsaraDB for MongoDB encrypts network connections in compliance with SSL at the transport layer to improve data security and ensure data integrity during communication. For more information, see [Configure SSL encryption for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure SSL encryption for an ApsaraDB for MongoDB instance.md).|
|TDE|ApsaraDB for MongoDB performs real-time I/O encryption and decryption on data files. Data is encrypted before it is written to a disk, and decrypted when it is read from the disk and written into the memory. TDE does not increase the size of data files. You can use TDE without modifying your application that uses ApsaraDB for MongoDB. For more information, see [Configure TDE for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure TDE for an ApsaraDB for MongoDB instance.md).|
|Automatic backup|You can set a backup policy to configure the start time for data backup during off-peak hours. For more information about how to set a backup policy, see [Configure automatic backup for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md).|
|Temporary backup|You can manually back up ApsaraDB for MongoDB data. For more information, see [Manually back up an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md). Both physical backup and logical backup are supported.|
|Data restoration|You can create an instance based on a backup file, create an instance based on the backup file that is generated at a specific time point, and restore backup data to the current instance. For more information, see [Create an instance from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Restore data to a new ApsaraDB for MongoDB instance by point in time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), and [Restore data to your current ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to your current ApsaraDB for MongoDB instance.md).|
|Backup file download|ApsaraDB for MongoDB retains your backup files free of charge for up to seven days. During this period, you can log on to the ApsaraDB for MongoDB console and download the backup files to a local device.|

## Comprehensive monitoring

ApsaraDB for MongoDB monitors up to 20 system performance metrics, such as disk capacity, IOPS, connections, CPU utilization, network traffic, transactions per second \(TPS\), queries per second \(QPS\), and cache hit ratio. For more information, see [View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md).

## Professional tools

[Data Management](~~47550~~) \(DMS\) allows you to manage relational databases such as MySQL, SQL Server, and PostgreSQL, non-relational databases such as MongoDB and Redis, and Linux servers. DMS offers an integrated solution to view BI charts and data trends, track data, optimize performance, implement access control, and manage data, schemas, and servers.

[Data Transmission Service](~~26592~~) \(DTS\) is a data service that is provided by Alibaba Cloud to support data exchange between data sources such as relational database management system \(RDBMS\), NoSQL, and online analytical processing \(OLAP\). It provides data transmission capabilities such as data migration, real-time data subscription, and real-time data synchronization. DTS applies to scenarios such as data migration without server downtime, geo-disaster recovery, cross-border data synchronization, and cache refresh policies. It helps you build a secure, scalable, and highly available data architecture.

