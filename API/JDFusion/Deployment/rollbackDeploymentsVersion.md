# rollbackDeploymentsVersion


## Description
Application Deployment Rollback

## Request Method
PUT

## Request Address
https://jdfusion.jdcloud-api.com/v1/regions/{regionId}/deployments/{id}/versions/{version_id}:rollback

|Name|Type|Required or Not|Default Value|Description|
|---|---|---|---|---|
|**id**|String|True| |deployment ID|
|**regionId**|String|True| |Region ID|
|**version_id**|String|True| |application ID|

## Request Parameter
|Name|Type|Required or Not|Default Value|Description|
|---|---|---|---|---|
|**x-jdcloud-fusion-cloudid**|String|False| |Cloud Registration Information ID|


## Return Parameter
|Name|Type|Description|
|---|---|---|
|**requestId**|String|Request ID|
|**result**|Result| |

### Result
|Name|Type|Description|
|---|---|---|
|**deployment**|DeploymentInfo| |
### DeploymentInfo
|Name|Type|Description|
|---|---|---|
|**content**|DeploymentResourcesInfo| |
|**info**|DeploymentBaseInfo| |
### DeploymentResourcesInfo
|Name|Type|Description|
|---|---|---|
|**diskAttachment**|Object| |
|**disks**|Object| |
|**eipAssociate**|Object| |
|**eips**|Object| |
|**httpListeners**|Object| |
|**keypairs**|Object| |
|**netInterfaceAttachment**|Object| |
|**networkInterfaces**|Object| |
|**securityGroups**|Object| |
|**slbs**|Object| |
|**subnets**|Object| |
|**variables**|Object| |
|**vms**|Object| |
|**vpcs**|Object| |
|**vserverGroups**|Object| |
### DeploymentBaseInfo
|Name|Type|Description|
|---|---|---|
|**cloudId**|String|ID of Cloud|
|**createdTime**|String|Creation Time|
|**description**|String|Description|
|**id**|String|ID|
|**name**|String|Name|
|**readOnly**|Integer|Whether it is read-only  0: No 1: Yes|
|**updatedTime**|String|Update Time|
|**userId**|String|User ID|
|**version**|String|Version|

## Return Code
|Return Code|Description|
|---|---|
|**202**|ACCEPTED|
|**404**|not found|
