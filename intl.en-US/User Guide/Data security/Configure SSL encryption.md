# Configure SSL encryption {#concept_v1g_vyv_y2b .concept}

To enhance the security of data links, you can enable SSL encryption and install an SSL certificate issued by the CA in your application. The SSL encryption feature encrypts network connections at the transport layer to improve data security and guarantee data integrity during communication. This topic describes how to view the details of SSL encryption, enable and disable SSL encryption, and update and download an SSL CA certificate.

## Notes {#section_ztb_1zz_ggb .section}

-   Only replica set instances whose database version is MongoDB 3.4 or MongoDB 4.0 support SSL encryption.
-   When you enable, update, or disable SSL encryption for an instance, the instance is restarted once. Therefore, we recommend that you perform such an operation during off-peak hours.
-   You can download an SSL CA certificate only from the console.
-   Due to the inherent defects of SSL encryption, this feature significantly increases the CPU usage. We recommend that you enable SSL encryption only when external network links need to be encrypted. Intranet links are securer and generally do not need to be encrypted.

## Enable SSL encryption {#section_qcd_4dv_y2b .section}

**Note:** When you enable SSL encryption for an instance, the instance is restarted once. Therefore, we recommend that you perform this operation during off-peak hours.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **SSL**.
6.  In the SSL area, turn on the **SSL Status** switch.
7.  In the Restart Instance dialog box that appears, click **OK**.

## Update an SSL CA certificate {#section_tzm_dfv_y2b .section}

An SSL CA certificate is valid for a year. You can update an SSL CA certificate when it expires or within its validity period.

**Note:** When you update the SSL CA certificate for an instance, the instance is restarted once. Therefore, we recommend that you perform this operation during off-peak hours.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **SSL**.
6.  In the SSL area, click **Update Certificate**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18857/155617605810641_en-US.png)

7.  In the Restart Instance dialog box that appears, click **OK**.

## Download an SSL CA certificate {#section_ajh_sdv_y2b .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **SSL**.
6.  Click **Download Certificate** to download the SSL CA certificate to a local device.

## Disable SSL encryption {#section_rvt_jhv_y2b .section}

You can disable SSL encryption when you do not need this feature.

**Note:** When you disable SSL encryption for an instance, the instance is restarted once. Therefore, we recommend that you perform this operation during off-peak hours.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **SSL**.
6.  In the SSL area, turn off the **SSL Status** switch.
7.  In the Restart Instance dialog box that appears, click **OK**.

