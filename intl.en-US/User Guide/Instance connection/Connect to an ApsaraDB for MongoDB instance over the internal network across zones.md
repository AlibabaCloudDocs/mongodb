# Connect to an ApsaraDB for MongoDB instance over the internal network across zones

Alibaba Cloud provides two internal network types: the classic network and VPCs. An ECS instance and an ApsaraDB for MongoDB instance in different zones of the same region can be interconnected over the internal network.

This topic describes two scenarios.

## Connect an ECS instance to a new ApsaraDB for MongoDB instance

-   If the network type of the ECS instance is VPC and you purchase an ApsaraDB for MongoDB instance in a different zone of the same region, you must ensure that the two instances have the same VPC ID. In addition, you must create a vSwitch in the zone where the ApsaraDB for MongoDB instance is deployed. Then the two instances can be interconnected properly over the internal network.
-   If the network type of the ECS instance is classic network and you purchase an ApsaraDB for MongoDB instance in a different zone of the same region, the two instances can be interconnected properly over the internal network because they are in the same region.

## Connect an ECS instance to an existing ApsaraDB for MongoDB instance

The ECS instance and ApsaraDB for MongoDB instance must be in the same region.

-   If both the ECS instance and ApsaraDB for MongoDB instance have the same network type \(\), they can be interconnected properly over the internal network.

    **Note:** The network type of both instances is classic network or VPC. If the network type is VPC, both instances must have the same VPC ID.

-   If the two instances have different network types, you can change the network type of the ApsaraDB for MongoDB instance to be the same as that of the ECS instance before connecting them. For more information, see [Switch the network type of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md).

    **Note:** You cannot switch the network type for standalone instances.


