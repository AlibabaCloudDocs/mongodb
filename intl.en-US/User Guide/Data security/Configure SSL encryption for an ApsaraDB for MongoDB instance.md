# Configure SSL encryption for an ApsaraDB for MongoDB instance

This topic describes how to enhance link security by enabling Secure Sockets Layer \(SSL\) encryption and installing SSL CA certificates on your application services. The SSL encryption feature encrypts network connections at the transport layer to improve data security and ensure data integrity during communication. This topic describes operations related to SSL encryption.

-   The instance is a replica set instance.
-   The database version of the instance is 3.4, 4.0, or 4.2.

## Notes

When you enable or disable SSL encryption or update SSL CA certificates for an instance, the instance is restarted. Plan your operations in advance and make sure that your applications can automatically re-establish a connection.

**Note:** When an instance is restarted, all its nodes are restarted in turn and each node goes through a transient connection of about 30 seconds. If the instance houses more than 10,000 collections, the transient connections last longer.

## Precautions

-   You can download SSL CA certificate files only from the ApsaraDB for MongoDB console.
-   After you enable SSL encryption for an instance, the CPU utilization of the instance is significantly increased. We recommend that you enable SSL encryption only when necessary. For example, you can enable SSL encryption when you connect to an ApsaraDB for MongoDB instance over the Internet.

    **Note:** Internal network connections are more secure than Internet connections and do not need SSL encryption.

-   After you enable SSL encryption for an instance, both SSL and non-SSL connections are supported.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Data Security** \> **SSL**.

6.  Perform one of the following operations:

    **Note:** When you enable or disable SSL encryption or update SSL CA certificates for an instance, the instance is restarted. Plan your operations in advance and make sure that your applications can automatically re-establish a connection.

    |Operation|Prerequisite|Procedure|
    |:--------|:-----------|:--------|
    |Enable SSL encryption|The SSL encryption status is **Disabled**.|Turn on the switch next to **SSL Status**. In the message that appears, click **OK**.|
    |Update an SSL CA certificate|The SSL encryption status is **Enabled**.|Click **Update Certificate**. In the message that appears, click **OK**.|
    |Download an SSL CA certificate file|The SSL encryption status is **Enabled**.|Click **Download Certificate** to download an SSL CA certificate file to your computer.|
    |Disable SSL encryption|The SSL encryption status is **Enabled**.|Turn off the switch next to **SSL Status**. In the message that appears, click **OK**.|


## References

[Use the mongo shell to connect to an ApsaraDB for MongoDB database in SSL encryption mode](/intl.en-US/User Guide/Data security/Use the mongo shell to connect to an ApsaraDB for MongoDB database in SSL encryption mode.md)

