# describeRouteTable


## Description
Query route table information details

## Request method
GET

## Request address
https://vpc.jdcloud-api.com/v1/regions/{regionId}/routeTables/{routeTableId}

|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**regionId**|String|True| |Region ID|
|**routeTableId**|String|True| |RouteTable ID|

## Request parameter
None


## Response parameter
|Name|Type|Description|
|---|---|---|
|**result**|Result|Returned Results|
|**requestId**|String|Request ID|

### Result
|Name|Type|Description|
|---|---|---|
|**routeTable**|RouteTable|Route table resource information|
### RouteTable
|Name|Type|Description|
|---|---|---|
|**routeTableId**|String|Route Table ID|
|**routeTableName**|String|Route table name, only allow Chinese, numbers, capital and lowercase letters, English underline “_” and line-through “-”, must provide a name which cannot exceed 32 characters.|
|**routeTableType**|String|Route Table Type, Default: default route table, Custom: customized route table|
|**description**|String|Route table description information, allow all characters under UTF-8 coding, which cannot exceed 256 characters.|
|**vpcId**|String|VPC ID|
|**routeTableRules**|RouteTableRule[]|Route Table Rule Information|
|**subnetIds**|String[]|Route Table Associated Subnet List|
|**createdTime**|String|Creation Time of Route Table|
### RouteTableRule
|Name|Type|Description|
|---|---|---|
|**ruleId**|String|Route Table Rule ID|
|**priority**|Number|Rule Matching Priority. Value Range: [1,255], default value is 100. When routing rule subnet masks are different, the longest routing will match the priority; when routing rule subnet masks are the same, forwarding is based on priority matching, where the smaller the priority number is, the higher priority it is; when the routing rule subnet masks and the priority are the same but the next is different, the equal-cost routing is constituted and the load of next is balanced.|
|**nextHopType**|String|Type of Next. Value Range: local:local, instance: Virtual Machine, internet: public network, VPC_peering: VPC peering connection, bgw: border gateway|
|**nextHopId**|String|Next ID|
|**addressPrefix**|String|Prefix of matching address, addressPrefix of internet type route and other types of routes is not allowed to be duplicate|

## Response code
|Return code|Description|
|---|---|
|**200**|OK|
|**400**|invalid parameter|
|**401**|Authentication failed|
