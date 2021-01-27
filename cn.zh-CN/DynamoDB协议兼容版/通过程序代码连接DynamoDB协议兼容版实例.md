# 通过程序代码连接DynamoDB协议兼容版实例

本文档通过AWS CLI、Python、Java多个维度，介绍如何连接到DynamoDB协议兼容版实例。

-   您已创建DynamoDB协议兼容版实例。更多信息，请参见[创建DynamoDB协议兼容版实例](/cn.zh-CN/DynamoDB协议兼容版/创建DynamoDB协议兼容版实例.md)。
-   您已获取到DynamoDB协议兼容版实例的连接地址。更多信息，请参见[获取DynamoDB协议兼容版实例的连接地址](/cn.zh-CN/DynamoDB协议兼容版/获取DynamoDB协议兼容版实例的连接地址.md)。

## AWS CLI连接示例

本章节以Ubuntu 16.04.6 LTS系统为例，演示如何通过AWS CLI（AWS Command Line Interface）连接DynamoDB协议兼容版实例。关于AWS CLI的详细信息，请参见[AWS Command Line Interface是什么](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-chap-welcome.html)。

前提条件：您使用的ECS实例必须和目标DynamoDB协议兼容版实例处于同一个专有网络（VPC）中。

1.  安装AWS CLI客户端。

    1.  执行如下命令获取最新版的AWS CLI并将其重命名为`awscliv2.zip`。

        ```
        curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
        ```

    2.  执行如下命令解压`awscliv2.zip`文件。

        ```
        unzip awscliv2.zip
        ```

        **说明：** 如果您尚未安装`unzip`，请先通过`apt install unzip`命令安装，然后再执行上面的解压命令。

    3.  执行如下命令安装AWS CLI。

        ```
        sudo ./aws/install
        ```

    当命令行窗口中出现`You can now run: /usr/local/bin/aws --version`提示，则表示您已成功安装AWS CLI。此时您可以执行`/usr/local/bin/aws --version`命令查看当前AWS CLI的版本号。

2.  执行`/usr/local/bin/aws configure`配置AWS CLI，分别输入下列几项参数（每输入一项参数按回车）：

    |参数|说明|示例|
    |--|--|--|
    |`AWS Access Key ID`|输入您AWS账号的Access Key ID，如没有可以输入任意字符。|`XXXXXXXXXX`|
    |`AWS Secret Access Key`|输入您AWS账号的Secret Access Key，如没有可以输入任意字符。|`XXXXXXXXXX`|
    |`Default region name`|输入您AWS的DynamoDB数据库所在的地域，如没有可以根据示例输入。|`us-west-2`|
    |`Default output format`|默认的输出格式，此处可以留空。|`json`|

    **说明：** 更多AWS CLI配置说明的相关信息，请参见[AWS CLI基本配置](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-configure-quickstart.html)。

3.  输入如下格式的命令连接到目标DynamoDB协议兼容版实例并创建一张表。

    ```
    aws dynamodb --endpoint-url <DynamoDB协议兼容版实例的连接串地址> \ 
        create-table --table-name <需要创建的表名> \
        --attribute-definitions AttributeName=<属性名>,AttributeType=<属性的数据类型> \
        --key-schema AttributeName=<指定主键的属性名>,KeyType=<主键的角色> \
        --provisioned-throughput ReadCapacityUnits=<预设读吞吐量>,WriteCapacityUnits=<预设写吞吐量>
    ```

    |参数|说明|
    |--|--|
    |`--endpoint-url`|需要连接的目标DynamoDB协议兼容版实例地址。需要以`HTTP://`开头。|
    |`create-table`|创建表的命令。**说明：** 更多信息，请参见[create-table](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/create-table.html)。 |
    |`--table-name`|指定需要创建表的名称。|
    |`--attribute-definitions`|描述表或索引整体架构的属性数组。该选项还需指定如下两个子选项：    -   `AttributeName`：属性的名称。
    -   `AttributeType`：属性的数据类型。

**说明：** 更多信息，请参见[create-table](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/create-table.html)。 |
    |`--key-schema`|指定表或索引的主键属性。该选项还需指定如下两个子选项：    -   `AttributeName`：指定通过`--attribute-definitions`创建的某个属性名为主键。
    -   `KeyType`：指定主键的角色。

**说明：** 更多信息，请参见[create-table](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/create-table.html)。 |
    |`--provisioned-throughput`|指定表或索引的预设吞吐量。该选项还需指定如下两个子选项：    -   `ReadCapacityUnits`：指定预设读吞吐量。
    -   `WriteCapacityUnits`：指定预设写吞吐量。
**说明：** 更多信息，请参见[create-table](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/create-table.html)。 |

    示例：

    ```
    /usr/local/bin/aws dynamodb --endpoint-url http://dds-xxxx.mongodb.rds.aliyuncs.com:3717 #连接到指定的DynamoDB协议兼容版实例地址。 \
        create-table --table-name student #创建一个名为student的表。 \
        --attribute-definitions AttributeName=name,AttributeType=S AttributeName=age,AttributeType=N #表的架构中，有类型为String的name属性和类型为Number的age属性。 \
        --key-schema AttributeName=name,KeyType=HASH AttributeName=age,KeyType=RANGE #指定name属性为分区键，并指定age属性为排序键。 \
        --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5 #指定预设的读写吞吐量各为5。
    ```

    当命令行中打印出如下内容，则表示您已成功连接到目标DynamoDB协议兼容版实例并创建了一张表。

    ```
    {
        "TableDescription": {
            "TableName": "student",
            "KeySchema": [
                {
                    "AttributeName": "name",
                    "KeyType": "HASH"
                },
                {
                    "AttributeName": "age",
                    "KeyType": "RANGE"
                }
            ],
            "TableStatus": "CREATING",
            "TableSizeBytes": 0,
            "ItemCount": 0
        }
    }
                            
    ```


## Python连接示例

前提条件：

-   已安装Python 2.6或更高版本。更多信息，请参见[Python官网](https://www.python.org/downloads/)。
-   已安装Boto3。更多信息，请参见[安装Boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)。

以下代码演示通过Python连接到DynamoDB协议兼容版实例并创建一个名为`Book`的表格：

```
import boto3

def create_book_table(dynamodb=None):
    if not dynamodb:
        dynamodb = boto3.resource('dynamodb', endpoint_url="http://dds-xxxx.mongodb.rds.aliyuncs.com:3717")
    table = dynamodb.create_table(
        TableName='Book',
        KeySchema=[
            {
                'AttributeName':'title',
                'KeyType':'HASH'
            },
            {
                'AttributeName':'year',
                'KeyType':'RANGE'
            }
        ],
        AttributeDefinitions=[
            {
                'AttributeName':'title',
                'AttributeType':'S'
            },
            {
                'AttributeName':'year',
                'AttributeType':'N'
            },
        ],
        ProvisionedThroughput={
            'ReadCapacityUnits':5,
            'WriteCapacityUnits':5
        }
    )
    return table
 
if __name__ == '__main__':
    book_table =create_book_table()
    print("Tablestatus:", book_table.table_status)
```

## Java连接示例

前提条件：已安装AWS SDK for Java。更多信息，请参见[安装AWS SDK for Java](https://docs.aws.amazon.com/zh_cn/sdk-for-java/v2/developer-guide/setup-install.html)。

以下代码演示通过Java连接到DynamoDB协议兼容版实例并创建一个名为`Book`的表格：

```
package com.amazonaws.codesamples.gsg;

import java.util.Arrays;
import com.amazonaws.client.builder.AwsClientBuilder;
import com.amazonaws.services.dynamodbv2.AmazonDynamoDB;
import com.amazonaws.services.dynamodbv2.AmazonDynamoDBClientBuilder;
import com.amazonaws.services.dynamodbv2.document.DynamoDB;
import com.amazonaws.services.dynamodbv2.document.Table;
import com.amazonaws.services.dynamodbv2.model.AttributeDefinition;
import com.amazonaws.services.dynamodbv2.model.KeySchemaElement;
import com.amazonaws.services.dynamodbv2.model.KeyType;
import com.amazonaws.services.dynamodbv2.model.ProvisionedThroughput;
import com.amazonaws.services.dynamodbv2.model.ScalarAttributeType;

public class MoviesCreateTable {
    public static void main(String[] args) throws Exception {
        
        AmazonDynamoDB client =AmazonDynamoDBClientBuilder.standard()
            .withEndpointConfiguration(new AwsClientBuilder.EndpointConfiguration("http://dds-xxxx.mongodb.rds.aliyuncs.com:3717",
"us-east-1"))
            .build();

        DynamoDB dynamoDB = new DynamoDB(client);

        String tableName ="Book";

        try {
            System.out.println("Creating table...");
            Table table =dynamoDB.createTable(tableName,
                Arrays.asList(new
KeySchemaElement("title", KeyType.HASH), // 分区键
                    new KeySchemaElement("year", KeyType.RANGE)), // 排序键
                Arrays.asList(new AttributeDefinition("title", ScalarAttributeType.S),
                    new AttributeDefinition("year", ScalarAttributeType.N)),
                new ProvisionedThroughput(5L, 5L));
            table.waitForActive();
           System.out.println("OK. Table status: " + table.getDescription().getTableStatus());
        }
        catch (Exception e) {
           System.err.println("Unable to create table: ");
           System.err.println(e.getMessage());
        }
    }
}
```

## 其他程序代码的连接示例

请参见[开始使用DynamoDB和AWS开发工具包](https://docs.aws.amazon.com/zh_cn/amazondynamodb/latest/developerguide/GettingStarted.html)。

