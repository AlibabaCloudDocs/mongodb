# How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions

If an ECS instance and an ApsaraDB for MongoDB instance are in different regions, you can use the methods described in this topic to quickly connect the ECS instance to the ApsaraDB for MongoDB instance.

## Method 1: Migrate the ApsaraDB for MongoDB instance to the region where the ECS instance is located

This method uses the data migration feature of [What is DTS?]() \(DTS\) to migrate the ApsaraDB for MongoDB instance to the region where the ECS instance is located. For example, you can migrate a MongoDB instance from China \(Qingdao\) to China \(Hangzhou\).

1.  Create an ApsaraDB for MongoDB instance in the region where the ECS instance is located. For more information, see [Create an instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md). Skip this step if you have already created an ApsaraDB for MongoDB instance.
2.  Migrate the MongoDB database from the instance in the source region to the instance in the destination region. For more information, see [Migrate the data of an ApsaraDB for MongoDB instance across regions](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate the data of an ApsaraDB for MongoDB instance across regions.md).
3.  Add the private IP address of the ECS instance to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

    **Note:** For more information about how to obtain the IP address of an ECS instance, see [How to query the IP address of an ECS instance](https://www.alibabacloud.com/help/zh/doc-detail/40637.htm#section-vpl-qbg-qgb).


## Method 2: Migrate the ECS instance to the region where the ApsaraDB for MongoDB instance is located

You can use the custom image feature or the migration tool to migrate the ECS instance data from the original region to the region where the ApsaraDB for MongoDB instance is located. For example, you can migrate the ECS instance from the China \(Qingdao\) region to the China \(Hangzhou\) region.

-   Create a custom image from the ECS instance and then create an ECS instance in the region where the ApsaraDB for MongoDB instance is located from the custom image \(this method is recommended\).
    1.  [Create a custom image from the ECS instance](~~35109~~).
    2.  Copy the created custom image to the region where the ApsaraDB for MongoDB instance is located. For more information, see [Copy an image](~~25462~~).
    3.  [Create an ECS instance from the custom image](~~25465~~).

        **Note:** When creating the ECS instance, select the same VPC as the ApsaraDB for MongoDB instance.

    4.  Add the private IP address of the ECS instance to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

        **Note:** For more information about how to obtain the IP address of an ECS instance, see [How to query the IP address of an ECS instance](https://www.alibabacloud.com/help/zh/doc-detail/40637.htm#section-vpl-qbg-qgb).

-   Use the migration tool to migrate the ECS instance to the region where the ApsaraDB for MongoDB instance is located.
    1.  Migrate the ECS instance to the region where the ApsaraDB for MongoDB instance is located. For more information, see [Migrate ECS instances](~~100988~~).
    2.  Add the private IP address of the ECS instance to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

