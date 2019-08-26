# Billing items and pricing {#concept_jww_bny_32b .concept}

## Billing items {#section_b4s_tny_32b .section}

The following table describes the billing items and billing standards of ApsaraDB for MongoDB.

|Instance|Billing item|Billing standard|
|--------|------------|----------------|
|Standalone instance Replica set instance

 | -   Number of nodes
-   Specifications
-   Disk space

 | For more information about the billing standards, see [ApsaraDB for MongoDB Pricing](https://www.alibabacloud.com/product/apsaradb-for-mongodb#pricing).

 |
|Sharded cluster instance| -   Mongos node specifications
-   Shard specifications
-   Shard disk space
-   Config server specifications
-   Config server disk space

 |

## Billing methods {#section_sqh_j2j_m2b .section}

|Billing method|Expiration or payment overdue|Renewal|Configuration change|
|--------------|-----------------------------|-------|--------------------|
|Subscription: A subscription mode in which you need to pay for an instance when creating it.

 |When the subscription to an instance expires, you can continue to use it for 15 days. After 15 days, the instance is locked and its data is kept for 15 days. No fee is charged when the instance is locked.

 After the instance has expired for 30 days, it is released and its data is permanently deleted.

 |You can renew the subscription to an instance within the contract period or within 30 days after the contract expires. The renewed instance is billed based on its new configuration and subscription period.

 | -   Within the contract period, you can only upgrade the configuration of a subscription-based instance, but cannot downgrade its configuration or release it.
-   Upgrade fee = Daily price difference of an instance before and after the upgrade x Number of remaining days from the upgrade date to the expiration date
-   If the configuration of an instance is upgraded for at least 356 days, its price after the upgrade is calculated on a yearly basis.
-   If the configuration of an instance is upgraded for less than 356 days, its price after the upgrade is calculated on a monthly basis. The remaining validity period of this instance lasts until its expiration date.

 |
|Pay-As-You-Go: A Pay-As-You-Go mode in which a bill is generated per hour based on the configuration of an instance to deduct money from your account balance.

 |If your account balance is insufficient, all Pay-As-You-Go instances under your account become overdue. You can continue to use an overdue instance for 15 days, after which the instance is locked. If the instance remains overdue after 30 days, it is released and its data is permanently deleted.

 After the instance has been released for seven days, its backup data is permanently deleted. Within seven days after the instance is released, the data that has exceeded the specified period for keeping backup data is deleted in half an hour.

 |Because a Pay-As-You-Go instance is billed based on the actual usage time, renewal is not required. You only need to recharge your account in the Alibaba Cloud console.| -   You can release a Pay-As-You-Go instance as required and downgrade or upgrade its configuration. For more information, see [Change the configuration](https://www.alibabacloud.com/help/zh/doc-detail/44655.htm).
-   You can directly change the billing method of a Pay-As-You-Go instance to subscription. The billing method takes effect immediately after being changed.

 |

