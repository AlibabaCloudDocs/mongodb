# Best practices for data security of ApsaraDB for MongoDB

ApsaraDB for MongoDB provides comprehensive security protection to eliminate your data security concerns. You can guarantee database data security by using zone-disaster recovery, RAM authorization, audit logs, network isolation, whitelists, or password authentication.

## Zone-disaster recovery

ApsaraDB for MongoDB provides a zone-disaster recovery solution for replica set instances to meet the high reliability and data security requirements in business scenarios. This solution deploys the nodes of a replica set instance or the components of a sharded cluster instance in three different [zones](~~26559~~). When one of the three zones loses communication due to force majeure factors such as power failure or network failure, the high-availability system automatically triggers a switchover.

You can select multiple zones when you create an instance. For more information, see [Create a multi-zone replica set instance](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone replica set instance.md) or [Create a multi-zone sharded cluster instance](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone sharded cluster instance.md). You can also migrate a replica set instance to multiple zones. For more information, see [Migrate an ApsaraDB for MongoDB instance across zones in the same region](/intl.en-US/User Guide/Instance management/Migrate an ApsaraDB for MongoDB instance across zones in the same region.md).

## Access control

-   Authorize a RAM user to manage ApsaraDB for MongoDB instances

    Resource Access Management \(RAM\) allows you to create and manage RAM users and control their permissions on resources of your Alibaba Cloud account. If multiple users in your enterprise need to use the resource at the same time, you can use RAM to assign least permissions to them and avoid the need to share the key of your Alibaba Cloud account. This reduces information security risks for your enterprise.

    For more information, see [How to configure RAM user permissions on ApsaraDB for MongoDB](/intl.en-US/Product Usage/Account and permission management/How to configure RAM user permissions on ApsaraDB for MongoDB.md).

-   Create and authorize a database user

    Do not connect to a database as the root user in the production environment. You can create database users and grant permissions to them.

    For more information, see [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md).


## Network isolation

-   Use VPCs

    ApsaraDB for MongoDB supports multiple network types. We recommend that you use VPCs.

    A VPC is an isolated virtual network with higher security and better performance than the classic network. You must create the VPC in advance. For more information, see [Create a default Virtual Private Cloud \(VPC\) network and VSwitch](~~65402~~).

    If an ApsaraDB for MongoDB instance is deployed in the classic network, you can switch the network type of the instance to VPC. For more information, see [Switch the network type of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md). If your ApsaraDB for MongoDB instance is deployed in a VPC, no further action is required.

    **Note:** ApsaraDB for MongoDB supports password-free access over a VPC. VPCs provide a convenient and secure way to connect to databases. For more information, see [Enable or disable password-free access for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Enable or disable password-free access for an ApsaraDB for MongoDB instance.md).

-   Set the whitelist

    By default, after an ApsaraDB for MongoDB instance is created, the IP address in its whitelist is `127.0.0.1`. You must manually set the IP address in the whitelist before you connect to MongoDB databases.

    For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

    **Note:**

    -   Do not include `0.0.0.0/0` in the whitelist, which indicates that the database can be accessed from all IP addresses.
    -   We recommend that you set the whitelist based on your business needs and remove IP addresses that are no longer needed from the whitelist on a regular basis.

## Log audit

Audit logs of ApsaraDB for MongoDB record all operations that you perform on databases. Audit logs allow you to obtain data execution information by performing fault analysis, behavior analysis, and security audit on databases.

For more information, see [Configure audit logging for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Audit logs (previous version)/Configure audit logging for an ApsaraDB for MongoDB instance.md).

## Data encryption

-   SSL encryption

    If you connect to a database over the Internet, you can enable Secure Sockets Layer \(SSL\) encryption to improve the security of data links. SSL encryption can encrypt network connections at the transport layer. This improves data security and ensures data integrity. For more information, see [Use the mongo shell to connect to an ApsaraDB for MongoDB database in SSL encryption mode](/intl.en-US/User Guide/Data security/Use the mongo shell to connect to an ApsaraDB for MongoDB database in SSL encryption mode.md).

-   TDE

    Transparent Data Encryption \(TDE\) implements real-time I/O encryption and decryption for data files. TDE encrypts data before data is written to a disk and decrypts data before data is read from the disk. TDE does not increase the size of data files. You can use TDE without modifying your application that uses ApsaraDB for MongoDB. For information, see [Configure TDE for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure TDE for an ApsaraDB for MongoDB instance.md).

    **Note:** You can enable and disable TDE only for a collection. For information about encryption at the field level, visit [Explicit \(Manual\) Client-Side Field Level Encryption](https://docs.mongodb.com/manual/core/security-explicit-client-side-encryption/). Field level encryption supports only MongoDB 4.2 instances.


