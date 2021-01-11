# Configure a whitelist for an ApsaraDB for MongoDB instance

This topic describes how to configure a whitelist for an ApsaraDB for MongoDB instance. After you create an ApsaraDB for MongoDB instance, you must configure an IP address whitelist to allow access only from authorized devices. The default whitelist contains only the IP address 127.0.0.1, which indicates that no devices can access the ApsaraDB for MongoDB instance.

-   Before you use an ApsaraDB for MongoDB instance for the first time, you must configure a whitelist for it. After you configure the whitelist, the endpoints of the instance appear on the **Basic Information** and **Database Connection** pages.
-   Whitelists make your ApsaraDB for MongoDB instance more secure. We recommend that you maintain the whitelists on a regular basis.

## Configure an IP address whitelist for a standalone or replica set instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Settings**.

6.  Find an IP address whitelist, and choose ![More](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7023797951/p13206.png) \> **Manually Modify** or **Import ECS Intranet IP** in the **Actions** column.

    **Manually Modify**

    1.  In the **Manually Modify** panel, click the **IPv4** or **IPv6** tab based on your network connection.

        **Note:**

        -   Limits for **IPv4** addresses:
            -   Separate multiple IP addresses with commas \(,\). A maximum of 1,000 different IP addresses can be added.

                Supported formats are IP addresses such as `0.0.0.0/0` and `10.23.12.24`, or CIDR blocks such as `10.23.12.24/24`. `/24` indicates the length of the IP address prefix in the [CIDR block](~~54484~~). An IP address prefix can contain 1 to 32 bits.

            -   If the whitelist is empty or contains only `0.0.0.0/0`, all devices are granted access. This is risky for your ApsaraDB for MongoDB instance. We recommend that you add only the IP addresses or CIDR blocks of your own web servers to the whitelist.
        -   Limits for **IPv6** addresses:
            -   Separate multiple IP addresses with commas \(,\). A maximum of 1,000 different IP addresses can be added.

                IP address formats such as `0:0:0:0:0:0:0:1` and `::` are supported. [CIDR blocks](~~54484~~) are not supported.

            -   If the whitelist is empty or contains only `::`, all devices are granted access. This is risky for your ApsaraDB for MongoDB instance. We recommend that you add only the IP addresses of your own web servers to the whitelist.
            -   You can specify **IPv6** whitelists only if the instance resides in Hangzhou Zone G.
            -   You can specify **IPv6** whitelists only if the engine version of the instance is 4.2.
        -   You cannot specify both **IPv4** and **IPv6** addresses in a single whitelist. If you want to specify both IPv4 and IPv6 addresses, specify them in separate whitelists.
    2.  Click **OK**.

    **Import ECS Intranet IP**

    1.  Click **Import ECS Intranet IP**. In the Import ECS Intranet IP panel, the internal IP addresses of ECS instances created in the current account are displayed. Select IP addresses and add them to the IP address whitelist.

        ![Add internal IP addresses of ECS instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8023797951/p13209.png)

    2.  Click **OK**.


## Configure an IP address whitelist for a sharded cluster instance

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Settings**.

6.  Find an IP address whitelist, and choose ![More](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7023797951/p13206.png) \> **Manually Modify** or **Import ECS Intranet IP** in the **Actions** column.

    **Manually Modify**

    1.  In the **Manually Modify** panel, click the **IPv4** or **IPv6** tab based on your network connection.

        **Note:**

        -   Limits for **IPv4** addresses:
            -   Separate multiple IP addresses with commas \(,\). A maximum of 1,000 different IP addresses can be added.

                Supported formats are IP addresses such as `0.0.0.0/0` and `10.23.12.24`, or CIDR blocks such as `10.23.12.24/24`. `/24` indicates the length of the IP address prefix in the [CIDR block](~~54484~~). An IP address prefix can contain 1 to 32 bits.

            -   If the whitelist is empty or contains only `0.0.0.0/0`, all devices are granted access. This is risky for your ApsaraDB for MongoDB instance. We recommend that you add only the IP addresses or CIDR blocks of your own web servers to the whitelist.
        -   Limits for **IPv6** addresses:
            -   Separate multiple IP addresses with commas \(,\). A maximum of 1,000 different IP addresses can be added.

                IP address formats such as `0:0:0:0:0:0:0:1` and `::` are supported. [CIDR blocks](~~54484~~) are not supported.

            -   If the whitelist is empty or contains only `::`, all devices are granted access. This is risky for your ApsaraDB for MongoDB instance. We recommend that you add only the IP addresses of your own web servers to the whitelist.
            -   You can specify **IPv6** whitelists only if the instance resides in Hangzhou Zone G.
            -   You can specify **IPv6** whitelists only if the engine version of the instance is 4.2.
        -   You cannot specify both **IPv4** and **IPv6** addresses in a single whitelist. If you want to specify both IPv4 and IPv6 addresses, specify them in separate whitelists.
    2.  Click **OK**.

    **Import ECS Intranet IP**

    1.  Click **Import ECS Intranet IP**. In the Import ECS Intranet IP panel, the internal IP addresses of ECS instances created in the current account are displayed. Select IP addresses and add them to the IP address whitelist.

        ![Add internal IP addresses of ECS instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8023797951/p13209.png)

    2.  Click **OK**.


## Common connection scenarios

-   [Connect a local client to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account.md)

