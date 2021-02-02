# Unbind or delete a tag

When a tag is no longer needed in an ApsaraDB for MongoDB instance, you can unbind the tag from the instance. If the tag is not bound to any other instance, it will be deleted.

You must log on to the ApsaraDB for MongoDB console with your Alibaba Cloud account. RAM users do not have permissions to manage or use tags.

## Precautions

-   You can unbind up to 20 tags at a time.
-   When a tag is unbound from all instances, it is automatically deleted.
-   Unbinding a tag does not affect the normal operation of the instance. After all tags of an instance are unbound, the instance cannot be filtered by tag.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the instance. Choose **![More icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Edit tags** in the **Actions** column.

5.  In the dialog box that appears, click ![Delete](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6935298951/p67173.png).

    ![Delete a tag](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6935298951/p67191.png)

    **Note:** To delete a tag, unbind the tag from all instances.

6.  Click **OK**.


