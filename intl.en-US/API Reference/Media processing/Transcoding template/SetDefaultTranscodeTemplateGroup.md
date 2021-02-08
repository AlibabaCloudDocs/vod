# SetDefaultTranscodeTemplateGroup

Specifies a transcoding template as the default one.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SetDefaultTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetDefaultTranscodeTemplateGroup|The operation that you want to perform. Set the value to **SetDefaultTranscodeTemplateGroup**. |
|TranscodeTemplateGroupId|String|Yes|d58079958be8d\*\*\*\*\*b699ab7ab6e1bf|The ID of the transcoding template group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SetDefaultTranscodeTemplateGroup
&TranscodeTemplateGroupId=d58079958be8d*****b699ab7ab6e1bf
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetDefaultTranscodeTemplateGroupResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</SetDefaultTranscodeTemplateGroupResponse>
```

`JSON` format

```
{
  "RequestId": "25818875-5F78-4A*****F6-D7393642CA58"
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
|InvalidTranscodeTemplateGroup.NotFound

|The transcode template group does not exist.

|404

|The error message returned because the specified transcoding template group does not exist. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

