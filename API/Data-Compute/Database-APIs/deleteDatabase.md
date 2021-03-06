# deleteDatabase


## Description
Delete a specified database of user instance

## Request method
DELETE

## Request address
https://xdata.jdcloud-api.com/v1/regions/{regionId}/dwDatabase/{databaseName}

|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**databaseName**|String|True| |Database Name|
|**regionId**|String|True| |Region ID|

## Request parameter
|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**instanceName**|String|True| |Instance Name|


## Response parameter
|Name|Type|Description|
|---|---|---|
|**requestId**|String| |
|**result**|Result| |


### Result
|Name|Type|Description|
|---|---|---|
|**message**|String| |
|**status**|Boolean| |

## Response code
|Return code|Description|
|---|---|
|**200**|OK|
|**500**|Internal server error|
