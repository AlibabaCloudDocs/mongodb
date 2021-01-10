# Instance categories

This topic describes general-purpose and dedicated instance categories of ApsaraDB for MongoDB.

## Categories

ApsaraDB for MongoDB provides general-purpose, dedicated-disk, and dedicated-host instance categories.

|Category|Description|Scenario|
|:-------|:----------|:-------|
|General-purpose|-   General-purpose instances occupy exclusive memory but share CPU, I/O, and storage resources with the other general-purpose instances on the same physical server.
-   CPU resources are highly reused among shared instances that are deployed on the same physical host. This maximizes cost-effectiveness.
-   The storage capacity of a general-purpose instance is independent of the number of CPU cores and memory capacity. You can flexibly configure the storage capacity.

|-   Price-sensitive scenarios.
-   Scenarios that require a baseline level of performance stability. |
|Dedicated-disk|-   Dedicated local disks: instances that occupy exclusive CPU, memory, and storage capacity, and share storage media and I/O resources with other general-purpose instances on the same physical server.
-   Dedicated cloud disks: instances that occupy exclusive CPU, memory, storage media, and I/O resources. The instances with dedicated cloud disks do not share storage media and I/O resources. Therefore, the performance remains stable and is not affected by other instances that are deployed on the same physical server.

The top configuration of this category is the dedicated host, which exclusively occupies all resources on a physical server.

|Business scenarios where databases are used as core systems, such as finance, e-commerce, government affairs, and large and medium-sized Internet services.|
|Dedicated-host|-   You can log on to dedicated hosts and perform operations and maintenance \(O&M\).
-   Instances with dedicated hosts occupy exclusive resources on the virtual or physical hosts where they are deployed.
-   You can create multiple database instances on a host.

Dedicated hosts enable flexible resource scheduling and meet your requirements for regulatory compliance, high performance, and security. For more information, see [What is ApsaraDB for MyBase?]()|Scenarios that require flexible resource scheduling and full permissions on hosts.|

The following figure shows the differences among general-purpose instances, instances with dedicated local disks, and instances with dedicated cloud disks.

![Comparison between ApsaraDB for MongoDB instance categories](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7801129951/p41619.png)

## Instance types

For more information about instance types and specifications such as the number of CPU cores, memory, storage space, maximum number of allowed connections, and IOPS, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

## Pricing

For the price of each instance type, see [Billing items and pricing](/intl.en-US/Purchase Guide/Billing items and pricing.md).

## Change instance types

You can change instance types. For more information about specific operations, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

