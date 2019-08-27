# 使用DTS将腾讯云MongoDB全量迁移至阿里云 {#concept_dx2_w5x_ggb .concept}

本文介绍如何使用数据传输服务DTS（Data Transmission Service），将3.2版本的腾讯云MongoDB副本集实例全量迁移至阿里云。

## 背景信息 {#section_ohv_lwz_ngb .section}

当您因业务调整或需要使用阿里云MongoDB特性功能时，您可以使用DTS工具，通过**全量数据迁移**方法，将3.2版本的腾讯云MongoDB副本集实例迁移至阿里云MongoDB实例。

## 前提条件 {#section_zz2_qsd_fnp .section}

-   腾讯云MongoDB副本集实例的数据库版本为3.2版本。

    **说明：** 关于3.6版本的腾讯云MongoDB副本集实例的迁移方法，请参见[使用DTS将腾讯云MongoDB增量迁移至阿里云](cn.zh-CN/用户指南/数据迁移__同步/第三方云迁移到阿里云/使用DTS将腾讯云MongoDB增量迁移至阿里云.md#)。

-   已创建阿里云MongoDB实例。如果尚未创建，请参见[创建副本集实例](../cn.zh-CN/副本集快速入门/创建副本集实例.md#)或[创建分片集群实例](../cn.zh-CN/分片集群快速入门/创建分片集群实例.md#)。

    **说明：** 阿里云MongoDB实例的存储空间应大于腾讯云MongoDB副本集实例已使用的存储空间。如果创建的阿里云MongoDB实例存储空间过低，您需要升级存储空间，详情请参见[变更配置](cn.zh-CN/用户指南/实例管理/变更配置.md#)。

-   如需迁移至阿里云MongoDB分片集群实例，建议对数据进行分片以更好地发挥性能，详情请参见[设置数据分片](../cn.zh-CN/最佳实践/设置数据分片以充分利用Shard性能.md#)。

## 注意事项 {#section_2h4_f82_ql1 .section}

-   迁移开始前需要停止腾讯云MongoDB数据库的相关业务，为保障数据一致性，全量数据迁移期间请勿在腾讯云MongoDB数据库中写入新的数据。
-   为避免影响您的业务使用，请在业务低峰期进行数据迁移操作。
-   对于迁移失败的任务，DTS会触发自动恢复。当您需要将业务切换至目标实例时，请务必先结束或释放该任务，避免该任务被自动恢复后，导致源端数据覆盖目标实例的数据。
-   不支持迁移admin数据库，即使您将admin数据库选择为迁移对象，该库中的数据也不会被迁移。
-   阿里云MongoDB实例支持的版本与存储引擎请参见[版本及存储引擎](../cn.zh-CN/产品简介/版本及存储引擎.md#)，如需跨版本或跨引擎迁移，请提前确认兼容性。

## 费用说明 {#section_brm_q21_1gb .section}

|迁移类型|链路配置费用|公网流量费用|
|:---|:-----|:-----|
|全量数据迁移|不收取|不收取|

## 迁移类型说明 {#section_vbi_8jf_fp6 .section}

全量数据迁移：将源MongoDB数据库迁移对象的存量数据全部迁移到目标MongoDB数据库中。

**说明：** 支持database、collection、index的迁移。

## 迁移权限要求 {#section_mfq_xmr_zfb .section}

|迁移对象|权限要求|
|:---|:---|
|腾讯云MongoDB副本集实例|待迁移库的read权限|
|阿里云MongoDB实例|目标库的readWrite权限|

## 迁移前准备工作 {#section_pcx_yhs_zfb .section}

由于腾讯云MongoDB实例只有内网连接地址，没有公网连接地址。此时需要创建一个具有公网地址的腾讯云服务器用作端口数据转发，以完成数据库的迁移操作。迁移操作完成后如不再需要，可释放腾讯云服务器。

1.  创建腾讯云服务器。本案例中创建的腾讯云服务器使用的是Linux操作系统。

    **说明：** 为保障腾讯云服务器和腾讯云MongoDB副本集实例的正常通信，腾讯云服务器的地域、可用区、私有网络和子网需配置与腾讯云MongoDB副本集实例一致。

2.  进入腾讯云服务器控制台，查看腾讯云服务器的内网IP地址与公网IP地址。

    ![查看云服务器的内外网IP地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156447897435509_zh-CN.png)

3.  进入腾讯云MongoDB控制台，查看腾讯云MongoDB副本集实例的内网IP地址。

    ![查看MongoDB实例的内网IP地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156447897435670_zh-CN.png)

4.  登录腾讯云服务器，使用如下命令开启腾讯云服务器的iptables服务。如果已开启，可跳过本步骤。

    ``` {#codeblock_24n_4iv_srj}
    service iptables start
    ```

5.  设置iptables规则，对27017端口进行映射。

    ``` {#codeblock_44l_dr2_b6d}
    iptables -t nat -A PREROUTING -d <CVM_IP>  -p tcp --dport 27017 -j DNAT --to-destination <MongoDB_IP>:27017
    iptables -t nat -A POSTROUTING -d <MongoDB_IP> -p tcp --dport 27017 -j SNAT --to-source <CVM_IP>
    ```

    **说明：** 

    -   <CVM\_IP\>：腾讯云服务器的内网IP地址。
    -   <MongoDB\_IP\>：腾讯云MongoDB副本集实例的内网IP地址。
    示例：

    ``` {#codeblock_uaj_j2v_c8x}
    iptables -t nat -A PREROUTING -d 10.10.0.5  -p tcp --dport 27017 -j DNAT --to-destination 10.10.0.7:27017
    iptables -t nat -A POSTROUTING -d 10.10.0.7 -p tcp --dport 27017 -j SNAT --to-source 10.10.0.5
    ```

6.  开启腾讯云服务器的路由转发功能。

    ``` {#codeblock_6kw_l4z_f2f}
    echo 1 > /proc/sys/net/ipv4/ip_forward
    ```

7.  返回腾讯云服务器控制台，在左侧导航栏，单击**安全组**。
8.  在入站规则页签，单击**添加规则**，放通MongoDB数据库端口27017，允许外网访问该端口。

    ![安全组配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156447897435723_zh-CN.png)

9.  进入腾讯云MongoDB控制台，单击目标MongoDB实例名。
10. 单击安全组页签，并单击**配置安全组**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/519067/156447897449246_zh-CN.png)

11. 在弹出的配置安全组对话框，选择已放通27017端口的安全组，并单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/519067/156447897449247_zh-CN.png)


## 数据迁移操作步骤 {#section_2ef_9ho_8w8 .section}

1.  登录[数据传输控制台](https://dts.console.aliyun.com/)。
2.  在左侧导航栏，单击**数据迁移**。
3.  在迁移任务列表页面顶部，选择目标MongoDB实例所属地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6682/156447897450190_zh-CN.png)

4.  单击右上角的**创建迁移任务**。
5.  配置迁移任务的源库及目标库信息。

    ![源库及目标库配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156447897536005_zh-CN.png)

    |类别|配置|说明|
    |:-|:-|:-|
    |任务名称|-|     -   DTS为每个任务自动生成一个任务名称，任务名称没有唯一性要求。
    -   您可以修改任务名称，建议为任务配置具有业务意义的名称，便于后续的任务识别。
 |
    |源库信息|实例类型|选择**有公网IP的自建数据库**。|
    |实例地区|当实例类型选择为**有公网IP的自建数据库**时，**实例地区**无需设置。 **说明：** 您可以参考[迁移前准备工作](#section_pcx_yhs_zfb)来配置安全组规则。您也可以在**实例地区**配置项后，单击**获取DTS IP段**来获取DTS服务器的IP地址，并将获取到的IP地址加入至腾讯云MongoDB副本集实例的安全组规则中。

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

7.  选择迁移对象和迁移类型。

    ![迁移对象和迁移类型配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83046/156447897535725_zh-CN.png)

    |配置|说明|
    |--|--|
    |迁移类型| 本案例为全量数据迁移，在迁移类型中勾选**全量数据迁移**。

 **说明：** 为保障数据一致性，全量数据迁移期间请勿在腾讯云MongoDB数据库中写入新的数据。

 |
    |迁移对象|     -   在**迁移对象**框中单击待迁移的对象，然后单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83046/156447897537966_zh-CN.png)将其移动到**已选择对象**框。

**说明：** 不支持迁移admin数据库，即使被选择为迁移对象，该库中的数据也不会被迁移。

    -   迁移对象选择的粒度为：database、collection/function 两个粒度。
    -   默认情况下，迁移对象的名称不变。如果您需要迁移对象在阿里云MongoDB数据库中名称不同，那么需要使用DTS提供的对象名映射功能。使用方法请参见[库表列映射](https://help.aliyun.com/document_detail/26628.html)。
 |

8.  上述配置完成后，单击页面右下角的**预检查并启动**。

    **说明：** 

    -   在迁移任务正式启动之前，会先进行预检查。只有预检查通过后，才能成功启动迁移任务。
    -   如果预检查失败，单击具体检查项后的![提示](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/140110/156447897550068_zh-CN.png)，查看失败详情。根据失败原因修复后，重新进行预检查。
9.  预检查通过后，单击**下一步**。
10. 在**购买配置确认**页面，选择**链路规格**并勾选**数据传输（按量付费）服务条款**。
11. 单击**购买并启动**，迁移任务正式开始。

    **说明：** 请勿手动停止迁移任务，否则可能会导致数据不完整。您只需等待迁移任务完成即可，迁移任务会自动停止。

12. 将业务切换至阿里云MongoDB实例。

## 后续操作 {#section_mf1_tp0_0df .section}

用于数据迁移的数据库账号拥有读写权限，为保障数据库安全性，请在数据迁移完成后，修改腾讯云MongoDB和阿里云MongoDB实例中的数据库密码。

## 如何连接阿里云MongoDB数据库 {#section_iz6_x9c_r6y .section}

-   [副本集实例连接说明](../cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)
-   [分片集群实例连接说明](../cn.zh-CN/分片集群快速入门/连接实例/分片集群实例连接说明.md#)

