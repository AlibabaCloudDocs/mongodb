# Architecture of ApsaraDB for MongoDB {#concept_lyt_gc5_xgb .concept}

## Architecture {#section_akh_kc5_xgb .section}

![Architecture of ApsaraDB for MongoDB](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132916/156222393139713_en-US.png)

## Components {#section_lzk_jc5_xgb .section}

-   HA control system

    It acts as a high-availability detection module to detect the running status of ApsaraDB for MongoDB instances. If the system determines that the primary node of an ApsaraDB for MongoDB instance is unavailable, it fails over to a secondary node to ensure the high availability of the instance.

-   Log collection system

    It collects the running logs of ApsaraDB for MongoDB, including slow query and audit logs.

-   Monitoring system

    This system collects important performance monitoring information about ApsaraDB for MongoDB instances, such as the basic metrics, disk capacity, access requests, and input/output operations per second \(IOPS\).

-   Online migration system

    To prevent interruptions to your business, the system create a new instance from the backup files in the backup system, when the physical server where the instance runs fails.

-   Backup system

    This system backs up ApsaraDB for MongoDB instances and stores the generated backup files in Object Storage Service \(OSS\). This backup system allows you to customize backup settings \(manual or automatic\). It can retain files for seven days.

-   Task control

    ApsaraDB for MongoDB instances manage and control various instance-related tasks, such as instance creation, configuration changes, and instance backup. The task system follows your instructions to control tasks, track tasks, and manage errors.


