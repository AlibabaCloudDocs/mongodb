# Java SDK使用说明

本文介绍如何使用云数据库MongoDB版的Java开发者工具包（SDK），并提供示例供您参考。

-   已经创建了AccessKey，详情请参见[创建AccessKey](~~53045~~)。

    **警告：** 为避免主账号泄露AccessKey带来的安全风险，建议您创建RAM用户，然后授予RAM用户云数据库MongoDB版相关的访问权限，再使用RAM用户的AccessKey调用SDK。详情请参见[账号访问控制](~~25481~~)。

-   已下载云数据库MongoDB版的SDK安装包，详情请前往[阿里云SDK频道](https://developer.aliyun.com/sdk)下载。

    ![下载安装包](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0273132061/p73175.png)


## 安装方法

详情请参见[安装Alibaba Cloud SDK for Java](~~52740~~)。

## 请求步骤

1.  设置地域和AK信息。

    ```
    IClientProfile profile = DefaultProfile.getProfile("<RegonId>","<accessKeyId>","<accessSecret>");
    ```

    **说明：**

    -   <RegonId\>：地域ID。
    -   <accessKeyId\>： RAM账号的AccessKey ID。
    -   <accessSecret\>：RAM账号AccessKey Secret。
2.  设置Endpoint信息。

    Endpoint是阿里云服务的API服务端地址。针对不同的地域，单个服务可能有不同的Endpoint。阿里云SDK内置了Endpoint寻址模块，当您调用SDK对一个服务发起请求时，SDK会自动根据您在创建SDK client时指定的地域ID（Region ID）和产品ID来找到Endpoint，所以该步骤为可选。各地域的Endpoint信息请参见[服务地址](/cn.zh-CN/API参考/请求结构.md)。

    ```
    DefaultProfile.addEndpoint("<endpointName>","<RegonId>", "dds", "<domain>");
    ```

    **说明：**

    -   <endpointName\>：Endpoint名称。
    -   <RegonId\>：地域ID，详情请参见[地域和可用区](~~40654~~)。
    -   <domain\>：域名信息，详情请参见[服务地址](/cn.zh-CN/API参考/请求结构.md)。
3.  初始化客户端。

    ```
    DefaultAcsClient client = new DefaultAcsClient(profile);
    ```

4.  创建API请求并设置参数。

    下述代码以DescribeAccounts（查询账号信息）为例。

    ```
    DescribeAccountsRequest request = new DescribeAccountsRequest();
          request.setDBInstanceId("dds-********");
          request.setAccountName("root");
    ```

5.  调用返回结果。

    ```
    DescribeAccountsResponse response = client.getAcsResponse(request);
    ```


## 请求示例

```
import com.alibaba.fastjson.JSON;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.dds.model.v20151201.DescribeAccountsRequest;
import com.aliyuncs.dds.model.v20151201.DescribeAccountsResponse;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.profile.IClientProfile;

 public class ApiDescribeAccountsTest {
    IClientProfile profile = DefaultProfile.getProfile("cn-qingdao", "********", "**********");
        //初始化客户端
        DefaultAcsClient client = new DefaultAcsClient(profile);
        DescribeAccountsRequest request = new DescribeAccountsRequest();
        request.setDBInstanceId("dds-********");
        request.setAccountName("root");
        try {
            DescribeAccountsResponse response = client.getAcsResponse(request);
            String s = JSON.toJSONString(response);
            System.out.println(s);
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }
```

## 返回示例

```
{"accounts":[{"accountName":"root","accountStatus":"Available","dBInstanceId":"dds-********"}],"requestId":"4D********-9640ED88F3C4"}
```

## 更多信息

-   在线调试和生成SDK示例。

    [OpenAPI Explorer](https://api.aliyun.com/)提供在线调用云产品API、动态生成SDK示例代码和快速检索接口等功能，能显著降低使用API的难度，推荐您使用。

-   更多相关说明，请参见[Java SDK使用说明](https://help.aliyun.com/product/108101.html)。

