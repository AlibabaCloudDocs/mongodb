# Request structure

ApsaraDB for MongoDB allows you to send URL-based requests by using the HTTP or HTTPS GET method. You must add parameters to a request based on the operation description. Then, ApsaraDB for MongoDB returns the result.

## Endpoints

The following table lists the endpoints of ApsaraDB for MongoDB.

|Region|Endpoint|
|------|--------|
|China \(Qingdao\), China \(Beijing\), China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), China \(Hong Kong\) Singapore, US \(Virginia\), and US \(Silicon Valley\)

|mongodb-inner.aliyuncs.com|
|China \(Zhangjiakou\)|mongodb.cn-zhangjiakou.aliyuncs.com|
|China \(Hohhot\)|mongodb.cn-huhehaote.aliyuncs.com|
|Australia \(Sydney\)|mongodb.ap-southeast-2.aliyuncs.com|
|Malaysia \(Kuala Lumpur\)|mongodb.ap-southeast-3.aliyuncs.com|
|Germany \(Frankfurt\)|mongodb.eu-central-1.aliyuncs.com|

## Protocols

You can call ApsaraDB for MongoDB API operations by sending HTTP or HTTPS requests. We recommend that you use HTTPS for enhanced security.

## Methods

The HTTP GET method can be used to send requests. Request parameters must be included in the request URL.

## Parameters

Each request must specify the operation to be performed \(such as CreateDBInstance\) in the Action parameter. Request parameters include both common parameters and operation-specific parameters.

## Encoding

All requests and responses are encoded in UTF-8.

