# Change the billing method of an ApsaraDB for MongoDB instance from pay-as-you-go to subscription

This topic describes how to change the billing method of an ApsaraDB for MongoDB instance from pay-as-you-go to subscription. Changes to the billing method do not impact on the running of the instance.

## Prerequisites

-   The instance is in the running state.
-   The billing method of the instance is pay-as-you-go.
-   The instance has no unpaid subscription orders.
-   The instance type is available for purchase. For more information about unavailable instance types, see [Historical instance types](/intl.en-US/Product Introduction/Instance types.md). If you want to change the billing method of an instance whose instance type is unavailable now to subscription, change the instance type first. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

## Precautions

-   The billing method of a subscription instance cannot be changed to pay-as-you-go. Exercise caution when changing the billing method of your instance.
-   You cannot release a subscription instance.
-   If the instance has an unpaid order, you cannot upgrade the specifications of a subscription instance. You need to cancel this order on the [Billing Management](https://expense.console.aliyun.com/?&returnExpense=true#/order/list/) page and change the billing method of the instance to subscription.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the **Basic Information** section, click **Switch to Subscription**.

    ![Change the billing method from pay-as-you-go to subscription](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7038862161/p240049.png)

6.  On the Confirm Order page, specify **Purchase Cycle** of the instance.

7.  Read and select **ApsaraDB for MongoDB Agreement of Service** and click **Activate**.

    **Note:** You must complete the generated subscription order. You cannot purchase a new instance or change the billing method to subscription until you pay for this order or cancel it. You can pay for or cancel this order on the [Billing Management](https://expense.console.aliyun.com/#/order/list/) page.

8.  Select a payment method and click **confirm to pay**.


