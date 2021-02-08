# CreateAppInfo

Creates an application.

**Note:** For more information, see [Overview](~~113600~~). You can create a maximum of **10** applications within an Alibaba Cloud account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=CreateAppInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAppInfo|The operation that you want to perform. Set the value to **CreateAppInfo**. |
|AppName|String|No|test|The name of the application, which must be unique.

-   The name can contain up to 128 characters in length.
-   The name can contain only UTF-8 characters. |
|Description|String|No|myfirstapp|The description of the application.

-   The description can contain up to 512 characters in length.
-   The description can contain only UTF-8 characters. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AppId|String|app-\*\*\*\*|The ID of the application. |
|RequestId|String|25818875-5F78-4A13-\*\*\*\*-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=CreateAppInfo
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateAppInfoResponse>
      <RequestId>25818875-5F78-4A13-****-D7393642CA58</RequestId>
      <AppId>app-****</AppId>
</CreateAppInfoResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A13-****-D7393642CA58",
    "AppId": "app-****"
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
|AlreadyExist.AppName

|The specified AppName has already exist.

|409

|The error message returned because the name of the application already exists. |
|LimitExceeded.AppCount

|App Count has exceeded 10.

|400

|The error message returned because the number of applications that can be created exceeds the upper limit. |

