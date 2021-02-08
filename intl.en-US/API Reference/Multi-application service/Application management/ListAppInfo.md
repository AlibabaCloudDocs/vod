# ListAppInfo

Queries the applications that you are authorized to manage based on query conditions.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListAppInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListAppInfo|The operation that you want to perform. Set the value to **ListAppInfo**. |
|Status|String|No|Normal|The status of the application. After an application is created, it enters the **Normal** state. Valid values:

 -   **Normal**
-   **Disable** |
|PageNo|Integer|No|1|The number of the page to return. By default, pages start from page 1. |
|PageSize|Integer|No|10|The number of entries to return on each page. Default value: **10**. Maximum value: **100**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AppInfoList|Array of AppInfo| |The details of each application. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|AppName|String|test|The name of the application. |
|CreationTime|String|2019-03-01T08:00:00Z|The time when the application was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|my first app.|The description of the application. |
|ModificationTime|String|2019-03-01T09:00:00Z|The last time when the application was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Status|String|Normal|The status of the application. Valid values:

 -   **Normal**
-   **Disable** |
|Type|String|System|The type of the application. Valid values:

 -   **System**
-   **Custom** |
|RequestId|String|25818875-5F78-4A13-\*\*\*\*-D7393642CA58|The ID of the request. |
|Total|Integer|10|The total number of entries returned. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListAppInfo
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListAppInfoResponse>
  <RequestId>25818875-5F78-4A13-****-D7393642CA58</RequestId>
  <Total>10</Total>
  <AppInfoList>
        <Status>Normal</Status>
        <Type>System</Type>
        <Description>my first app. </Description>
        <AppId>app-****</AppId>
        <CreationTime>2019-03-01T08:00:00Z</CreationTime>
        <ModificationTime>2019-03-01T09:00:00Z</ModificationTime>
        <AppName>test</AppName>
  </AppInfoList>
</ListAppInfoResponse>
```

`JSON` format

```
{
	"RequestId": "25818875-5F78-4A13-****-D7393642CA58",
	"Total": "10",
	"AppInfoList": [{
		"Status": "Normal",
		"Type": "System",
		"Description": "my first app.",
		"AppId": "app-****",
		"CreationTime": "2019-03-01T08:00:00Z",
		"ModificationTime": "2019-03-01T09:00:00Z",
		"AppName": "test"
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

