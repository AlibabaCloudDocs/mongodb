# Configure database parameters for an ApsaraDB for MongoDB instance

This topic describes how to configure database parameters for an ApsaraDB for MongoDB instance to better fit your business needs.

## Prerequisites

The instance is a standalone or replica set instance.

## Precautions

After you save the changes to some parameters, the instance is restarted. For more information, see descriptions in the **Force Restart** column on the Parameter List page.

**Note:** While the instance is restarting, it is not connected. We recommend that you restart your instance during off-peak hours to minimize the impact on your business.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **Parameters** \> **Parameter List**.

6.  Click **Modify Parameter**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7345298951/p33193.png)

    **Note:** On the parameter list, you can check whether the instance needs to be restarted after you modify a parameter.

7.  In the **Modify Parameter** dialog box, modify the parameters.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8345298951/p33192.png)

    **Note:**

    -   You can modify more than one parameter in this step.
    -   You must configure parameters in compliance with the value ranges displayed in the console.
8.  Click **OK**.


