# UpdateAppInfo

Updates the information about an application.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateAppInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateAppInfo|The operation that you want to perform. Set the value to **UpdateAppInfo**. |
|AppId|String|No|app-\*\*\*\*|The ID of the application.

 -   Default value: **app-1000000**.
-   For more information, see [Overview](~~113600~~). |
|AppName|String|No|test|The name of the application.

 -   The name can contain up to 128 characters in length.
-   The name can contain only UTF-8 characters. |
|Description|String|No|my first app.|The description of the application.

 -   The description can contain up to 512 characters in length.
-   The description can contain only UTF-8 characters. |
|Status|String|No|Disable|The status of the application. Valid values:

 -   **Normal**
-   **Disable** |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A13-\*\*\*\*-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateAppInfo
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateAppInfoResponse>
  <RequestId>25818875-5F78-4A13-****-D7393642CA58</RequestId>
</UpdateAppInfoResponse>
```

`JSON` format

```
{
     "RequestId": "25818875-5F78-4A13-****-D7393642CA58"
    }
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

The following table describes the common errors that this operation can return. For more information about errors common to all operations, see [Common errors](https://help.aliyun.com/document_detail/52841.html?spm=a2c4g.11186623.2.17.72657c55cS5tmj).

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

