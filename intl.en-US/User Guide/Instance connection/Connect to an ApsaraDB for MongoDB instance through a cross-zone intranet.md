# Connect to an ApsaraDB for MongoDB instance through a cross-zone intranet {#concept_57139_zh .concept}

Currently, Alibaba Cloud intranets are classified into classic networks and VPCs. Cloud products, such as an ECS instance and an ApsaraDB for MongoDB instance, in different zones of the same region can be interconnected through an intranet.

This topic describes two scenarios.

## Connect an ECS instance to a new ApsaraDB for MongoDB instance {#section_mw3_b5w_fgb .section}

-   If the network type of the ECS instance is VPC and you purchase an ApsaraDB for MongoDB instance in a different zone of the same region, you need to ensure that the two instances have the same VPC ID. In addition, you need to create a VSwitch in the same zone as the ApsaraDB for MongoDB instance. In this way, the two instances can be interconnected properly through an intranet.
-   If the network type of the ECS instance is classic network and you purchase an ApsaraDB for MongoDB instance in a different zone of the same region, you need to ensure that the two instances are on the same classic network. In this way, they can be interconnected through a cross-zone intranet.

## Connect an ECS instance to an existing ApsaraDB for MongoDB instance {#section_v2b_25w_fgb .section}

The ECS instance and the ApsaraDB for MongoDB instance must be in the same region.

-   If the two instances are configured with the same network type \(either classic network or VPC with the same VPC ID\), they can be interconnected through an intranet.
-   If the two instances are configured with different network types, you can [switch the network type of the ApsaraDB for MongoDB instance](intl.en-US/User Guide/Network connection management/Switch the network type of an instance.md#) to be the same as that of the ECS instance before their interconnection.

    **Note:** You cannot switch the network type for standalone instances.


