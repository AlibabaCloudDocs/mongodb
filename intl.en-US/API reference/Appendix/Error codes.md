# Error codes {#reference7153 .reference}

|Description|Error code|Error message|HTTP status code|
|:----------|:---------|:------------|:---------------|
|The error message returned when unauthorized users call the operation.|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn’t support RAM.|403|
|The error message returned when this operation is not available for RAM users.|Forbedden.NotSupportRAM|This action does not support accessed by RAM mode.|403|
|The error message returned when an exception occurs on the server.|ServiceUnavailable|The request has failed due to a temporary failure of the server.|503|
|The error message returned when the specified instance status does not exist.|InvalidStatus.NotFound|The Status provided does not exist in our records.|404|
|The error message returned when the input parameter is invalid.|InvalidParameter|The specified parameter "InstanceName" is not valid.|400|
|The error message returned when a normal user other than an administrator calls the management operation.|Forbbiden.NotAdminUser|User not authorized to operate on the specified API as you are not the administrator.|403|
|The error message returned when a required parameter is not specified.|MissingParameter|Specified parameter is missing.|400|
|The error message returned when neither the InstanceName nor NewPassword parameter is specified.|MissingParameter|InstanceName/NewPassword at least one is mandatory for this action.|400|
|The error message returned when the OwnerId parameter is not specified.|MissingParameter|The input parameter OwnerId,OwnerAccount that is mandatory for process this request is not supplied.|403|
|The error message returned when the specified Token parameter is invalid.|InvalidToken.Malformed|The Specified parameter \\”Token\\” is not valid.|400|
|The error message returned when the specified InstanceName parameter is invalid.|InvalidInstanceName.Malformed|The Specified parameter \\”InstanceName\\” is not valid.|400|
|The error message returned when the specified Password parameter is invalid.|InvalidPassword.Malformed|The Specified parameter \\”Password\\” is not valid.”|400|
|The error message returned when the specified Instances parameter is invalid.|InvalidInstances.Malformed|The Specified parameter \\”Instances\\” is not valid.|400|
|The error message returned when the specified StartTime parameter is invalid.|InvalidStartTime.Malformed|The Specified parameter \\”StartTime\\” is not valid.|400|
|The error message returned when the specified EndTime parameter is invalid.|InvalidEndTime.Malformed|The Specified parameter \\”EndTime\\” is not valid.|400|
|The error message returned when the specified InstanceIds parameter is invalid.|InvalidInstanceIds.Malformed|The Specified parameter \\”InstanceIds\\” is not valid.|400|
|The error message returned when your account balance is insufficient.|InsufficientBalance|Your account does not have enough balance.|400|
|The error message returned when the specified user has not performed real-name authentication.|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|403|
|The error message returned when your instance quota has been exhausted.|QuotaExceed|Living afterpay instances quota exceeded.|400|
|The error message returned when the capacity configuration is invalid.|InvalidCapacity.NotFound|The Capacity provided does not exist in our records.|400|
|The error message returned when a different request uses a client token that was used for a previous request.|IdempotentParameterMismatch|Request uses a client token in a previous request but is not identical to that request.|400|
|The error message returned when there is insufficient inventory in the specified zone.|QuotaNotEnough|Quota not enough in this zone.|400|
|The error message returned when you are unauthorized to use the subscription operation.|Forbbiden.SubUser|The specified action is not available for you.|403|
|The error message returned when the risk control system rejects the access attempt.|Forbidden.RiskControl|This operation is forbidden by Aliyun Risk Control system.|403|
|The error message returned when the specified region does not exist.|InvalidRegion.NotFound|The RegionId or ZoneId provided does not exist in our records.|404|
|The error message returned when the specified ZoneId parameter is invalid.|InvalidZoneId.NotFound|The ZoneId provided is invalid.|400|
|The error message returned when the specified instance ID does not exist.|InvalidInstanceId.NotFound|The InstanceId provided does not exist in our records.|404|
|The error message returned when the password is incorrect.|IncorrectPassword|The Password provided is not correct.|400|
|The error message returned when the specified service is unavailable.|ServiceNotSupported|The specified service is not supported.|400|
|The error message returned when the instance has a renewal and reconfiguration that has not taken effect.|HasRenewChangeOrder|This instance has a renewChange order.|400|
|The error message returned when an internal error occurs.|InternalError|The request processing has failed due to some unknown error.|500|
|The error message returned when the backup time is invalid.|InvalidPreferredBackupTime|Specified preferred backup time is not valid.|400|
|The error message returned when the input backup type is invalid.|InvalidBackupType.Format|Specified backup type is not valid.|400|
|The error message returned when the input backup method is invalid.|InvalidBackupMethod.Format|Specified backup method is not valid.|400|
|The error message returned when the backup task already exists.|BackupJobExists|A backup job already exists in the specified DB instance.|400|
|The error message returned when the number of times the instance is backed up has exceeded the upper limit.|BackupTimesExceeded|Exceeding the daily backup times of this DB instance.|400|
|The error message returned when no optional parameters are specified.|ParameterLeastAssociate|Must input at least one optional parameter.|400|
|The error message returned when the specified backup retention period is invalid.|InvalidBackupRetentionPeriod.Malformed|Specified backup retention period is not valid.|400|
|The error message returned when the specified next backup time is invalid.|InvalidPreferredBackupTime.Format|Specified preferred backup time is not valid.|400|
|The error message returned when the specified backup retention period is invalid.|InvalidPreferredBackupPeriod.Malformed|Specified backup period is not valid.|400|
|The error message returned when the current instance type does not support this operation.|IncorrectDBInstanceType|Current DB instance type does not support this operation.|400|
|The error message returned when the specified key is invalid.|InvalidKey.Malformed|Specified key is not valid.|400|
|The error message returned when the signature has been used.|SignatureNonceUsed|The specified SignatureNonce has already been used.|400|
|The error message returned when no more virtual IP address can be assigned.|AllocateVpcIp.NotEnough|Ip resource is not enough.|400|
|The error message returned when the instances of the specified type cannot be created in the zone.|Zone.NotSupport|Specified zone does not support creating with instance class.|400|
|The error message returned when the specification code is invalid.|MissingClassCode|Capacity or InstanceClass is mandatory for this action.|400|
|The error message returned when the specified instance type is not supported.|InvalidDBInstanceClass.NotFound|Specified DB instance class is not found.|404|
|The error message returned when the instance is locked.|IncorrectDBInstanceLockMode|Current DB instance lock mode does not support this operation.|400|
|The error message returned when the backup set ID does not exist.|InvalidBackupSetID.NotFound|Specified backup set ID does not exist.|400|
|The error message returned when the instance is in a state that does not support the current operation.|IncorrectDBInstanceState|Current DB instance state does not support this operation.|400|
|The error message returned when the resources are insufficient.|InsufficientResourceCapacity|There is insufficient capacity available for the requested instance.|400|
|The error message returned when the input end time is invalid.|InvalidEndTime.Format|Specified end time is not valid.|400|
|The error message returned when the duration for the reserved classic IP address is invalid.|InvalidClassicExpiredDays.Format|The specified classicExpiredDays format is not valid.|400|
|The error message returned when the backup set is in a state that does not support the current operation.|IncorrectBackupSetState|Current backup set state does not support operations.|400|
|The error message returned when the whitelist format is invalid.|InvalidSecurityIPList.Format|Specified security IP list format is not valid.|400|

