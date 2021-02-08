# GetAppInfos

Queries the information about one or more applications based on application IDs.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetAppInfos&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetAppInfos|The operation that you want to perform. Set the value to **GetAppInfos**. |
|AppIds|String|Yes|app-\*\*\*\*|The ID of the application. You can specify a maximum of 10 application IDs. Separate them with commas \(,\). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AppInfoList|Array of AppInfo| |The details of each application. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|AppName|String|test|The name of the application. |
|CreationTime|String|2019-03-01T08:00:00Z|The time when the application was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|\*\*\*\*|The description of the application. |
|ModificationTime|String|2019-03-01T09:00:00Z|The last time when the application was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Status|String|Normal|The status of the application. Valid values:

 -   **Normal**
-   **Disable** |
|Type|String|System|The type of the application. Valid values:

 -   **System**
-   **Custom** |
|NonExistAppIds|List|\*\*\*\*|The ID of the application that was not found. |
|RequestId|String|25818875-5F78-4A13-\*\*\*\*-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetAppInfos
&AppIds=app-****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetAppInfosResponse>
  <RequestId>25818875-5F78-4A13-****-D7393642CA58</RequestId>
  <AppInfoList>
        <Status>Normal</Status>
        <Type>System</Type>
        <Description>****</Description>
        <AppId>app-****</AppId>
        <CreationTime>2019-03-01T08:00:00Z</CreationTime>
        <ModificationTime>2019-03-01T09:00:00Z</ModificationTime>
        <AppName>test</AppName>
  </AppInfoList>
  <NonExistAppIds>****</NonExistAppIds>
</GetAppInfosResponse>
```

`JSON` format

```
{
	"RequestId": "25818875-5F78-4A13-****-D7393642CA58",
	"AppInfoList": [{
		"Status": "Normal",
		"Type": "System",
		"Description": "****",
		"AppId": "app-****",
		"CreationTime": "2019-03-01T08:00:00Z",
		"ModificationTime": "2019-03-01T09:00:00Z",
		"AppName": "test"
	}],
	"NonExistAppIds": "****"
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

