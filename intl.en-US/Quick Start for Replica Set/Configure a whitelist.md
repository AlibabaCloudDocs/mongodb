# Configure a whitelist {#task774 .task}

After an ApsaraDB for MongoDB instance is created, it automatically adds the IP address 127.0.0.1 to a whitelist, indicating that all IP addresses and CIDR blocks are prohibited to access this instance. To guarantee database security and stability, you must delete 127.0.0.1 and add IP addresses or CIDR blocks that need to access your ApsaraDB for MongoDB instance to the whitelist. Otherwise, you cannot view the connection information about the instance on its Basic Information page. ApsaraDB for MongoDB allows you to add a maximum of 1,000 IP addresses to the whitelist.

Before using the target instance for the first time, you must configure its whitelist.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  Click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6671/155609100013267_en-US.png)** \> **Manage**in the Operation column corresponding to the target instance.
3.  On the Basic Information page that appears, click **Set the whitelist and the address will be displayed.**, as shown in the following figure. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6670/155609100013264_en-US.png)

    Alternatively, in the left-side navigation pane, choose **Data Security** \> **Whitelist Setting**, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6670/155609100013265_en-US.png)

4.  Select **Manually Modify** or **Import ECS Intranet IP** to configure the IP address whitelist. 

    -   Select **Manually Modify**. On the page that appears, enter IP addresses or CIDR blocks and click **OK**.
    -   Select **Import ECS Intranet IP**. The system displays all ECS intranet IP addresses under your account. You can select ECS intranet IP addresses, add them to the whitelist, and click **OK**, as shown in the following figure.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6670/155609100013266_en-US.png)

    **Note:** 

    -   You need to separate IP addresses with commas \(,\) and ensure that they are different from one another. You can add a maximum of 1,000 IP addresses. Supported formats include 0.0.0.0/0, 10.23.12.24, and 10.23.12.24/24. 10.23.12.24 is an IP address, and 10.23.12.24/24 is a CIDR notation, in which the suffix /24 indicates the number of bits for the prefix of the IP address. The suffix ranges from 1 to 32.
    -   0.0.0.0/0 and empty indicate that your ApsaraDB for MongoDB instance can be accessed by all IP addresses. In this case, the database is at high security risk. We recommend that you add only the public IP addresses or CIDR blocks of your web servers to the whitelist.


After configuring the whitelist, you can view the VPC connection information about the instance on its Basic Information page.

Subsequent operations

-   If you use the whitelist correctly, you can guarantee the highest-level security protection for your ApsaraDB for MongoDB instance. We recommend that you maintain the whitelist on a regular basis.
-   If necessary, you can select **Manually Modify** or **Import ECS Intranet IP** to modify the whitelist.

