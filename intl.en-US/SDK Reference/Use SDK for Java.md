# Use SDK for Java

This topic describes how to use ApsaraDB for MongoDB SDK for Java. Examples are also provided for your reference.

-   An AccessKey pair is created. For more information, see [Create an AccessKey pair](~~53045~~).

    **Warning:** To protect the AccessKey pair of your Alibaba Cloud account, we recommend that you create a RAM user, grant the RAM user the permissions to access ApsaraDB for MongoDB, and then use the AccessKey pair of the RAM user to call the Java SDK. For more information, see [Resource Access Management](~~25481~~).

-   The SDK installation package of ApsaraDB for MongoDB is downloaded. For more information, see [Download SDKs](/intl.en-US/SDK Reference/Download SDKs.md).

## Install the SDK

For more information, see [Install Alibaba Cloud SDK for Java](~~52740~~).

## Procedure

1.  Set the region and AccessKey pair.

    ```
    IClientProfile profile = DefaultProfile.getProfile("<RegonId>","<accessKeyId>","<accessSecret>");
    ```

    **Note:**

    -   <RegonId\>: the region ID.
    -   <accessKeyId\>: the AccessKey ID of the RAM user.
    -   <accessSecret\>: the AccessKey secret of the RAM user.
2.  Set the endpoint.

    An endpoint is the API server address of an Alibaba Cloud service. Each service may have different endpoints in different regions. An endpoint addressing module is built in the Alibaba Cloud SDK. When you call the SDK to initiate a request to a service, the SDK automatically identifies the endpoint based on the region ID that you specified when you create the SDK client and the service ID. Therefore, this step is optional. For more information about the endpoints of different regions, see [Endpoints](/intl.en-US/API Reference/Request structure.md).

    ```
    DefaultProfile.addEndpoint("<endpointName>","<RegonId>", "dds", "<domain>");
    ```

    **Note:**

    -   <endpointName\>: the name of the endpoint.
    -   <RegonId\>: the region ID. For more information, see [Regions and zones](~~40654~~).
    -   <domain\>: the endpoint information. For more information, see [Endpoints](/intl.en-US/API Reference/Request structure.md).
3.  Initiate the client.

    ```
    DefaultAcsClient client = new DefaultAcsClient(profile);
    ```

4.  Create an API request and configure parameters.

    The following code is based on the DescribeAccounts request.

    ```
    DescribeAccountsRequest request = new DescribeAccountsRequest();
          request.setDBInstanceId("dds-********");
          request.setAccountName("root");
    ```

5.  View the response.

    ```
    DescribeAccountsResponse response = client.getAcsResponse(request);
    ```


## Sample requests

```
import com.alibaba.fastjson.JSON;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.dds.model.v20151201.DescribeAccountsRequest;
import com.aliyuncs.dds.model.v20151201.DescribeAccountsResponse;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.profile.IClientProfile;

 public class ApiDescribeAccountsTest {
    IClientProfile profile = DefaultProfile.getProfile("cn-qingdao", "********", "**********");
        // Initialize the client.
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

## Sample responses

```
{"accounts":[{"accountName":"root","accountStatus":"Available","dBInstanceId":"dds-********"}],"requestId":"4D********-9640ED88F3C4"}
```

## References

For more information, see [Use Alibaba Cloud SDK for Java](https://www.alibabacloud.com/help/zh/product/108101.html).

