# MoveAppResource

Migrates one or more resources from an application to another application. The application administrator can directly migrate resources between applications. RAM users or RAM roles must obtain the write permissions on the source and destination applications before they can migrate resources between the applications. Multiple resources can be migrated at a time.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=MoveAppResource&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|MoveAppResource|The operation that you want to perform. Set the value to **MoveAppResource**. |
|ResourceIds|String|Yes|\*\*\*\*,\*\*\*\*|The ID of the resource. You can specify a maximum of 20 IDs at a time. Separate them with commas \(,\). |
|ResourceType|String|Yes|video|The type of the resource. Valid values:

 -   **video**
-   **image**
-   **attached** |
|TargetAppId|String|Yes|app-\*\*\*\*|The ID of the application to which resources are migrated. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|FailedResourceIds|List|\*\*\*\*|The ID of the resource that failed to be migrated. |
|NonExistResourceIds|List|\*\*\*\*|The ID of the resource that was not found. |
|RequestId|String|25818875-5F78-4A13-BEF6-\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=MoveAppResource
&ResourceIds=****,****
&ResourceType=video
&TargetAppId=app-****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<MoveAppResourceResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-****</RequestId>
	  <FailedResourceIds>****</FailedResourceIds>
	  <NonExistResourceIds>****</NonExistResourceIds>
</MoveAppResourceResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A13-BEF6-****",
    "FailedResourceIds":"****",
    "NonExistResourceIds":"****"
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
|Forbidden.OperateAppResource

|Invalid app permission to operate on the specified resource.

|403

|The error message returned because you are not authorized to manage resources under the destination application. |

