# Features {#concept_uw4_3zd_z2b .concept}

## Flexible Architecture {#section_oyk_3nk_xdb .section}

ApsaraDB for MongoDB supports flexible deployment architecture. It provides standalone, replica set, and sharded cluster instances to meet requirements in different business scenarios.

## Auto scaling {#section_xkx_d23_zz .section}

Based on business requirements, you can change the configuration of an ApsaraDB for MongoDB instance, including its specifications, storage space, and number of nodes. You can also set the effective time for the configuration change. We recommend that the configuration change take effect during off-peak hours to avoid an impact on business.

## Data security {#section_xqc_knk_xdb .section}

-   Automatic backup: You can set a backup policy to flexibly configure the start time for data backup during off-peak hours.
-   Temporary backup: You can start data backup as required. ApsaraDB for MongoDB supports physical backup and logical backup.
-   Data recovery: Using backup files, you can directly overwrite data to recover an existing instance or create an instance based on a time point.
-   Backup file download: ApsaraDB for MongoDB keeps your backup files free of charge for seven days. During this period, you can log on to the console and download the backup files to your local device.
-   Anti-DDoS: ApsaraDB for MongoDB monitors traffic at the network ingress in real time. When it detects any heavy-traffic attacks, it starts traffic scrubbing to filter source IP addresses. If traffic scrubbing is ineffective, ApsaraDB for MongoDB triggers the black hole mechanism.
-   IP address whitelist: ApsaraDB for MongoDB filters IP addresses for access to instances to provide the highest-level access security protection. You can add a maximum of 1,000 IP addresses to the whitelist.
-   SSL encryption: Network connections are encrypted in compliance with SSL at the transport layer to improve data security and guarantee data integrity during communication.
-   Multi-layer network security protection: A VPC is directly isolated and protected at the TCP layer. Anti-DDoS provides real-time monitoring and traffic scrubbing to mitigate heavy-traffic attacks.

## Comprehensive monitoring {#section_z1d_qnz_j1b .section}

ApsaraDB for MongoDB provides over 20 system performance metrics, including the disk capacity, IOPS, connections, CPU usage, network traffic, transactions per second \(TPS\), queries per second \(QPS\), and cache hit ratio.

## Professional tools {#section_zgn_2sd_z2b .section}

Data Transmission Service \(DTS\) is a data service provided by Alibaba Cloud to support data exchanges between relational database management system \(RDBMS\), NoSQL, online analytical processing \(OLAP\), and other data sources. DTS provides multiple data transmission features, including data migration, real-time data subscription, and real-time data synchronization. Data Transmission applies to use cases such as data migration, remote disaster recovery, cross-border data synchronization, and cache update policies without service interruption, helping you build a secure, scalable, and highly available data architecture.

