# 使用DTS迁移单节点架构的自建MongoDB数据库上云 {#concept_rcw_511_kfb .concept}

本文介绍如何使用数据传输服务DTS（Data Transmission Service），将单节点架构的自建MongoDB数据库迁移至云数据库MongoDB中。DTS支持全量数据迁移和增量数据迁移，同时使用这两种迁移类型可以实现在不停服的情况下，平滑地完成数据库的迁移上云。

## 前提条件 {#section_tql_qpw_pgb .section}

-   自建MongoDB数据库的服务端口已开放至公网。
-   自建MongoDB数据库版本为3.0、3.2、3.4或3.6版本，暂不支持4.0版本。

    **说明：** 4.0版本的自建MongoDB数据库请参见[使用MongoDB工具迁移自建数据库上云](cn.zh-CN/单节点快速入门/数据迁移/使用MongoDB工具迁移自建数据库上云.md#)。

-   阿里云MongoDB实例的存储空间须大于自建MongoDB数据库占用的存储空间。

## 注意事项 {#section_a3z_x11_kfb .section}

-   为避免影响您的正常业务使用，请在业务低峰期进行数据迁移。
-   不支持迁移admin数据库，即使您将admin数据库选择为迁移对象，该库中的数据也不会被迁移。
-   config数据库属于系统内部数据库，如无特殊需求，请勿迁移该库。
-   单节点架构的自建MongoDB数据库，须开启oplog才可以使用增量数据迁移功能。详情请参见[增量数据迁移前的准备工作](#section_vqd_r51_dhb)。

## 费用说明 {#section_m3c_t5f_cgb .section}

|迁移类型|链路配置费用|公网流量费用|
|:---|:-----|:-----|
|全量数据迁移|不收取|不收取|
|增量数据迁移|收取，费用详情请参见[DTS产品定价](https://cn.aliyun.com/price/product#/dts/detail)。|不收取|

## 迁移类型说明 {#section_vax_ah2_vha .section}

-   全量数据迁移：将源MongoDB数据库迁移对象的存量数据全部迁移到目标MongoDB数据库中。

    **说明：** 支持database、collection、index的迁移。

-   增量数据迁移：在全量迁移的基础上，将源MongoDB数据库的增量更新数据同步到目标MongoDB数据库中。

    **说明：** 

    -   支持database、collection、index的新建和删除操作的同步。
    -   支持document的新增、删除和更新操作的同步。

## 数据库账号的权限要求 {#section_kvw_kb1_kfb .section}

|迁移数据源|全量数据迁移|增量数据迁移|
|:----|:-----|------|
|自建MongoDB数据库|待迁移库的read权限|待迁移库、admin库和local库的read权限|
|阿里云MongoDB数据库|目标库的readWrite权限|目标库的readWrite权限|

 **数据库账号创建及授权方法：** 

-   阿里云MongoDB实例请参见[使用DMS管理MongoDB数据库用户](../cn.zh-CN/用户指南/账号管理/使用DMS管理MongoDB数据库用户.md#)。
-   自建MongoDB数据库请参见[MongoDB Create User说明](https://docs.mongodb.com/manual/reference/method/db.createUser/)。

## 增量数据迁移前的准备工作 {#section_vqd_r51_dhb .section}

使用DTS进行增量数据迁移时，需要开启源数据库的oplog。如您仅需要全量数据迁移，可跳过本步骤。

**说明：** 该操作需要重启MongoDB服务，请在业务低峰期操作。

1.  使用Mongo Shell连接自建MongoDB数据库。
2.  使用下述命令关闭MongoDB服务。

    ``` {#codeblock_d6d_tqp_ek5}
    use admin
    db.shutdownServer()
    ```

3.  以副本集的方式在后台启动MongoDB服务。

    ``` {#codeblock_nit_3ed_hi4}
    mongod --port 27017 --dbpath /var/lib/mongodb --logpath /var/log/mongodb/mongod.log --replSet rs0 --bind_ip 0.0.0.0 --auth --fork
    ```

    **说明：** 

    -   该命令使用的数据库路径为/var/lib/mongodb，日志存储文件路径为/var/log/mongodb/mongod.log。您需要根据实际环境中的路径自行指定。
    -   该命令使用0.0.0.0作为MongoDB数据库服务的绑定地址，即允许所有IP地址访问该数据库。迁移结束后可使用`kill`命令结束该进程，然后以原有的配置文件启动MongoDB服务。
    -   该命令开启了认证功能，用户需要认证后才可以访问数据库。
4.  使用Mongo Shell连接自建MongoDB数据库。
5.  使用如下命令初始化副本集。

    ``` {#codeblock_g91_vyt_ll7}
    use admin
    rs.initiate()
    ```

6.  等待一段时间，当前节点的角色将转变为Primary。

    **说明：** 您可以通过`rs.printReplicationInfo()`命令查看oplog的状态信息。


## 操作步骤 {#section_njl_2c1_kfb .section}

1.  登录[数据传输控制台](https://dts.console.aliyun.com/)。
2.  在左侧导航栏，单击**数据迁移**。
3.  单击数据迁移页面右侧的**创建迁移任务**。
4.  配置迁移任务的**源库及目标库**信息。

    ![MongoDB迁移源目数据库配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6682/156159794134129_zh-CN.png)

    |类别|配置|说明|
    |:-|:-|:-|
    |任务名称|-|     -   DTS为每个任务自动生成一个任务名称，任务名称没有唯一性要求。
    -   您可以修改任务名称，建议为任务配置具有业务意义的名称，便于后续的任务识别。
 |
    |源库信息|实例类型|选择**有公网IP的自建数据库**。|
    |实例地区|当实例类型选择为**有公网IP的自建数据库**时，**实例地区**无需设置。 **说明：** 如果您的自建数据库配置了白名单安全类设置，您需要在**实例地区**配置项后，单击**获取DTS IP段**来获取DTS服务器的IP地址，并将获取到的IP地址加入自建数据库的白名单安全设置中。

 |
    |数据库类型|选择**MongoDB**。|
    |主机名或IP地址|填入自建MongoDB数据库的访问地址，本案例中填入公网地址。|
    |端口|填入自建MongoDB数据库的服务端口。|
    |数据库名称|填入鉴权数据库名称。|
    |数据库账号|填入自建MongoDB数据库的连接账号，权限要求请参见[数据库账号的权限要求](#section_kvw_kb1_kfb)。|
    |数据库密码|填入自建MongoDB数据库账号对应的密码。 **说明：** 源库信息填写完毕后，您可以单击**数据库密码**后的**测试连接**来验证填入的源库信息是否正确。源库信息填写正确则提示**测试通过**，如提示**测试失败**，单击**测试失败**后的**诊断**，根据提示调整填写的源库信息。

 |
    |目标库信息|实例类型|选择**MongoDB实例**。|
    |实例地区|选择目标MongoDB实例所在地域。|
    |MongoDB实例ID|选择目标MongoDB实例ID。|
    |数据库名称|填入鉴权数据库名称。|
    |数据库账号|填入连接目标MongoDB实例数据库的账号，权限要求请参见[数据库账号的权限要求](#section_kvw_kb1_kfb)。|
    |数据库密码|填入连接目标MongoDB实例数据库账号对应的密码。 **说明：** 目标库信息填写完毕后，您可以单击**数据库密码**后的**测试连接**来验证填入的目标库信息是否正确。目标库信息填写正确则提示**测试通过**，如提示**测试失败**，单击**测试失败**后的**诊断**，根据提示调整填写的目标库信息。

 |

5.  配置完成后，单击页面右下角的**授权白名单并进入下一步**。

    **说明：** 此步骤会将DTS服务器的IP地址自动添加到目标MongoDB实例的白名单中，用于保障DTS服务器能够正常连接目标MongoDB实例。迁移完成后如不再需要可手动删除，详情请参见[白名单设置](cn.zh-CN/副本集快速入门/设置白名单.md#)。

6.  选择迁移对象及迁移类型。

    ![MongoDB迁移对象迁移类型选择](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6682/156159794138327_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |迁移类型|     -   如果只需要进行全量迁移，则勾选**全量数据迁移**。

**说明：** 为保障数据一致性，全量数据迁移期间请勿在自建MongoDB数据库中写入新的数据。

    -   如果需要进行不停机迁移，则同时选择**全量数据迁移**和**增量数据迁移**。

**说明：** 单节点架构的自建MongoDB数据库，须提前开启oplog才可以使用增量数据迁移功能，详情请参见[增量数据迁移前的准备工作](#section_vqd_r51_dhb)。

 |
    |迁移对象|     -   在**迁移对象**框中将想要迁移的数据库选中，单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79929/156159794140698_zh-CN.png)移动到**已选择对象**框。

**说明：** 

        -   不支持迁移admin数据库，即使您将admin数据库选择为迁移对象，该库中的数据也不会被迁移。
        -   config数据库属于系统内部数据库，如无特殊需求，请勿迁移config数据库。
    -   迁移对象选择的粒度为database、collection/function。
    -   默认情况下，迁移完成后，迁移对象的名称保持不变。如果您需要迁移对象在目标数据库中的名称不同，那么需要使用DTS提供的对象名映射功能。使用方法请参见[库表列映射](https://help.aliyun.com/document_detail/26628.html)。
 |

7.  上述配置完成后，单击页面右下角的**预检查并启动**。

    **说明：** 

    -   在迁移任务正式启动之前，会先进行预检查。只有预检查通过后，才能成功启动迁移任务。
    -   如果预检查失败，单击具体检查项后的![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/140110/156159794150068_zh-CN.png)，查看具体的失败详情。根据失败原因修复后，重新进行预检查。
8.  预检查通过后，单击**下一步**。
9.  在购买配置确认页面，选择**链路规格**并勾选**数据传输（按量付费）服务条款**。
10. 单击**购买并启动**，迁移任务正式开始。
    -   全量数据迁移

        请勿手动停止迁移任务，否则可能会导致数据不完整。您只需等待迁移任务完成即可，迁移任务会自动停止。

    -   增量数据迁移

        增量数据迁移迁移任务不会自动结束，需要手动结束迁移任务。

        **说明：** 请选择合适的时间手动结束迁移任务，例如业务低峰期或准备将业务切换至MongoDB实例时。

        1.  观察迁移任务的进度变更为**增量迁移**，并显示为**无延迟**状态时，将源库停写几分钟，此时**增量迁移**的状态可能会显示延迟的时间。
        2.  等待再次进入**无延迟**状态，手动停止迁移任务。

            ![MongoDB增量迁移无延迟](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75938/156159794133674_zh-CN.png)

11. 将业务切换至阿里云MongoDB实例。

## 更多信息 {#section_v5g_lrw_pgb .section}

 [通过Mongo Shell登录MongoDB单节点实例](cn.zh-CN/单节点快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#) 

