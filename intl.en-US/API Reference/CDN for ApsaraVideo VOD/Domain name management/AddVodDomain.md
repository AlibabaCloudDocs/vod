# AddVodDomain

Adds a domain name for CDN to ApsaraVideo VOD. You can add only one domain name for CDN to ApsaraVideo VOD each time. You can add a maximum of 20 domain names for CDN within an Alibaba Cloud account.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   Before you add a domain name for CDN, you must activate [ApsaraVideo VOD](~~51512~~) and apply for an Internet content provider \(ICP\) filing for domain name.
-   If the content on the origin server is not stored on Alibaba Cloud, the content must be reviewed by Alibaba Cloud. The review will be complete by the end of the next business day after you submit an application.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=AddVodDomain&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AddVodDomain|The operation that you want to perform. Set the value to **AddVodDomain**. |
|DomainName|String|Yes|example.com|The domain name for CDN that you want to add to ApsaraVideo VOD. Wildcard domain names are supported. Start the domain name with a period \(.\). Example: .example.com. |
|Sources|String|Yes|\[\{"content":"1.1.1.1","type":"ipaddr","priority":"20","port":80\}\]|The information about the address of the origin server. For more information about the Sources parameter, see the **Sources** section. |
|CheckUrl|String|No|www.example.com/test.html|The URL that is used for health checks. |
|Scope|String|No|domestic|This parameter is applicable to users of level 3 or higher in mainland China and users outside mainland China. Valid values:

 -   **domestic**: mainland China. This is the default value.
-   **overseas**: outside mainland China.
-   **global**: regions in and outside mainland China. |
|TopLevelDomain|String|No|example.com|The top-level domain name. |

## Sources

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|type

|String

|Yes

|The type of the origin server. Valid values:

 **ipaddr**: a server that you can access by using an IP address.

 **domain**: a server that you can access by using a domain name.

 **oss**: an Object Storage Service \(OSS\) bucket. |
|content

|String

|Yes

|The address of the origin server. You can specify an IP address or a domain name. |
|port

|Integer

|No

|The port number. You can specify port **443** or **80**. Default value: **80**. If you specify port **443**, Alibaba Cloud CDN communicates with the origin server over HTTPS. You can also customize a port. |
|priority

|String

|No

|The priority of the origin server if multiple origin servers are specified. Valid values: **20** and **30**. Default value: **20**. A value of **20** indicates that the origin server is the primary origin server. A value of **30** indicates that the origin server is a secondary origin server. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|15C66C7B-671A-4297-\*\*\*\*-2C4477247A74|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=AddVodDomain
&DomainName=example.com
&Sources=[{"content":"1.1.1.1","type":"ipaddr","priority":"20","port":80}]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AddVodDomainResponse>
      <RequestId>15C66C7B-671A-4297-****-2C4477247A74</RequestId>
</AddVodDomainResponse>
```

`JSON` format

```
{
  "RequestId": "15C66C7B-671A-4297-****-2C4477247A74"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## Common errors

The following table describes the common errors that this operation can return.

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|InvalidDomainName.Malformed

|Specified DomainName is malformed.

|400

|The error message returned because the value of the DomainName parameter is invalid. |
|InvalidCdnType.Malformed

|Specified CdnType is malformed.

|400

|The error message returned because the value of the CdnType parameter is invalid. |
|InvalidSourceType.Malformed

|Specified SourceType is malformed.

|400

|The error message returned because the value of the SourceType parameter is invalid. |
|InvalidSources.Malformed

|Specified Sources is malformed.

|400

|The error message returned because the origin address does not match the origin type. |
|InvalidScope.Malformed

|Specified Scope is malformed.

|400

|The error message returned because the value of the Scope parameter is invalid. |
|InvaildParameter

|The Certificate you provided is malformed!

|400

|The error message returned because the total length of the HTTPS certificate and private key exceeds the upper limit. |
|BusinessExist

|Business exist do not repeated submission

|400

|The error message returned because the domain name is being added. Do not repeat the operation. |
|DomainAlreadyExist

|This domain name is exist already

|400

|The error message returned because the domain name has been added. |
|DomainOverLimit

|The Number of Domain is over the limit

|403

|The error message returned because the number of domain names that can be added exceeds the upper limit. |
|DomainNotRegistration

|The Domain name is not registered

|404

|The error message returned because the domain name does not have an ICP filing. |
|IllegalOperation

|Illegal domain operate is not permitted.

|403

|The error message returned because you are not authorized to perform this operation. |
|ServiceBusy

|The specified Domain is configuring, please retry later.

|403

|The error message returned because the domain name is being configured. Try again later. |
|InvalidDomain.NotFound

|The domain provided does not belong to you.

|404

|The error message returned because the domain name does not exist or does not belong to you. |
|InnerAddDomainDenied

|Your account haven't bind aoneId, can not add domain.

|400

|The error message returned because you cannot add a domain name by using an internal account that is not bound to an Aone ID. |
|ExtensiveAndAllBothExist

|Extensive domain and the domain begins with 'all.' can not exist at the same time.

|400

|The error message returned because wildcard domain names and domain names that start with all. exist at the same time. |
|CdnTypeNotSupportExtensiveDomain

|Extensive domain not supported for this cdn type.

|400

|The error message returned because wildcard domain names are not supported for the specified business type. |
|ExtensiveAndSpecificDomainConflict

|Extensive domain and corresponding specific domain are mutually exclusive.

|400

|The error message returned because the wildcard domain name matches an exact domain name. Wildcard domain names are mutually exclusive with the matching exact domain names. |
|InvalidParameter

|Add live region parameters have error.

|400

|The error message returned because the system failed to specify the region parameter for the ApsaraVideo Live service. |
|InvalidRegion.Malformed

|Specified Region is malformed.

|400

|The error message returned because the value of the region parameter is invalid. |
|InvalidResourceGroupId.Malformed

|Specified ResourceGroupId is malformed.

|400

|The error message returned because the value of the ResourceGroupId parameter is invalid. |
|EntityNotExists.ResourceGroup

|The resource group does not exist.

|400

|The error message returned because the resource group does not exist. |
|InvalidStatus.ResourceGroup

|It’s now allowed to do this operation because of the current status of resource-group.

|400

|The error message returned because the resource group is in an invalid state. |
|InvalidPriorities.Malformed

|The length of priorities is not the same with source.

|400

|The error message returned because the number of priorities does not match the number of origin servers. |
|NotInternationRealIdentity

|You need to do real name authentication when you use Chinese mainland resources.

|400

|The error message returned because you have not completed the real-name verification that is required to use resources in mainland China. |

