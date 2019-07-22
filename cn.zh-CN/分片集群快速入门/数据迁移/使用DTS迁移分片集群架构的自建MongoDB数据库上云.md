# 使用DTS迁移分片集群架构的自建MongoDB数据库上云 {#concept_fdj_twz_zfb .concept}

本文介绍如何使用数据传输服务DTS（Data Transmission Service），依次将本地MongoDB分片集群数据库中的各个Shard节点，迁移至阿里云MongoDB分片集群实例来实现迁移上云。通过DTS的增量迁移功能，可以实现在本地应用不停服的情况下，平滑完成数据库的迁移上云。

## 迁移原理介绍 {#section_egp_cs5_23b .section}

DTS通过迁移分片集群中的每个Shard节点来实现分片集群数据库的整体迁移，您需要为每个Shard节点创建一个对应的数据迁移任务。

**说明：** 数据在目标MongoDB实例中的分布取决于您设置的片键，详情请参见[设置数据分片以充分利用Shard性能](../intl.zh-CN/最佳实践/设置数据分片以充分利用Shard性能.md#)。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156376374950227_zh-CN.png)

## 前提条件 {#section_jx1_5wy_ngb .section}

-   自建数据库中，各Shard节点的服务端口已开放至公网。
-   自建MongoDB数据库版本为3.0、3.2、3.4、3.6或4.0版本。
-   确保目标分片集群实例中的Shard节点具备充足的存储空间。

    **说明：** 例如自建数据库中有三个Shard节点，其中第二个Shard节点占用的存储空间最多（500GB），那么分片集群实例中的每个Shard节点的存储空间均需要大于500GB。


## 注意事项 {#section_dww_lmr_zfb .section}

-   为避免影响您的正常业务使用，请在业务低峰期进行数据迁移。
-   不支持迁移admin数据库，即使您将admin数据库选择为迁移对象，该库中的数据也不会被迁移。
-   config数据库属于系统内部数据库，如无特殊需求，请勿迁移该库。
-   MongoDB实例支持的版本与存储引擎请参见[版本及存储引擎](../intl.zh-CN/产品简介/版本及存储引擎.md#)，如需跨版本或跨引擎迁移，请提前确认兼容性。

## 费用说明 {#section_brm_q21_1gb .section}

|迁移类型|链路配置费用|公网流量费用|
|:---|:-----|:-----|
|全量数据迁移|不收取|不收取|
|增量数据迁移|收取，费用详情请参见[数据传输服务DTS定价](https://www.alibabacloud.com/zh/product/data-transmission-service/pricing)。|不收取|

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

-   阿里云MongoDB实例请参见[使用DMS管理MongoDB数据库用户](../intl.zh-CN/用户指南/账号管理/使用DMS管理MongoDB数据库用户.md#)。
-   自建MongoDB数据库请参见[MongoDB Create User说明](https://docs.mongodb.com/manual/reference/method/db.createUser/)。

## 迁移前准备工作 {#section_pcx_yhs_zfb .section}

1.  关闭本地MongoDB数据库的均衡器，详情请参见[关闭Mongodb分片集群均衡器](../intl.zh-CN/最佳实践/管理MongoDB均衡器Balancer.md#section_k3j_4wl_2gb) 。
2.  清除本地MongoDB数据库中，因块迁移失败产生的孤立文档。

    示例：

    在某个shard节点中执行下述命令，清除test数据库中user集合的所有孤立文档。

    ``` {#codeblock_6lk_28q_7j0 .language-javascript}
    var nextKey = { };
    var result;
    
    while ( nextKey != null ) {
      result = db.adminCommand( { cleanupOrphaned: "test.user", startingFromKey: nextKey } );
    
      if (result.ok != 1)
         print("Unable to complete at this time: failure or timeout.")
    
      printjson(result);
    
      nextKey = result.stoppedAtKey;
    }
    ```

    **说明：** 

    -   您需要将示例中`test.user`的替换为真实的数据库名和集合名。
    -   该操作需要在每个Shard节点中执行。
    -   如果未清除孤立文档，可能在迁移过程会遇到\_id冲突的文档，导致迁移错误的数据，并且影响迁移的性能。
3.  根据业务需要，在目标MongoDB实例中创建需要分片的数据库和集合，并配置数据分片，详情请参见[设置数据分片以充分利用Shard性能](../intl.zh-CN/最佳实践/设置数据分片以充分利用Shard性能.md#)。

    **说明：** 在配置数据迁移前配置数据分片，可避免数据被迁移至同一Shard中，导致单个Shard使用的存储空间超出预期规划。


## 操作步骤 {#section_lnt_knr_zfb .section}

1.  登录[数据传输控制台](https://dts-intl.console.aliyun.com/)。
2.  在左侧导航栏，单击**数据迁移**。
3.  在迁移任务列表页面顶部，选择目标MongoDB实例所属地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6682/156376374950190_zh-CN.png)

4.  单击右上角的**创建迁移任务**。
5.  配置迁移任务的源库及目标库信息。

    ![配置源库和目标库信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6682/156376375034129_zh-CN.png)

    |类别|配置|说明|
    |:-|:-|:-|
    |任务名称|-|     -   DTS为每个任务自动生成一个任务名称，任务名称没有唯一性要求。
    -   您可以修改任务名称，建议为任务配置具有业务意义的名称，便于后续的任务识别。
 |
    |源库信息|实例类型|选择**有公网IP的自建数据库**。|
    |实例地区|当实例类型选择为**有公网IP的自建数据库**时，**实例地区**无需设置。 **说明：** 如果您的自建数据库配置了白名单安全类设置，您需要在**实例地区**配置项后，单击**获取DTS IP段**来获取DTS服务器的IP地址，并将获取到的IP地址加入自建数据库的白名单安全设置中。

 |
    |数据库类型|选择**MongoDB**。|
    |主机名或IP地址|填入自建MongoDB数据库中，单个Shard节点的域名或IP地址，本案例填入公网IP地址。 **说明：** DTS通过依次迁移分片集群中的每个Shard节点来实现整体迁移，此处先填入第一个Shard节点的域名或IP地址，稍后创建第二个迁移任务时，此处填入第二个Shard节点的域名或IP地址。以此类推，直至迁移所有Shard节点。

 |
    |端口|填入自建MongoDB数据库的服务端口。|
    |数据库名称|填入鉴权数据库名称。|
    |数据库账号|填入自建MongoDB数据库的连接账号，权限要求请参见[数据库账号的权限要求](#section_kvw_kb1_kfb)。|
    |数据库密码|填入自建MongoDB数据库账号对应的密码。 **说明：** 源库信息填写完毕后，您可以单击**数据库密码**后的**测试连接**来验证填入的源库信息是否正确。源库信息填写正确则提示**测试通过**，如提示**测试失败**，单击**测试失败**后的**诊断**，根据提示调整填写的源库信息。

 |
    |目标库信息|实例类型|选择**MongoDB实例**。|
    |实例地区|选择目标MongoDB实例所在地域。|
    |MongoDB实例ID|选择目标MongoDB实例ID，本案例选择为分片集群实例。|
    |数据库名称|填入鉴权数据库名称。|
    |数据库账号|填入连接目标MongoDB实例的数据库账号，权限要求请参见[数据库账号的权限要求](#section_kvw_kb1_kfb)。|
    |数据库密码|填入连接目标MongoDB实例的数据库账号对应的密码。 **说明：** 目标库信息填写完毕后，您可以单击**数据库密码**后的**测试连接**来验证填入的目标库信息是否正确。目标库信息填写正确则提示**测试通过**，如提示**测试失败**，单击**测试失败**后的**诊断**，根据提示调整填写的目标库信息。

 |

6.  配置完成后，单击页面右下角的**授权白名单并进入下一步**。

    **说明：** 此步骤会将DTS服务器的IP地址自动添加到目标MongoDB实例的白名单中，用于保障DTS服务器能够正常连接目标MongoDB实例。迁移完成后如不再需要可手动删除，详情请参见[白名单设置](../intl.zh-CN/用户指南/数据安全性/设置白名单.md#)。

7.  选择**迁移对象**和**迁移类型**。

    ![选择迁移对象和迁移类型](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156376375034699_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |迁移类型|     -   如果只需要进行全量迁移，则勾选**全量数据迁移**。

**说明：** 为保障数据一致性，全量数据迁移期间请勿在自建MongoDB数据库中写入新的数据。

    -   如果需要进行不停机迁移，则同时勾选**全量数据迁移**和**增量数据迁移**。
 |
    |迁移对象|     -   在**迁移对象**框中单击待迁移的对象，然后单击![向右箭头](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79929/156376375040698_zh-CN.png)移动到**已选择对象**框。

**说明：** 

        -   不支持迁移admin数据库，即使您将admin数据库选择为迁移对象，该库中的数据也不会被迁移。
        -   config数据库属于系统内部数据库，如无特殊需求，请勿迁移config数据库。
    -   迁移对象选择的粒度为database、collection/function。
    -   默认情况下，迁移完成后，迁移对象的名称保持不变。如果您需要迁移对象在目标数据库中的名称不同，那么需要使用DTS提供的对象名映射功能。使用方法请参见[库表列映射](https://help.aliyun.com/document_detail/26628.html)。
 |

8.  上述配置完成后，单击页面右下角的**预检查并启动**。

    **说明：** 

    -   在迁移任务正式启动之前，会先进行预检查。只有预检查通过后，才能成功启动迁移任务。
    -   如果预检查失败，单击具体检查项后的![提示](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/140110/156376375050068_zh-CN.png)，查看失败详情。根据失败原因修复后，重新进行预检查。
9.  预检查通过后，单击**下一步**。
10. 在**购买配置确认**页面，选择**链路规格**并勾选**数据传输（按量付费）服务条款**。
11. 单击**购买并启动**，迁移任务正式开始。
12. 重复第1步到第11步的操作，为剩余的Shard节点创建迁移任务。
13. 完成迁移任务。
    -   全量数据迁移

        请勿手动结束迁移任务，否则可能会导致数据不完整。您只需等待迁移任务完成即可，迁移任务会自动结束。

    -   增量数据迁移

        迁移任务不会自动结束，需要手动结束迁移任务。

        **说明：** 请选择合适的时间手动结束迁移任务，例如业务低峰期或准备将业务切换至MongoDB实例时。

        1.  等待所有Shard节点的迁移任务的进度变更为**增量迁移**，并显示为**无延迟**状态时，将源库停写几分钟，此时**增量迁移**的状态可能会显示延迟的时间。
        2.  等待所有Shard节点迁移任务的**增量迁移**再次进入**无延迟**状态后，手动结束迁移任务。

            ![结束迁移任务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80861/156376375034689_zh-CN.png)

14. 将业务切换至阿里云MongoDB实例。

