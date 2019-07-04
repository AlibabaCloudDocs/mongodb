# Instance type families {#concept_ic2_kd3_fhb .concept}

## Families {#section_ykl_vwh_fhb .section}

ApsaraDB for MongoDB provides general and dedicated instance type families.

|Family|Description|Scenario|
|:-----|:----------|:-------|
|General| -   Instances that have exclusive use of allocated memory and I/O resources and share CPU and storage resources with other general instances on the same physical server.
-   It is a highly cost-effective instance type family which allows you to minimize costs by reusing resources and enjoy the benefits brought by the scale.
-   Its storage capacity is independent of CPU and memory, which allows flexible configurations.

 | -   Price-sensitive customers.
-   Fewer requirements for performance and stability.

 |
|Dedicated| Instances that have exclusive use of CPU, memory, storage, and I/O resources. Instances of this type family feature high performance and stability and are independent of other instances running on the same physical server.

 The top configuration of this type family is the **Exclusive physical machine** \(also called the DDH\), which exclusively occupies all resources owned by a physical server.

 |A database is a core component of certain businesses, such as finance, e-commerce, government, and large and medium-sized online businesses.|

The following figure shows the differences between general and dedicated instance type families.

![Comparison between ApsaraDB for MongoDB instance type families](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149733/156222481141619_en-US.png)

## Instance types {#section_svm_dxh_fhb .section}

For more information about instance types and specifications such as the number of CPU cores, memory, storage space, maximum number of allowed connections, and IOPS, see [Instance type families](#).

## Pricing {#section_fmc_fxh_fhb .section}

For the price of each instance type, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#).

## Change instance types {#section_ehw_fxh_fhb .section}

You can change instance types as needed. For more information about specific operations, see [Change the configuration](../../../../intl.en-US/User Guide/Instance management/Change the configuration.md#).

