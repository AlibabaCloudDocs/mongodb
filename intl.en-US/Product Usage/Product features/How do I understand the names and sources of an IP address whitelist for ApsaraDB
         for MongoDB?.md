# How do I understand the names and sources of an IP address whitelist for ApsaraDB for MongoDB?

This topic describes the names and sources of an IP address whitelist for ApsaraDB for MongoDB. After you create an ApsaraDB for MongoDB instance, the instance has the default IP address whitelist. When you configure data migration or perform operations, more whitelists are generated.

![IP address whitelists](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3471166951/p69175.png)

**Note:** You can open the Whitelist Settings page by following the instructions provided in [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

|IP address whitelist name|Source|
|-------------------------|------|
|default|The default IP address whitelist, which cannot be deleted.|
|ddsdts|The IP address whitelist automatically generated when you migrate your ApsaraDB for MongoDB instance. It contains the IP addresses of DTS servers. **Note:** When you migrate data, do not delete this IP address whitelist. Otherwise, data migration fails. |

