# Modify a public or internal endpoint of an ApsaraDB for MongoDB instance

This topic describes how to modify the public and internal endpoints of an ApsaraDB for MongoDB instance in the ApsaraDB for MongoDB console.

## Limits

|Instance|Limit|
|--------|-----|
|Standalone instances|You can only modify the public and internal endpoints of a primary node.|
|Replica set instances|You can modify the public and internal endpoints of both primary and secondary nodes.|
|Sharded cluster instances|You can only modify the public and internal endpoints of a mongos.|

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  In the **Intranet Connection** or **Public IP Connection** section, click **Update Connection String**.

7.  In the dialog box that appears, enter a new endpoint.

    ![Enter a new endpoint](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5045298951/p66853.png)

    **Note:**

    -   You can only modify the prefix of the endpoint.
    -   The new endpoint must be 8 to 64 characters in length and can contain lowercase letters, digits, and hyphens \(-\). It must start with a lowercase letter and end with a lowercase letter or digit.
8.  Click **Submit**.


After you modify the public or internal endpoint, you must connect a client or an application to your ApsaraDB for MongoDB instance by using the new endpoint.

