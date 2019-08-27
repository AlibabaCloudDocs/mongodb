# 使用DTS将腾讯云MongoDB增量迁移至阿里云 {#concept_645293 .concept}

本文介绍如何使用数据传输服务DTS（Data Transmission Service），将腾讯云MongoDB副本集实例增量迁移至阿里云。DTS支持全量数据迁移和增量数据迁移，同时使用这两种迁移类型可以实现在不停服的情况下，平滑地完成腾讯云MongoDB数据库的迁移。

## 背景信息 {#section_kp5_4jl_qsf .section}

当您因业务调整或需要使用阿里云MongoDB特性功能时，您可以使用DTS工具，通过**增量数据迁移**方法，将3.6版本的腾讯云MongoDB副本集实例迁移至阿里云MongoDB实例。

## 前提条件 {#section_d74_hkx_h7o .section}

-   腾讯云MongoDB副本集实例的数据库版本为3.6版本。

    **说明：** 关于3.2版本的腾讯云MongoDB副本集实例和分片集群实例的迁移方法，请参见[使用MongoDB工具将腾讯云MongoDB迁移至阿里云](cn.zh-CN/用户指南/数据迁移__同步/第三方云迁移到阿里云/使用MongoDB工具将腾讯云MongoDB迁移至阿里云.md#)。

-   已创建阿里云MongoDB实例。如果尚未创建，请参见[创建副本集实例](../cn.zh-CN/副本集快速入门/创建副本集实例.md#)或[创建分片集群实例](../cn.zh-CN/分片集群快速入门/创建分片集群实例.md#)。

    **说明：** 阿里云MongoDB实例的存储空间应大于腾讯云MongoDB副本集实例已使用的存储空间。如果创建的阿里云MongoDB实例存储空间过低，您需要升级存储空间，详情请参见[变更配置](cn.zh-CN/用户指南/实例管理/变更配置.md#)。

-   如需迁移至阿里云MongoDB分片集群实例，建议对数据进行分片以更好地发挥性能，详情请参见[设置数据分片](../cn.zh-CN/最佳实践/设置数据分片以充分利用Shard性能.md#)。

## 注意事项 {#section_3dv_46s_fs8 .section}

-   为避免影响您的业务使用，请在业务低峰期进行数据迁移操作。
-   对于迁移失败的任务，DTS会触发自动恢复。当您需要将业务切换至目标实例时，请务必先结束或释放该任务，避免该任务被自动恢复后，导致源端数据覆盖目标实例的数据。
-   不支持迁移admin数据库，即使您将admin数据库选择为迁移对象，该库中的数据也不会被迁移。
-   阿里云MongoDB实例支持的版本与存储引擎请参见[版本及存储引擎](../cn.zh-CN/产品简介/版本及存储引擎.md#)，如需跨版本或跨引擎迁移，请提前确认兼容性。

## 费用说明 {#section_o7d_vds_7ta .section}

|迁移类型|链路配置费用|公网流量费用|
|:---|:-----|:-----|
|全量数据迁移|不收取|不收取|
|增量数据迁移|收取，费用详情请参见[数据传输服务DTS定价](https://cn.aliyun.com/price/product#/dts/detail)。|不收取|

## 迁移类型说明 {#section_kg3_ye2_9pm .section}

-   全量数据迁移：将源MongoDB数据库迁移对象的存量数据全部迁移到目标MongoDB数据库中。

    **说明：** 支持database、collection、index的迁移。

-   增量数据迁移：在全量迁移的基础上，将源MongoDB数据库的增量更新数据同步到目标MongoDB数据库中。

    **说明：** 

    -   支持database、collection、index的新建和删除操作的同步。
    -   支持document的新增、删除和更新操作的同步。

## 迁移权限要求 {#section_9ub_nay_9yo .section}

|实例类型|全量数据迁移|增量数据迁移|
|:---|:-----|:-----|
|腾讯云MongoDB副本集实例|待迁移库的read权限|待迁移库、admin库和local库的read权限|
|阿里云MongoDB实例|目标库的readWrite权限|目标库的readWrite权限|

## 迁移前准备工作 {#section_e8n_jwq_uwg .section}

由于腾讯云MongoDB实例只有内网连接地址，没有公网连接地址。此时需要创建一个具有公网地址的腾讯云服务器用作端口数据转发，以完成数据库的迁移操作。迁移操作完成后如不再需要，可释放腾讯云服务器。

1.  创建腾讯云服务器。本案例中创建的腾讯云服务器使用的是Linux操作系统。

    **说明：** 为保障腾讯云服务器和腾讯云MongoDB副本集实例的正常通信，腾讯云服务器的地域、可用区、私有网络和子网需配置与腾讯云MongoDB副本集实例一致。

2.  进入腾讯云服务器控制台，查看腾讯云服务器的内网IP地址与公网IP地址。

    ![查看云服务器的内外网IP地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156447894835509_zh-CN.png)

3.  进入腾讯云MongoDB控制台，查看腾讯云MongoDB副本集实例的内网IP地址。

    ![查看MongoDB实例的内网IP地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156447894835670_zh-CN.png)

4.  登录腾讯云服务器，使用如下命令开启腾讯云服务器的iptables服务。如果已开启，可跳过本步骤。

    ``` {#codeblock_nrm_972_0sc}
    service iptables start
    ```

5.  设置iptables规则，对27017端口进行映射。

    ``` {#codeblock_r77_ae3_uh3}
    iptables -t nat -A PREROUTING -d <CVM_IP>  -p tcp --dport 27017 -j DNAT --to-destination <MongoDB_IP>:27017
    iptables -t nat -A POSTROUTING -d <MongoDB_IP> -p tcp --dport 27017 -j SNAT --to-source <CVM_IP>
    ```

    **说明：** 

    -   <CVM\_IP\>：腾讯云服务器的内网IP地址。
    -   <MongoDB\_IP\>：腾讯云MongoDB副本集实例的内网IP地址。
    示例：

    ``` {#codeblock_7nq_l0t_e75}
    iptables -t nat -A PREROUTING -d 10.10.0.5  -p tcp --dport 27017 -j DNAT --to-destination 10.10.0.7:27017
    iptables -t nat -A POSTROUTING -d 10.10.0.7 -p tcp --dport 27017 -j SNAT --to-source 10.10.0.5
    ```

6.  开启腾讯云服务器的路由转发功能。

    ``` {#codeblock_my8_4yp_ozb}
    echo 1 > /proc/sys/net/ipv4/ip_forward
    ```

7.  返回腾讯云服务器控制台，在左侧导航栏，单击**安全组**。
8.  在入站规则页签，单击**添加规则**，放通MongoDB数据库端口27017，允许外网访问该端口。

    ![安全组配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156447894835723_zh-CN.png)

9.  进入腾讯云MongoDB控制台，单击目标MongoDB实例名。
10. 单击安全组页签，并单击**配置安全组**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/519067/156447894849246_zh-CN.png)

11. 在弹出的配置安全组对话框，选择已放通27017端口的安全组，并单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/519067/156447894849247_zh-CN.png)


## 数据迁移操作步骤 {#section_3sy_wsn_j0t .section}

1.  登录[数据传输控制台](https://dts.console.aliyun.com/)。
2.  在左侧导航栏，单击**数据迁移**。
3.  在迁移任务列表页面顶部，选择目标MongoDB实例所属地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6682/156447894950190_zh-CN.png)

4.  单击右上角的**创建迁移任务**。
5.  配置迁移任务的**源库及目标库**信息。

    ![源库及目标库配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156447894936005_zh-CN.png)

    |类别|配置|说明|
    |:-|:-|:-|
    |任务名称|-|     -   DTS为每个任务自动生成一个任务名称，任务名称没有唯一性要求。
    -   您可以修改任务名称，建议为任务配置具有业务意义的名称，便于后续的任务识别。
 |
    |源库信息|实例类型|选择**有公网IP的自建数据库**。|
    |实例地区|当实例类型选择为**有公网IP的自建数据库**时，**实例地区**无需设置。 **说明：** 您可以参考[迁移前准备工作](#section_e8n_jwq_uwg)来配置安全组规则。您也可以在**实例地区**配置项后，单击**获取DTS IP段**来获取DTS服务器的IP地址，并将获取到的IP地址加入至腾讯云MongoDB副本集实例的安全组规则中。

 |
    |数据库类型|选择**MongoDB**。|
    |主机名或IP地址|填入腾讯云服务器的公网IP地址。|
    |端口|填入腾讯云MongoDB数据库的端口号，本案例中填入**27017**。|
    |数据库名称|填入鉴权数据库名，默认为**admin**。|
    |数据库账号|填入登录腾讯云MongoDB数据库的账号，默认为**mongouser**。权限要求请参见[迁移账号权限要求](#)。|
    |数据库密码|填入登录腾讯云MongoDB数据库账号对应的密码。 **说明：** 源库信息填写完毕后，您可以单击**数据库密码**后的**测试连接**来验证填入的源库信息是否正确。源库信息填写正确则提示**测试通过**，如提示**测试失败**，单击**测试失败**后的**诊断**，根据提示调整填写的源库信息。

 |
    |目标库信息|实例类型|选择**MongoDB实例**。|
    |实例地区|选择阿里云MongoDB实例所在地域。|
    |MongoDB实例ID|选择阿里云MongoDB实例ID。|
    |数据库名称|填入鉴权数据库名，默认为**admin**。|
    |数据库账号|填入登录阿里云MongoDB数据库的账号，权限要求请参见[迁移账号权限要求](#)。|
    |数据库密码|填入登录阿里云MongoDB数据库账号对应的密码。 **说明：** 目标库信息填写完毕后，您可以单击**数据库密码**后的**测试连接**来验证填入的目标库信息是否正确。目标库信息填写正确则提示**测试通过**，如提示**测试失败**，单击**测试失败**后的**诊断**，根据提示调整填写的目标库信息。

 |

6.  配置完成后，单击页面右下角的**授权白名单并进入下一步**。

    **说明：** 此步骤会将DTS服务器的IP地址自动添加阿里云MongoDB实例的白名单中，用于保障DTS服务器能够正常连接MongoDB实例。迁移完成后如不再需要可手动删除，详情请参见[白名单设置](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

7.  选择**迁移对象**和**迁移类型**。

    ![迁移对象和迁移类型配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/519067/156447894949320_zh-CN.png)

    |配置|说明|
    |--|--|
    |迁移类型|     -   如果只需要进行全量迁移，在迁移类型选择时勾选**全量数据迁移**。

**说明：** 为保障数据一致性，全量数据迁移期间请勿在腾讯云MongoDB数据库中写入新的数据。

    -   如果需要进行不停机迁移，在迁移类型选择时勾选**全量数据迁移**和**增量数据迁移**。
 本案例为增量数据迁移，在迁移类型中同时勾选**全量数据迁移**和**增量数据迁移**。

 |
    |迁移对象|     -   在**迁移对象**框中单击待迁移的对象，然后单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83046/156447894937966_zh-CN.png)将其移动到**已选择对象**框。

**说明：** 不支持迁移admin数据库，即使被选择为迁移对象，该库中的数据也不会被迁移。

    -   迁移对象选择的粒度为：database、collection/function 两个粒度。
    -   默认情况下，迁移对象的名称不变。如果您需要迁移对象在阿里云MongoDB数据库中名称不同，那么需要使用DTS提供的对象名映射功能。使用方法请参见[库表列映射](https://help.aliyun.com/document_detail/26628.html)。
 |

8.  上述配置完成后，单击页面右下角的**预检查并启动**。

    **说明：** 

    -   在迁移任务正式启动之前，会先进行预检查。只有预检查通过后，才能成功启动迁移任务。
    -   如果预检查失败，单击具体检查项后的![提示](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/140110/156447894950068_zh-CN.png)，查看失败详情。根据失败原因修复后，重新进行预检查。
9.  预检查通过后，单击**下一步**。
10. 在**购买配置确认**页面，选择**链路规格**并勾选**数据传输（按量付费）服务条款**。
11. 单击**购买并启动**，迁移任务正式开始。
    -   全量数据迁移

        请勿手动结束迁移任务，否则可能会导致数据不完整。您只需等待迁移任务完成即可，迁移任务会自动结束。

    -   增量数据迁移

        迁移任务不会自动结束，需要手动结束迁移任务。

        **说明：** 请选择合适的时间手动结束迁移任务，例如业务低峰期或准备将业务切换至MongoDB实例时。

        1.  观察迁移任务的进度变更为**增量迁移**，并显示为**无延迟**状态时，将源库停写几分钟，此时**增量迁移**的状态可能会显示延迟的时间。
        2.  等待迁移任务的**增量迁移**再次进入**无延迟**状态，手动结束迁移任务。

            ![增量迁移无延迟](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75938/156447894933674_zh-CN.png)

12. 业务切换至阿里云MongoDB实例。

## 后续操作 {#section_4s7_z0j_kzx .section}

用于数据迁移的数据库账号拥有读写权限，为保障数据库安全性，请在数据迁移完成后，修改腾讯云MongoDB和阿里云MongoDB实例中的数据库密码。

## 如何连接阿里云MongoDB数据库 {#section_fdb_6l0_u7n .section}

-   [副本集实例连接说明](../cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)
-   [分片集群实例连接说明](../cn.zh-CN/分片集群快速入门/连接实例/分片集群实例连接说明.md#)

