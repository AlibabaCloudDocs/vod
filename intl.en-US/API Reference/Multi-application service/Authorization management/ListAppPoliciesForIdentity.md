# ListAppPoliciesForIdentity

Queries the application policies that are attached to the specified identity. The identity may be a RAM user or RAM role.

**Note:** The IdentityType and IdentityName parameters take effect only when an identity assumes the application administrator role to call this operation. Otherwise, only application policies that are attached to the current identity are returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListAppPoliciesForIdentity&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListAppPoliciesForIdentity|The operation that you want to perform. Set the value to **ListAppPoliciesForIdentity**. |
|IdentityName|String|Yes|\*\*\*\*|The name of the identity.

 -   Specifies the ID of the RAM user when the IdentityType parameter is set to RamUser.
-   Specifies the name of the RAM role when the IdentityType parameter is set to RamRole. |
|IdentityType|String|Yes|RamUser|The type of the identity. Valid values:

 -   **RamUser**: a RAM user.
-   **RamRole**: a RAM role. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AppPolicyList|Array of AppPolicy| |The details of each policy.

 **Note:** A maximum of 100 entries can be returned. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|CreationTime|String|2019-01-01T01:01:01Z|The time when the application policy was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|App full access permission|The description of the policy. |
|ModificationTime|String|2019-01-01T01:08:01Z|The last time when the application policy was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|PolicyName|String|VODAppFullAccess|The name of the policy. |
|PolicyType|String|System|The type of the policy. Valid values:

 -   **System**
-   **Custom** |
|PolicyValue|String|\*\*\*\*|The content of the policy. |
|RequestId|String|C9F3E715-B3B8-4D\*\*\*\*\*27-3A70346F0E04|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListAppPoliciesForIdentity
&IdentityName=****
&IdentityType=RamUser
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListAppPoliciesForIdentityResponse>
  <RequestId>C9F3E715-B3B8-4D*****27-3A70346F0E04</RequestId>
  <AppPolicyList>
        <PolicyType>System</PolicyType>
        <Description>App full access permission</Description>
        <AppId>app-****</AppId>
        <PolicyName>VODAppFullAccess</PolicyName>
        <PolicyValue>****</PolicyValue>
        <CreationTime>2019-01-01T01:01:01Z</CreationTime>
        <ModificationTime>2019-01-01T01:08:01Z</ModificationTime>
  </AppPolicyList>
</ListAppPoliciesForIdentityResponse>
```

`JSON` format

```
{
	"RequestId": "C9F3E715-B3B8-4D*****27-3A70346F0E04",
	"AppPolicyList": [{
		"PolicyType": "System",
		"Description": "App full access permission",
		"AppId": "app-****",
		"PolicyName": "VODAppFullAccess",
		"PolicyValue": "****",
		"CreationTime": "2019-01-01T01:01:01Z",
		"ModificationTime": "2019-01-01T01:018:01Z"
	}]
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
|OperationDenied.NotOpenAppService

|The app service is not open.

|403

|The error message returned because the multi-application service has not been activated. |

