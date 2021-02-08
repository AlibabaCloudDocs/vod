# UpdateTranscodeTemplateGroup

Modifies a transcoding template group. You can modify the configurations of the specified transcoding templates in a transcoding template group.

**Note:**

-   You cannot add, modify, or remove transcoding templates in a transcoding template group that is locked in the ApsaraVideo VOD console. To manage such transcoding template groups, contact the ApsaraVideo VOD technical support.
-   You can call the GetTranscodeTemplateGroup operation to query the configurations of a transcoding template group and check whether the transcoding template group is locked by using the response parameter Locked.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UpdateTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateTranscodeTemplateGroup|The operation that you want to perform. Set the value to **UpdateTranscodeTemplateGroup**. |
|TranscodeTemplateGroupId|String|Yes|4c71a339fe\*\*\*\*\*52b4fa6f4527|The ID of the transcoding template group. |
|Name|String|No|transcodetemplate|The name of the transcoding template group.

 -   The name can be up to 128 bytes in length.
-   The value must be encoded in UTF-8. |
|TranscodeTemplateList|String|No|\[\{"Video":\{"Bitrate":"400","Codec":"H.264","Fps":"30"\},"Audio":\{"Codec":"AAC","Bitrate":"64","Definition":"SD","EncryptType":"Private","Container":\{"Format":"m3u8"\},"PackageType":"HLSPackage"\}\}\]|The configurations of the transcoding template. The value is a JSON-formatted string. For more information about the data structure, see the "TranscodeTemplate" section of the [Basic data types](~~52839~~) topic. |
|Locked|String|No|locked|The lock status of the template group. Valid values:

 -   **Enabled**: The template group is locked.
-   **Disabled**: The template group is not locked. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|TranscodeTemplateGroupId|String|34e908aa4024a\*\*\*\*\*f7821c31f93a2a|The ID of the transcoding template group. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UpdateTranscodeTemplateGroup
&TranscodeTemplateGroupId=4c71a339fe*****52b4fa6f4527
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateTranscodeTemplateGroupResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <TranscodeTemplateGroupId>34e908aa4024a*****f7821c31f93a2a</TranscodeTemplateGroupId>
</UpdateTranscodeTemplateGroupResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "TranscodeTemplateGroupId":"34e908aa4024a*****f7821c31f93a2a"
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
|InvalidStorage.NotFound

|The storage info dose not exist.

|404

|The error message returned because ApsaraVideo VOD has not allocated a bucket. |
|InvalidTranscodeTemplateGroup.NotFound

|The transcode template group does not exist.

|404

|The error message returned because the specified transcoding template group does not exist. |
|Forbidden.LockedTemplateGroup

|The transcode template group has been locked.

|403

|The error message returned because the specified template group is locked and cannot be managed. To manage the template group, contact the ApsaraVideo VOD technical support. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

