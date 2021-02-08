# DeleteAppInfo

Deletes an application.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteAppInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAppInfo|The operation that you want to perform. Set the value to **DeleteAppInfo**. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A13-BEF6-\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteAppInfo
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteAppInfoResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-****</RequestId>
</DeleteAppInfoResponse>
```

`JSON` format

```
{
     "RequestId": "25818875-5F78-4A13-BEF6-****"
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
|Forbidden.ResourceNotEmpty

|The App: app-\*\***has**\*\* resource, can not be deleted.

|403

|The error message returned because the application has resources. |

