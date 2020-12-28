# 云数据库MongoDB版如何配置RAM用户（子账号）授权

为细分账号权限，提升账号安全性，您可以通过访问控制RAM（Resource Access Management）将MongoDB的管理权限授权给RAM用户（子账号），使用RAM用户管理MongoDB实例。

## RAM用户授权操作步骤

1.  云账号登录[RAM控制台](https://ram.console.aliyun.com/)。
2.  [创建RAM用户](/intl.zh-CN/用户管理/创建RAM用户.md)。
3.  在左侧导航栏的**人员管理**菜单下，单击**用户**。
4.  在**用户登录名称/显示名称**列表下，找到目标RAM用户。
5.  单击**添加权限**。

    ![添加授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6874797951/p48650.png)

6.  在添加权限对话框中，配置授权信息。

    ![配置授权信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6874797951/p48651.png)

    1.  在搜索框中输入**mongodb**，展现相关的系统权限策略。

        **说明：**

        -   **AliyunMongoDBFullAccess**：为RAM用户授予MongoDB的完全管理权限。
        -   **AliyunMongoDBReadOnlyAccess**：为RAM用户授予MongoDB的只读访问权限。
    2.  根据业务需求，单击要授权的权限策略添加到已选择区域框中。
7.  单击**确定**。
8.  单击**完成**。

## 自定义RAM授权策略

系统策略针对所有MongoDB资源进行RAM授权，您也可以根据业务需求自定义授权策略，仅向RAM用户授予指定实例的具体操作权限。关于自定义授权策略语法，请参见[Policy结构和语法](~~93739~~)。

RAM授权MongoDB Resource的方式

目前RAM对MongoDB进行授权的资源类型仅支持dbinstance（实例）一种。在通过RAM进行授权时，可以在策略的`Resource`字段中进行描述，资源的描述方式如下。

|资源类型|授权策略中的资源描述方式|
|:---|:-----------|
|dbinstance|-   acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid
-   acs:dds:$regionid:$accountid:dbinstance/
-   acs:dds:::dbinstance/ |

参数说明

|参数名称|说明|
|----|--|
|```
$regionid
```

|地域的ID，可以用`*`表示。|
|```
$dbinstanceid
```

|实例ID，可以用`*`表示。|
|```
$accountid
```

|云账号的数字ID，可以用`*`表示。|

可授权的Action

在RAM中，可以对一个MongoDB资源进行以下Action的授权。

|Action|功能描述|
|:-----|:---|
|CreateDBInstance|创建实例|
|ModifyDBInstanceSpec|变更实例配置|
|DeleteDBInstance|删除实例|
|DescribeDBInstances|查询实例|
|RestartDBInstance|重启实例|
|DescribeSecurityIps|查询白名单|
|ModifySecurityIps|修改白名单|
|ResetAccountPassword|重置密码|
|DescribeBackupPolicy|查询备份策略|
|ModifyBackupPolicy|修改备份策略|
|CreateBackup|创建备份|
|RestoreDBInstance|恢复实例|
|DescribeAccounts|查询账号信息|
|DescribeDBInstancePerformance|查询实例状态|
|DescribeReplicaSetRole|查询实例主从属性|
|ModifyDBInstanceDescription|修改实例描述|
|ModifyAccountDescription|修改账号信息|
|DescribeDBInstanceAttribute|查询实例属性|
|RenewDBInstance|续费实例|
|ModifyDBInstanceNetworkType|修改实例网络类型|

