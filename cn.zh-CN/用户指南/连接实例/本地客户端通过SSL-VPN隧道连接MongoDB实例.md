# 本地客户端通过SSL-VPN隧道连接MongoDB实例 {#concept_185604 .concept}

您可以在管理终端与MongoDB实例的专有网络之间建立SSL-VPN隧道，实现安全便捷地连接MongoDB实例。

## 适用场景 {#section_fnd_jrq_ggb .section}

-   管理MongoDB数据库的客户端所处的网络环境没有固定的公网地址，导致您要在MongoDB控制台上频繁调整白名单IP地址，且如果没有及时清理过期的白名单地址，将存在一定的安全风险。
-   对网络安全要求较高，通过公网连接MongDB实例时，需要更加安全的方式连接MongoDB实例。
-   数据库运维人员在公网环境中通过ECS来登录MongoDB数据库，在权限管理上存在一定的风险，需要实现ECS的管理权限和MongoDB数据库权限的分离。

## 费用说明 {#section_vhc_dxq_ggb .section}

操作步骤中创建VPN网关时将产生费用，详情请参见[计费说明](https://help.aliyun.com/document_detail/64984.html)。

## 前提条件 {#section_jg1_tvq_ggb .section}

-   MongoDB实例的网络类型为专有网络，如果是经典网络请切换至专有网络，详情请参考[从经典网络切换为专有网络](cn.zh-CN/用户指南/管理网络连接/切换实例网络类型.md#section_tp1_1sl_2fb)。
-   本地客户端的IP地址段和MongoDB实例所在的VPC网络的IP地址段不能相同，否则无法通信。
-   本地客户端必须能访问外网。

## 案例环境介绍 {#section_yf2_jdr_ggb .section}

![SSL连接环境介绍](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/159808/156879106244679_zh-CN.png)

## 步骤一 创建VPN网关 {#section_xxd_vwq_ggb .section}

1.  登录[专有网络管理控制台](https://vpc.console.aliyun.com)。
2.  在页面左上角选择地域。
3.  在左侧导航栏，单击**VPN** \> **VPN网关**
4.  在VPN网关页面，单击**创建VPN网关**。
5.  根据业务需求，配置VPN网关的规格信息。

    |配置项|配置说明|
    |:--|:---|
    |地域|VPN网关的所属地域，选择与MongoDB实例相同的地域。|
    |专有网络|选择MongoDB实例所属的专有网络。|
    |带宽规格|选择VPN网关的带宽规格，带宽规格是VPN网关所具备的公网带宽。|
    |IPsec-VPN| 选择是否开启IPsec-VPN功能，您可以根据业务需求选择。本案例使用终端直接接入，选择为**关闭IPsec-VPN**。

 IPsec-VPN功能提供站点到站点的连接。您可以通过创建IPsec隧道将本地数据中心网络和专有网络或两个专有网络安全地连接起来。

 |
    |SSL-VPN| 选择是否开启SSL-VPN功能，您可以根据业务需求选择，本案例使用终端直接接入，选择为**开启SSL-VPN**。

 提供点到站点的VPN连接，不需要配置客户网关，终端直接接入。

 |
    |计费周期|选择包年包月实例的时长，包月可选择1~9个月，包年可选择1~3年。|
    |自动续费|选择是否自动续费。     -   按月购买：自动续费周期为1个月。
    -   按年购买：则自动续费周期为1年。
 |

6.  单击**立即购买**，根据提示完成支付流程。

## 步骤二 创建SSL服务端 {#section_qxs_y2r_ggb .section}

1.  登录[专有网络管理控制台](https://vpc.console.aliyun.com)。
2.  在页面左上角选择地域。
3.  在左侧导航栏，单击**VPN** \> **SSL服务端**。
4.  在SSL服务端页面，单击**创建SSL服务端**。
5.  在创建SSL服务端对话框，配置SSL服务端信息。

    |配置项|配置说明|
    |:--|:---|
    |名称| SSL服务端的名称。

 名称在2-128个字符之间，以英文字母或中文开始，可包含数字、连字符（-）和下划线（\_）。

 |
    |VPN网关| 关联的VPN网关，选择[步骤一 创建VPN网关](#section_xxd_vwq_ggb)中创建的VPN网关。

 |
    |本端网段| 本端网段是客户端通过SSL-VPN连接要访问的地址段。本端网段可以是VPC的网段、交换机的网段、通过专线和VPC互连的IDC的网段、云服务如RDS/OSS等网段。

 本案例填写MongoDB实例所属专有网络中交换机的网段地址：172.16.1.0/24。

 **说明：** 本端网段的子网掩码的范围为16到29位。

 |
    |客户端网段| 客户端网段是给客户端虚拟网卡分配访问地址的的地址段，不是指客户端已有的内网网段。当客户端通过SSL-VPN连接访问本端时，VPN网关会从指定的客户端网段中分配一个IP地址给客户端使用。

 此案例中填写192.168.100.0/24。

 **说明：** 确保客户端网段和**本端网段**不冲突。

 |

6.  单击**确定**。

## 步骤三 创建SSL客户端 {#section_oxb_dfr_ggb .section}

1.  登录[专有网络管理控制台](https://vpc.console.aliyun.com)。
2.  在页面左上角选择地域。
3.  在左侧导航栏，单击**VPN** \> **SSL客户端**。
4.  在SSL客户端页面，单击**SSL客户端证书**。

    |配置项|说明|
    |:--|:-|
    |名称| SSL客户端证书的名称。

 名称在2-128个字符之间，以英文字母或中文开始，可包含数字、连字符（-）和下划线（\_）。

 |
    |SSL服务端|选择[步骤二 创建SSL服务端](#section_qxs_y2r_ggb)中创建的SSL服务端。|

5.  单击**确定**。

## 客户端通过SSL-VPN隧道登录MongoDB数据库 {#section_ds2_jhr_ggb .section}

本文以Windows系统为例连接SSL-VPN，其他操作系统请参考：[在Linux系统中连接SSL-VPN](https://help.aliyun.com/document_detail/65075.html#h2-url-5)、[在Mac系统中连接SSL-VPN](https://help.aliyun.com/document_detail/65068.html#h2-url-5)。

1.  登录[专有网络管理控制台](https://vpc.console.aliyun.com)。
2.  在页面左上角选择地域。
3.  在左侧导航栏，单击**VPN** \> **SSL客户端**。
4.  在刚刚创建的SSL客户端实例的右侧，单击**下载**，下载生成的客户端证书。
5.  在需要进行连接SSL-VPN的客户端设备中，下载并安装OpenVPN客户端。
6.  将下载的客户端证书解压后复制到OpenVPN安装目录中的config文件夹中。
7.  单击**Connect**发起连接。

    ![发起SSL连接](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/159808/156879106244665_zh-CN.png)

8.  将MongoDB实例所属的专有网络IP地址段添加至MongoDB实例的白名单中，本案例将172.16.1.0/24加入至MongoDB实例的白名单中。
9.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
10. 获取MongoDB实例的专有网络地址，详情请参考[实例连接说明](../../../../cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)。

    ![MongoDB实例专有网络](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/159808/156879106244701_zh-CN.png)

11. 使用[Mongo Shell](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)或者其他管理工具登录MongoDB数据库。

    **说明：** 请使用MongoDB实例的专有网络地址登录。


