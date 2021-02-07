# Error codes

This topic describes the error codes of ApsaraDB for MongoDB.

|Description|Code|Message|HTTP Status Code|
|:----------|:---|:------|:---------------|
|The error message returned because unauthorized users call the operation.|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn’t support RAM.|403|
|The error message returned because this operation is not available for RAM users.|Forbedden.NotSupportRAM|This action does not support accessed by RAM mode.|403|
|The error message returned because an exception or error occurs on the server.|ServiceUnavailable|The request has failed due to a temporary failure of the server.|503|
|The error message returned because the instance status that you specified does not exist.|InvalidStatus.NotFound|The Status provided does not exist in our records.|404|
|The error message returned because the specified value of the parameter is invalid.|InvalidParameter|The specified parameter "InstanceName" is not valid.|400|
|The error message returned because a normal user other than an administrator calls the management operation.|Forbbiden.NotAdminUser|User not authorized to operate on the specified API as you are not the administrator.|403|
|The error message returned because the parameter is missing.|MissingParameter|Specified parameter is missing.|400|
|The error message returned because neither the InstanceName nor NewPassword parameter is specified.|MissingParameter|InstanceName/NewPassword at least one is mandatory for this action.|400|
|The error message returned because the OwnerId parameter is not specified.|MissingParameter|The input parameter OwnerId,OwnerAccount that is mandatory for processing this request is not supplied.|403|
|The error message returned because the specified Token parameter is invalid.|InvalidToken.Malformed|The Specified parameter \\"Token\\" is not valid.|400|
|The error message returned because the specified InstanceName parameter is invalid.|InvalidInstanceName.Malformed|The Specified parameter \\"InstanceName\\" is not valid.|400|
|The error message returned because the specified Password parameter is invalid.|InvalidPassword.Malformed|The Specified parameter \\"Password\\" is not valid.|400|
|The error message returned because the specified Instances parameter is invalid.|InvalidInstances.Malformed|The Specified parameter \\"Instances\\" is not valid.|400|
|The error message returned because the specified StartTime parameter is invalid.|InvalidStartTime.Malformed|The Specified parameter \\"StartTime\\" is not valid.|400|
|The error message returned because the specified EndTime parameter is invalid.|InvalidEndTime.Malformed|The Specified parameter \\"EndTime\\" is not valid.|400|
|The error message returned because the specified InstanceIds parameter is invalid.|InvalidInstanceIds.Malformed|The Specified parameter \\"InstanceIds\\" is not valid.|400|
|The error message returned because the balance is insufficient.|InsufficientBalance|Your account does not have enough balance.|400|
|The error message returned because your account fails to pass the real-name authentication.|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|403|
|The error message returned because your instance quota has been reached.|QuotaExceed|Living afterpay instances quota exceeded.|400|
|The error message returned because the capacity configuration is invalid.|InvalidCapacity.NotFound|The Capacity provided does not exist in our records.|400|
|The error message returned because the two specified requests use the same client token.|IdempotentParameterMismatch|Request uses a client token in a previous request but is not identical to that request.|400|
|The error message returned because the inventory of instances in the specified zone is insufficient.|QuotaNotEnough|Quota not enough in this zone.|400|
|The error message returned because you are not authorized to call the order-class API.|Forbbiden.SubUser|The specified action is not available for you.|403|
|The error message returned because the Apsara Stack risk control system denies this access request.|Forbidden.RiskControl|This operation is forbidden by Aliyun Risk Control system.|403|
|The error message returned because the specified region does not exist.|InvalidRegion.NotFound|The RegionId or ZoneId provided does not exist in our records.|404|
|The error message returned because the specified ZoneId parameter is invalid.|InvalidZoneId.NotFound|The ZoneId provided is invalid.|400|
|The error message returned because the specified instance ID does not exist.|InvalidInstanceId.NotFound|The InstanceId provided does not exist in our records.|404|
|The error message returned because the password is incorrect.|IncorrectPassword|The Password provided is not correct.|400|
|The error message returned because the specified service is not available.|ServiceNotSupported|The specified service is not supported.|400|
|The error message returned because a renewal and configuration change order has not taken effect.|HasRenewChangeOrder|This instance has a renewChange order.|400|
|The error message returned because an internal error occurred.|InternalError|The request processing has failed due to some unknown error.|500|
|The error message returned because the backup time is invalid.|InvalidPreferredBackupTime|Specified preferred backup time is not valid.|400|
|The error message returned because the specified backup type is invalid.|InvalidBackupType.Format|Specified backup type is not valid.|400|
|The error message returned because the specified backup method is invalid.|InvalidBackupMethod.Format|Specified backup method is not valid.|400|
|The error message returned because the specified instance already has a backup task.|BackupJobExists|A backup job already exists in the specified DB instance.|400|
|The error message returned because the backup times exceed the upper limit.|BackupTimesExceeded|Exceeding the daily backup times of this DB instance.|400|
|The error message returned because at least one parameter must be specified.|ParameterLeastAssociate|Must input at least one optional parameter.|400|
|The error message returned because the specified backup cycle is invalid.|InvalidBackupRetentionPeriod.Malformed|Specified backup retention period is not valid.|400|
|The error message returned because the specified next backup time is invalid.|InvalidPreferredBackupTime.Format|Specified preferred backup time is not valid.|400|
|The error message returned because the specified backup cycle is invalid.|InvalidPreferredBackupPeriod.Malformed|Specified backup period is not valid.|400|
|The error message returned because the current instance type does not support this operation.|IncorrectDBInstanceType|Current DB instance type does not support this operation.|400|
|The error message returned because the specified key is invalid.|InvalidKey.Malformed|Specified key is not valid.|400|
|The error message returned because the nonce signature is used and cannot be used again.|SignatureNonceUsed|Specified signature nonce was used already.|400|
|The error message returned because no available virtual IP addresses can be allocated.|AllocateVpcIp.NotEnough|Ip resource is not enough.|400|
|The error message returned because instances of the specified type cannot be created in the zone.|Zone.NotSupport|Specified zone does not support creating with instance class.|400|
|The error message returned because the code for the instance type is invalid.|MissingClassCode|Capacity or InstanceClass is mandatory for this action.|400|
|The error message returned because the specified instance type is not supported.|InvalidDBInstanceClass.NotFound|Specified DB instance class is not found.|404|
|The error message returned because the specified instance has been locked.|IncorrectDBInstanceLockMode|Current DB instance lock mode does not support this operation.|400|
|The error message returned because the specified backup set ID does not exist.|InvalidBackupSetID.NotFound|Specified backup set ID does not exist.|400|
|The error message returned because the operation is not supported while the instance is in the current state.|IncorrectDBInstanceState|Current DB instance state does not support this operation.|400|
|The error message returned because the available resource capacity in the specified instance is insufficient.|InsufficientResourceCapacity|There is insufficient capacity available for the requested instance.|400|
|The error message returned because the specified end time is invalid.|InvalidEndTime.Format|Specified end time is not valid.|400|
|The error message returned because the specified retention period of the classic network endpoint is invalid.|InvalidClassicExpiredDays.Format|The specified classicExpiredDays format is not valid.|400|
|The error message returned because the operation is not supported while the backup set is in the current state.|IncorrectBackupSetState|Current backup set state does not support operations.|400|
|The error message returned because the specified whitelist is not correct in format.|InvalidSecurityIPList.Format|Specified security IP list format is not valid.|400|

