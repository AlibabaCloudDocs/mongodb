# Configure a whitelist {#concept_xpy_wcx_w2b .concept}

After creating an ApsaraDB for MongoDB instance, you need to configure a whitelist for the instance to allow external devices to access this instance. The default whitelist contains only the IP address 127.0.0.1, indicating that no device is allowed to access this instance. This topic describes how to configure a whitelist in the console.

## Notes {#section_jmq_nvs_lgb .section}

-   Before using the target instance for the first time, you must configure its whitelist. After configuring the whitelist, you can view the connection information about the instance on its Basic Information page and Database Connection page.
-   If you use the whitelist correctly, you can guarantee the highest-level security protection for your ApsaraDB for MongoDB instance. We recommend that you maintain the whitelist on a regular basis.

## Procedure {#section_omq_pjw_w2b .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Setting**.
6.  Select **Manually Modify** or **Import ECS Intranet IP** to configure the IP address whitelist.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18639/155617506345451_en-US.png)

    -   Select **Manually Modify**. On the page that appears, enter IP addresses or CIDR blocks and click **OK**.
    -   Select **Import ECS Intranet IP**. The system displays all ECS intranet IP addresses under your account. You can select ECS intranet IP addresses, add them to the whitelist, and click **OK**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18639/155617506345452_en-US.png)

    **Note:** 

    -   You need to separate IP addresses with commas \(,\) and ensure that they are different from one another. You can add a maximum of 1,000 IP addresses. Supported formats include 0.0.0.0/0, 10.23.12.24, and 10.23.12.24/24. 10.23.12.24 is an IP address, and 10.23.12.24/24 is a CIDR notation, in which the suffix /24 indicates the number of bits for the prefix of the IP address. The suffix ranges from 1 to 32.
    -   0.0.0.0/0 and empty indicate that your ApsaraDB for MongoDB instance can be accessed by all IP addresses. In this case, the database is at high security risk. We recommend that you add only the public IP addresses or CIDR blocks of your web servers to the whitelist.

## Delete a whitelist group {#section_j1p_nlw_w2b .section}

You can delete whitelist groups other than the default group.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Setting**.
6.  Locate the whitelist group to be deleted. Choose **![](images/13851_en-US.png)** \> **Delete Whitelist Group** in the **Operation** column.
7.  In the Delete Whitelist Group dialog box that appears, click **OK** to delete the whitelist group.

