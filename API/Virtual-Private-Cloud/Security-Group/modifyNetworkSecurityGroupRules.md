# modifyNetworkSecurityGroupRules


## Description
Modify security group rule

## Request method
POST

## Request address
https://vpc.jdcloud-api.com/v1/regions/{regionId}/networkSecurityGroups/{networkSecurityGroupId}:modifyNetworkSecurityGroupRules

|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**regionId**|String|True| |Region ID|
|**networkSecurityGroupId**|String|True| |NetworkSecurityGroup ID|

## Request parameter
|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**modifySecurityGroupRuleSpecs**|ModifySecurityGroupRules[]|True| |Security Group Rule Information|

### ModifySecurityGroupRules
|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**ruleId**|String|True| |Security Group Rule ID.|
|**protocol**|Number|False| |Rule Limits Protocol. 300:All; 6:TCP; 17:UDP; 1:ICMP|
|**fromPort**|Integer|False| |Start Port of Security Group Rule. Value Range: 1-65535|
|**toPort**|Integer|False| |End Port of Security Group Rule. Value Range: 1-65535|
|**addressPrefix**|String|False| |Prefix of Security Group Rule. Value Range: correct CIDR        |
|**description**|String|False| |Security Group Rule Description. Value Range: 0-256 of all characters entered under UTF-8 coding|

## Response parameter
|Name|Type|Description|
|---|---|---|
|**requestId**|String|Request ID|


## Response code
|Return code|Description|
|---|---|
|**200**|Successful operation|
|**400**|invalid parameter|
|**404**|SecurityGroup or SecurityGroupRule not found|
|**500**|Internal server error|
