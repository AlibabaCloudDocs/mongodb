# Configure log auditing {#concept_dqn_qnr_l2b .concept}

ApsaraDB for MongoDB provides log auditing to record all database operations that you have performed. Based on log auditing, you can conduct fault analysis, behavior analysis, and security audits for ApsaraDB for MongoDB. This feature can effectively help you obtain the information about data operations.

## Before you start {#section_vc4_4sh_y2b .section}

-   Replica set and sharded cluster instances support log auditing. Standalone instances do not support this feature.
-   You can specify the types of database operations to be audited for replica set instances.
-   You cannot specify the types of database operations to be audited for sharded cluster instances. When log auditing is enabled, the system automatically audits admin, slow, query, insert, update, and delete operations.
-   After log auditing is enabled, ApsaraDB for MongoDB stores the audit data for 30 days by default.
-   You can enable and disable log auditing only in the console. For more information, see [Enable log auditing](#section_yqc_1th_y2b) and [Disable log auditing](#section_gwp_bd3_y2b).
-   To query audited logs, you can log on to the ApsaraDB for MongoDB console or call the DescribeAuditRecords operation.

## Enable log auditing {#section_yqc_1th_y2b .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **Audit Log**.
6.  Click **Enable Audit Log**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6736/155617573210389_en-US.png)

    **Note:** When you enable log auditing, the CloudDBA index optimization feature is also enabled. For more information about CloudDBA index optimization, see Optimize indexes.

7.  Click **OK**.

## Query and download audited logs {#section_q3c_n43_y2b .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **Audit Log**.
6.  You can query, export, and download audited logs.
    -   Query: You can enter the database name \(**DB**\), username used to log on to the database \(**User**\), and a word or record in a collection \(**Keyword**\), and select or enter the start time and end time to query audited logs by condition.

        |Name|Description|
        |:---|:----------|
        |**Database Name**|The name of the queried database. If you specify the database name, audited logs of the specified database are displayed for the target instance. If you do not specify the database name, audited logs of all databases are displayed for the target instance.

 |
        |**Account Name**|The username used to log on to the queried database. If you specify the username, audited logs of the database that is logged on to by using the specified username are displayed for the target instance. If you do not specify the username, audited logs of all databases are displayed for the target instance.

 |
        |**Connection IP Address**|The IP address of the client used to log on to the queried database. If you specify the client IP address, audited logs of the database that is logged on to on the specified client are displayed for the target instance. If you do not specify the client IP address, audited logs of all databases are displayed for the target instance.

 |
        |**Log Details**|The statement that was run and recorded in the audited logs. If you specify the keyword, audited logs that contain the specified keyword are displayed for the target instance. If you do not specify the keyword, audited logs of all databases are displayed for the target instance.

 |
        |**Time Consumed \(Microseconds\)**|The execution time of the statement.|
        |**Number of Returned Records**|The number of records returned after the statement was run.|
        |**Thread ID**|None|
        |**Execution Time**|The time when the statement was run.|

    -   Export File: You can export a file of audited logs.

        **Note:** If the number of statements in audited logs that meet the filtering conditions exceeds 1 million, only 1 million statements can be exported. Statements are exported at the speed of 900 rows per second. It takes about 20 minutes to export 1 million statements.

    -   File List: You can view a list of exported files of audited logs. [Table 2](#table_sbk_ch3_y2b) describes the parameters of the list.

        |Name|Description|
        |:---|:----------|
        |**File ID**|The ID automatically generated by the system for the file of audited logs.|
        |**Archiving Status**|The archiving status of the file of audited logs, including:         -   **Initializing**: indicates that the system has not started to export or is exporting the file of audited logs.
        -   **Success**: indicates that the system has successfully exported the file of audited logs.

**Note:** You can download files in the **Success** status only.

 |
        |**Audit Start Time**|The start time for exporting the file of audited logs.|
        |**Audit End Time**|The end time for exporting the file of audited logs.|
        |**Download**|The button that you click to download the file of audited logs to a local device.****|
        |**Log Size**|The size of the file of audited logs.|


## Specify audit settings {#section_wnl_fk3_y2b .section}

After log auditing is enabled for a replica set instance, you can specify the types of database operations to be audited.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **Audit Log**.
6.  Click **Audit Log Filter Setting**.
7.  In the Audit Log Filter Setting dialog box that appears, select the types of database operations to be audited.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6736/155617573237323_en-US.png)

    You can select the following database operations:

    -   admin: The O&M operation.
    -   slow: The slow query operation.
    -   query: The query operation.
    -   insert: The insert operation.
    -   update: The update operation.
    -   delete: The delete operation.
    -   command: The protocol commands, such as the aggregate method.
    **Note:** 

    -   If log auditing was enabled for instances before July 2018, the default types of database operations to be audited are admin, slow, insert, update, delete, and command. If you need to audit the query operation, you can select query in audit settings.
    -   If log auditing is enabled for instances after July 2018, the default types of database operations to be audited are admin, slow, query, insert, update, delete, and command.
8.  Click **OK**.

## Disable log auditing {#section_gwp_bd3_y2b .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Data Security** \> **Audit Log**.
6.  Click **Disable Audit Log**.

    **Note:** 

    -   After you disable log auditing, the CloudDBA index optimization feature is also disabled.
    -   After you disable log auditing, logs are no longer collected, subsequent database operations cannot be audited, and stored audited logs are also deleted.
7.  In the Disable Audit Log dialog box that appears, click **OK**.

