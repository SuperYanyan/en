# modifyVpcPeering


## Description
Modify VPCPeering API

## Request method
PUT

## Request address
https://vpc.jdcloud-api.com/v1/regions/{regionId}/vpcPeerings/{vpcPeeringId}

|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**regionId**|String|True| |Region ID|
|**vpcPeeringId**|String|True| |vpcPeeringId ID|

## Request parameter
|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**vpcPeeringName**|String|False| |VPCPeering Name, Must Provide A nName. Value Range of Name: 1-32 Chinese, English capital and lowercase letters, numbers and underline delimiter|
|**description**|String|False| |VPCPeering Description. Value Range: 0-256 Chinese, English capital and lowercase letters, numbers and underline delimiter|


## Response parameter
|Name|Type|Description|
|---|---|---|
|**vpcPeering**|VpcPeering|VPCPeering Resource Information|
|**requestId**|String|Request ID|

### VpcPeering
|Name|Type|Description|
|---|---|---|
|**vpcPeering**|VpcPeering| |
### VpcPeering
|Name|Type|Description|
|---|---|---|
|**vpcPeeringId**|String|VPCPeering ID|
|**vpcPeeringName**|String|VPCPeering name, no duplicate under the same account is allowed. Value Range: 1-32 Chinese, English capital and lowercase letters, numbers and underline delimiter|
|**vpcPeeringState**|String|Status, values include Connected, Disconnected, Initiated|
|**description**|String|VPCPeering description, can be null. Value Range: 0-256 Chinese, English capital and lowercase letters, numbers and underline delimiter|
|**vpcInfo**|VpcPeeringVpcInfo|VPC Information Launching VPCPeering|
|**remoteVpcInfo**|VpcPeeringVpcInfo|Opposite Terminal VPC information|
|**createdTime**|String|VPCPeering Creation Time|
### VpcPeeringVpcInfo
|Name|Type|Description|
|---|---|---|
|**vpcId**|String|VPC ID of Subnet|
|**vpcName**|String|VPC Name. Value Range: 1-60 Chinese, English capital and lowercase letters, numbers and underline delimiter|
|**addressPrefix**|String[]|If it is blank, segment is not limited; if it is not blank, it is 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 and their subnets included and the length of subnet mask is between 16 and 28|

## Response code
|Return code|Description|
|---|---|
|**200**|Successful operation|
|**429**|VpcPeering quota limit exceeded.|
|**404**|Resource not found|
|**409**|Already has VpcPeering with param|
