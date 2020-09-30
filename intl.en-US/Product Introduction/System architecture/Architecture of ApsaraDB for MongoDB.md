# Architecture of ApsaraDB for MongoDB

This topic describes the architecture and components of ApsaraDB for MongoDB.

## Architecture

![Architecture of ApsaraDB for MongoDB](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1801129951/p39713.png)

## Components

-   Task control system

    ApsaraDB for MongoDB instances support various tasks, such as instance creation, configuration change, and instance backup. You can use the system to control tasks, track tasks, and manage errors.

-   HA control system

    The system acts as a high-availability detection module to detect the running status of ApsaraDB for MongoDB instances. If the system determines that the primary node of an ApsaraDB for MongoDB instance is unavailable, the system fails over to a secondary node to maintain the availability of the instance. You can also manually switch over between the primary and secondary nodes. For more information, see [Switch node roles](/intl.en-US/User Guide/Instance management/Switch node roles.md).

-   Log collection system

    The system collects the running logs of ApsaraDB for MongoDB, such as slow query and audit logs. For more information about the benefits of ApsaraDB for MongoDB, see [Overview](/intl.en-US/User Guide/Log management/Overview.md) and [Enable the new audit log feature](/intl.en-US/User Guide/Data security/Audit logs (new version)/Enable the new audit log feature.md).

-   Monitoring system

    The system monitors the performance of ApsaraDB for MongoDB instances and collects information such as their basic metrics, disk capacities, access requests, and input/output operations per second \(IOPS\). For more information, see [View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md).

-   Backup system

    The system backs up ApsaraDB for MongoDB instances and stores the generated backup files in Object Storage Service \(OSS\). It allows you to customize the backup policy to manually or automatically back up the instances. It retains the backup files for up to seven days. For more information about the benefits of ApsaraDB for MongoDB, see [Configure automatic backup for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md) and [Manually back up an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md).

-   Online migration system

    If the physical server where the instance resides fails, the system creates another instance from the backup files in the backup system to prevent impacts on your business. For more information, see [Overview](/intl.en-US/User Guide/Data migration and synchronization/Overview.md).


