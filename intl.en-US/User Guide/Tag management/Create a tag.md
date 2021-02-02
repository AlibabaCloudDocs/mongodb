# Create a tag

You can create and bind multiple tags to a large number of instances to classify and filter instances by tag.

You must log on to the ApsaraDB for MongoDB console with your Alibaba Cloud account. RAM users do not have permissions to manage or use tags.

## Precautions

-   A tag consists of a key-value pair. The key must be unique in the same region of the same account, while the value is not limited.

    **Note:** A key can have zero to multiple values.

-   You can edit tags for a maximum of 50 instances at a time.
-   You can bind up to 20 tags to each instance.
-   You can bind or unbind up to 20 tags at a time.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  To create a tag, perform the following steps:

    -   Create tags for an instance: Find the instance. Choose **![More icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9545298951/p13851.png)** \> **Edit tags** in the **Actions** column.

        ![Create tags for an instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4935298951/p67128.png)

    -   Create tags for multiple instances: Select the instances for which you want to create tags and then click **Edit tags** at the lower part of the page.

        ![Create tags for multiple instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4935298951/p67129.png)

5.  In the dialog box that appears, click **Create**.

    **Note:** If you have created tags, click **Available Tags** to bind the tags to the instances. For more information, see [Bind existing tags](/intl.en-US/User Guide/Tag management/Bind existing tags.md).

6.  Set the key and value of the tag and then click **Ok**.

    ![Edit tags](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2935298951/p67130.png)

7.  Repeat the preceding steps to create all the tags. Then click **OK** in the lower-right corner of the dialog box.

    **Note:** After you create tags, you can bind them to other instances.


After you create a tag, you can view the tag information of the instance in the instance list.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2935298951/p67179.png)

