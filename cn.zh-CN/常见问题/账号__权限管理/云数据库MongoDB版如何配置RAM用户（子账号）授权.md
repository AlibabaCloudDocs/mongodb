# 云数据库MongoDB版如何配置RAM用户（子账号）授权 {#concept_39932_zh .concept}

为细分账号权限，提升账号安全性，您可以通过[访问控制RAM](https://help.aliyun.com/document_detail/28627.html)（Resource Access Management）将MongoDB的管理权限授权给RAM用户（子账号），使用RAM用户管理MongoDB实例。

## RAM用户授权操作步骤 {#section_fn6_6td_7oj .section}

1.  登录[RAM管理控制台](https://ram.console.aliyun.com/)，创建RAM用户。详情请参见[创建RAM用户](https://help.aliyun.com/document_detail/28637.html)。
2.  在RAM控制台的左侧导航栏，单击**人员管理** \> **用户**。
3.  定位至创建的RAM用户，在**操作**列单击**添加权限**。

    ![添加授权](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6833/156410461248650_zh-CN.png)

4.  在添加权限对话框中，配置授权信息。

    ![配置授权信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6833/156410461248651_zh-CN.png)

    1.  在搜索框中输入**mongodb**，展现相关的系统权限策略。

        **说明：** 

        -   **AliyunMongoDBFullAccess**：为RAM用户授予MongoDB的完全管理权限。
        -   **AliyunMongoDBReadOnlyAccess**：为RAM用户授予MongoDB的只读访问权限。
    2.  根据业务需求，单击要授权的权限策略添加到已选择区域框中。
5.  单击**确定**并在授权结果对话框中单击**完成**。

## 自定义RAM授权策略 {#section_57r_45m_8n1 .section}

系统策略针对所有MongoDB资源进行RAM授权，您也可以根据业务需求自定义授权策略，仅向RAM用户授予指定实例的具体操作权限。关于自定义授权策略语法，请参见[Policy结构和语法](https://help.aliyun.com/document_detail/93739.html)。

**RAM授权MongoDB Resource的方式**

目前RAM对MongoDB进行授权的资源类型仅支持dbinstance（实例）一种。在通过RAM进行授权时，可以在策略的`Resource`字段中进行描述，资源的描述方式如下。

|资源类型|授权策略中的资源描述方式|
|:---|:-----------|
|dbinstance| -   acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid
-   acs:dds:$regionid:$accountid:dbinstance/
-   acs:dds:::dbinstance/

 |

**参数说明**

|参数名称|说明|
|----|--|
| ``` {#codeblock_isd_8z5_cdw}
$regionid
```

 |地域的ID，可以用`*`表示。|
| ``` {#codeblock_2lb_ai9_4ue}
$dbinstanceid
```

 |实例ID，可以用`*`表示。|
| ``` {#codeblock_s61_03e_4r2}
$accountid
```

 |云账号的数字ID，可以用`*`表示。|

**可授权的Action**

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

