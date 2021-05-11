# Instance categories

This topic describes general-purpose, dedicated-disk, and dedicated-host instance categories of ApsaraDB for MongoDB.

## Categories

|Category|Description|Scenario|
|--------|-----------|--------|
|General-purpose|-   General-purpose instances on the same physical server occupy dedicated memory and storage but share CPU and I/O resources.
-   CPU resources are highly reused among shared instances that are deployed on the same physical server. This maximizes cost-effectiveness.

|-   Price-sensitive scenarios.
-   Scenarios that require a baseline level of performance stability. |
|Dedicated-disk|-   Dedicated local-disk instances on the same physical server occupy dedicated memory, storage, and CPU resources but share I/O resources.
-   Dedicated cloud-disk instances occupy dedicated memory, storage, CPU, and I/O resources. Therefore, dedicated cloud-disk instances provide higher performance and stability and is less affected by other instances that are deployed on the same physical server than dedicated local-disk instances.

The top configuration of this category is a dedicated-host instance, which exclusively occupies all resources on a physical server.

|Business scenarios where databases are used as core systems, such as finance, e-commerce, government affairs, and large and medium-sized Internet services.|

The following figure shows the differences between general-purpose instances, dedicated local-disk instances, and dedicated cloud-disk instances.

![Comparison between ApsaraDB for MongoDB instance categories](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5820370261/p272668.png)

## Instance specifications

For more information about instance specifications such as the number of vCPUs, memory, storage capacity, maximum number of connections, and IOPS, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

## Pricing

For more information about the pricing of each instance type, see [Billing items and pricing](/intl.en-US/Purchase Guide/Billing items and pricing.md).

## Change instance specifications

You can change the specifications of an instance. For more information about specific operations, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

