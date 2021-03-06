# createInstances


## Description
Create one or more Cloud Physical Servers with specified configuration<br/>
- Region and Availability Zone<br/>
  - The region and availability zone supported by the Cloud Physical Servers can be obtained by calling API (describeRegions)<br/>
- Instance Type Family<br/>
  - The physical instance type family list can be obtained by calling APIs<br/>
  - Instance type family which is off line or sold out is not available for use<br/>
- Operating System and Pre-installed Software<br/>
  - The operating system list supported by the Cloud Physical Server can be obtained by calling API (describeOS)<br/>
- Storage<br/>
  - Multiple RAIDs are available for the data disk and the RAID list supported by the server can be obtained by calling API (describeDeviceRaids)<br/>
- Network<br/>
  - Network type currently only supports basic<br/>
  - ISP Line only supports bgp currently<br/>
  - Disabled Internet is supported. If the Internet is enabled, the bandwidth range is [1,200], in unit Mbps<br/>
- Miscellaneous<br/>
  - Purchase duration can be under monthly package: month value range[1,9], year value range [1,3]<br/>
  - Refer to the Public Parameter Specification for password setting<br/>


## Request method
PUT

## Request address
https://cps.jdcloud-api.com/v1/regions/{regionId}/instances

|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**regionId**|String|True| |Region ID, the Region and Availability Zone Supported by the Cloud Physical Servers can be Obtained by Calling API (describeRegions)|

## Request parameter
|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**clientToken**|String|False| |Generated by the client to ensure the idempotence of the request, and the length cannot exceed 36 characters;<br/><br>If multiple requests use the same clientToken, only the first request will be executed, and the following requests will directly return the result of the first request<br/><br>|
|**instanceSpec**|InstanceSpec|True| |Description of Cloud Physical Server Configuration|

### InstanceSpec
|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**az**|String|True| |Availability Zone, such as cn-east-1|
|**deviceType**|String|True| |Instance Type Family, such as cps.c.normal|
|**hostname**|String|False| |Machine Name|
|**imageType**|String|True| |Image Type, Value Range: Standard, Standard_app|
|**osTypeId**|String|True| |Operating System Type ID|
|**sysRaidTypeId**|String|True| |System Disk RAID Type ID|
|**dataRaidTypeId**|String|True| |Data Disk RAID Type ID|
|**subnetId**|String|False| |Subnet Number|
|**enableInternet**|String|False|yes|Whether to Enable Internet, Value Range: yes/no|
|**enableIpv6**|String|False|yes|Whether to enable IPv6, value range: yes, no|
|**networkType**|String|True| |Network Type, Currently Only Support Basic|
|**cidr**|String|False| |Network CIDR|
|**lineType**|String|False| |Internet Link Type, Currently Only Support Bgp|
|**bandwidth**|Integer|False| |Internet bandwidth, Range [1,200] Unit: Mbps|
|**name**|String|True| |Name of Cloud Physical Server|
|**description**|String|False| |Description of Cloud Physical Server|
|**password**|String|True| |Password|
|**count**|Integer|True| |Purchase Count|
|**charge**|ChargeSpec|True| |Billing Configuration|
|**softwares**|Software[]|False| | |
### Software
|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**name**|String|False| |Software Package Name|
|**version**|String|False| |Software Package Version|
|**osTypeId**|String|False| |Operating System Type ID|
|**description**|String|False| |Software Package Description|
### ChargeSpec
|Name|Type|Required or not|Default value|Description|
|---|---|---|---|---|
|**chargeMode**|String|False|postpaid_by_duration|Billing model value is prepaid_by_duration, postpaid_by_usage or postpaid_by_duration; prepaid_by_duration means Pay-In-Advance, postpaid_by_usage means Pay-As-You-Go By Consumption and postpaid_by_duration means pay by configuration; is postpaid_by_duration by default. Please refer to the Help Documentation of specific product line to confirm the billing type supported by the production line|
|**chargeUnit**|String|False| |Billing unit of Pay-In-Advance, the Pay-In-Advance is compulsory, and valid only when chargeMode is prepaid_by_duration, and the value is month or year and month by default|
|**chargeDuration**|Integer|False| |Pay-In-Advance billing duration, the Pay-In-Advance is compulsory and valid only when the value of chargeMode is prepaid_by_duration. When chargeUnit is month, the value shall be 1~9; when chargeUnit is year, the value shall be 1, 2 or 3|

## Response parameter
|Name|Type|Description|
|---|---|---|
|**result**|Result| |
|**requestId**|String| |

### Result
|Name|Type|Description|
|---|---|---|
|**instanceIds**|String[]| |

## Response code
|Return code|Description|
|---|---|
|**200**|OK|
|**400**|Bad request|
|**404**|Not found|
|**500**|Internal server error|
|**503**|Service unavailable|
