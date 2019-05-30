# Configure a whitelist {#concept_xpy_wcx_w2b .concept}

After a MongoDB instance is created, you must configure a whitelist to allow external devices to access the instance. The default whitelist contains only the default IP address 127.0.0.1, indicating that no device is able to access the MongoDB instance. This topic describes how to configure a whitelist in the console.

## Precautions {#section_jmq_nvs_lgb .section}

-   Before using an instance for the first time, you must modify its whitelist. After the whitelist is configured, the network addresses of the instance are displayed on the Basic Information and Database Connection pages.
-   Proper configuration of the whitelist can enhance access security protection for ApsaraDB for MongoDB. We recommend that you regularly maintain the whitelist.

## Procedure {#section_omq_pjw_w2b .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the homepage, select the region of the instance.
3.  In the left-side navigation pane, click **Sharding instances**.
4.  Locate the target instance, and then click the instance ID.
5.  In the left-side navigation pane, choose **Security Control** \> **Whitelist Settings**.
6.  Select **Manually Modify** or **Import ECS Intranet IP**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6670/155920688013265_en-US.png)

    -   Click **Manually Modify**, enter an IP address or CIDR block, and click**OK**.
    -   Click **Import ECS Intranet IP**. All internal IP addresses of ECS instances that belong to your account are displayed. You can select some ECS internal IP addresses, add them to the whitelist, and click **OK**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6670/155920688013266_en-US.png)

    **Note:** 

    -   Separate multiple addresses with commas \(,\). No duplicate addresses are allowed. A maximum of 1,000 addresses can be added. Format: 0.0.0.0/0, 10.23.12.24 \(IP address\), or 10.23.12.24/24 \(CIDR block. /24 represents the length of the prefix in the IP address. The prefix length can range from 1 to 32\).
    -   0.0.0.0/0 or null represents no IP address is blocked. This configuration incurs a high security risk to the database. We recommend that you add only the public IP addresses or CIDR blocks of your own Web servers to the whitelist.

## Delete a whitelist {#section_j1p_nlw_w2b .section}

You can delete any whitelist group other than the default whitelist group.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the homepage, select the region of the instance.
3.  In the left-side navigation pane, click **Sharding instances**.
4.  Locate the target instance, and then click the instance ID.
5.  In the left-side navigation pane, choose **Security Control** \> **Whitelist Settings**.
6.  Locate the whitelist group and choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6723/155920688013851_en-US.png)** \> **Delete Whitelist Group** in the **Actions** column.
7.  In the Delete Whitelist Group message that appears, click **OK**.

