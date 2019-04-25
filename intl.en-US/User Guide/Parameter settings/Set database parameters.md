# Set database parameters {#concept_547_r3z_xfb .concept}

ApsaraDB for MongoDB allows you to set part of database parameters based on your own requirements to adapt the features of ApsaraDB for MongoDB properly to your business.

## Notes {#section_ev3_b5h_yfb .section}

-   You can set database parameters for standalone and replica set instances, but not for sharded cluster instances.
-   You must modify parameter values within their respective value ranges specified in the console.
-   After you submit some parameters to be modified for an instance, the instance is automatically restarted. For more information, see the **Force Restart** column on the Parameter List page. Because an instance may be disconnected during a restart, you need to restart it with caution and make arrangements for business interruption.

## Procedure {#section_t4k_p5h_yfb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **Parameters** \> **Parameter List**.
6.  Click **Modify Parameter**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6738/155617727233193_en-US.png)

    **Note:** On the parameter list, you can view all parameters that you can modify, whether the instance needs to be restarted, and the effective rule for each parameter.

7.  On the Modify Parameter page that appears, modify parameters as required.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6738/155617727233192_en-US.png)

    You can modify multiple parameters in this step.

8.  Click **OK**.

