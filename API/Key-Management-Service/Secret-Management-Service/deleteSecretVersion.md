# deleteSecretVersion


## Description
Delete confidentiality of specified version

## Request Method
DELETE

## Request Address
https://kms.jdcloud-api.com/v1/secret/{secretId}/version/{version}:delete

|Name|Type|Required or Not|Default Value|Description|
|---|---|---|---|---|
|**secretId**|String|True| |Confidentiality ID|
|**version**|String|True| |Confidential version|

## Request Parameter
None


## Return Parameter
|Name|Type|Description|
|---|---|---|
|**requestId**|String|Request ID|


## Return Code
|Return Code|Description|
|---|---|
|**200**|OK|
|**404**|Not found|
