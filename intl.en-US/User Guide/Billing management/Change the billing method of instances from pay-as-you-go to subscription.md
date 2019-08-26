# Change the billing method of instances from pay-as-you-go to subscription {#concept_ejm_sbv_4fb .concept}

You can change the billing method of an ApsaraDB for MongoDB instance from pay-as-you-go to subscription. Changing the billing method of the instance has no impact on the running of the instance.

## Precautions {#section_x42_ql1_pfb .section}

-   The billing method of subscription-based instances cannot be changed to pay-as-you-go. To prevent resource waste, determine whether you need to change the billing method of your resources.
-   You cannot release subscription-based instances. If you want to unsubscribe from subscription-based instances during your contract period, you need to pay the fees accordingly. For more information, see [Refund instructions](https://help.aliyun.com/document_detail/37096.html).
-   You cannot update the specifications of the instance if you have an unpaid subscription-based instance. You need to cancel this order on the [Orders](https://expense.console.aliyun.com/#/order/list/) page and change the billing method of the corresponding instance to subscription.

## Prerequisites {#section_c1x_b41_pfb .section}

-   The instance is in the running state.
-   The billing method of the instance is pay-as-you-go.
-   You do not have an unpaid subscription-based instance.
-   The instance type cannot be phased-out types \(that is, instance types are no longer available for sale\). For more information about phased-out instance types, see the [Instance types](../../../../intl.en-US/Product Introduction/Instance specifications.md#section_hxm_lmc_bfb) displayed before July 10, 2017. If you need to change the billing method of a phased-out instance type to subscription, change the instance type first. For specific operations, see [Change the configuration](intl.en-US/User Guide/Instance management/Change the configuration.md#).

## Procedure {#section_zgc_p41_pfb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the page, select the region of the instance.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances**.
4.  Locate the instance and click the instance ID.
5.  On the Basic Information page, click **Switch to Subscription**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24535/156679894514324_en-US.png)

6.  On the Confirm Order page, select the **Purchase Duration** of the instance.
7.  Select ApsaraDB for MongoDB Agreement of Service, and click **Activate**.

    **Note:** The system will generate an order for you to switch to the subscription billing method. If this order is not paid or canceled, you cannot purchase new instances or switch the instance billing method to subscription. You can pay for or cancel this order on the [Orders](https://expense.console.aliyun.com/#/order/list/) page.

8.  Select a payment method and click **Confirm Payment**.

