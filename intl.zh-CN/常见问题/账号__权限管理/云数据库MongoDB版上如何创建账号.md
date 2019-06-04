# 云数据库MongoDB版上如何创建账号 {#concept_vmn_5sc_lfb .concept}

当实例创建完成后，云数据库MongoDB版默认为用户在admin数据库中创建了一个root账号，拥有MongoDB内置的root权限。通过root账号登录数据库后，您可以根据业务需求，创建用户并分配权限。

通过`db.createUser()`命令创建账号，详情请参见[db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/index.html)。

