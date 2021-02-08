# DetachAppPolicyFromIdentity

Revokes application permissions from the specified identity. The identity may a RAM user or RAM role.

**Note:** You can grant a maximum of 10 application permissions to a RAM user or RAM role.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DetachAppPolicyFromIdentity&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DetachAppPolicyFromIdentity|The operation that you want to perform. Set the value to **DetachAppPolicyFromIdentity**. |
|AppId|String|Yes|app-\*\*\*\*|The ID of the application. This parameter is optional when the PolicyNames parameter is set to VODAppAdministratorAccess. This parameter is required when the PolicyNames parameter is set to other values.

 -   Default value: **app-1000000**.
-   For more information, see [Overview](~~113600~~). |
|IdentityName|String|Yes|\*\*\*\*|The name of the identity.

 -   Specifies the ID of the RAM user when the IdentityType parameter is set to RamUser.
-   Specifies the name of the RAM role when the IdentityType parameter is set to RamRole. |
|IdentityType|String|Yes|RamUser|The type of the identity. Valid values:

 -   **RamUser**: a RAM user.
-   **RamRole**: a RAM role. |
|PolicyNames|String|Yes|VODAppFullAccess|The name of the policy. Separate multiple policies with commas \(,\). Only system policies are supported.

 -   **VODAppFullAccess**: authorizes an identity to manage all resources in an application.
-   **VODAppReadOnlyAccess**: authorizes an identity to access all resources in an application in read-only mode.
-   **VODAppAdministratorAccess**: assigns the application administrator role to an identity. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|FailedPolicyNames|List|\*\*\*\*|The name of the policy that failed to be detached from the identity. |
|NonExistPolicyNames|List|\*\*\*\*|The name of the policy that was not found. |
|RequestId|String|25818875-5F78-4A13-\*\*\*\*-D7393642C|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DetachAppPolicyFromIdentity
&AppId=app-****
&IdentityName=****
&IdentityType=RamUser
&PolicyNames=VODAppFullAccess
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DetachAppPolicyFromIdentityResponse>
	  <RequestId>25818875-5F78-4A13-****-D7393642C</RequestId>
	  <FailedPolicyNames>****</FailedPolicyNames>
	  <NonExistPolicyNames>****x</NonExistPolicyNames>
</DetachAppPolicyFromIdentityResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A13-****-D7393642C",
    "FailedPolicyNames":"****",
    "NonExistPolicyNames":"****"
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
|Forbidden.OperateApp

|User not authorized to operate app.

|403

|The error message returned because you are not authorized to manage the application. |

