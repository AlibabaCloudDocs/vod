# AddTranscodeTemplateGroup

Creates a transcoding template group or adds one or more transcoding templates to a template group.

**Note:**

-   You cannot perform custom operations on transcoding template groups that are **locked** in the ApsaraVideo VOD console. To manage such transcoding template groups, submit a ticket.
-   An Object Storage Service \(OSS\) bucket is required for storing the files that are involved in transcoding. You can create a transcoding template group only after ApsaraVideo VOD has allocated a bucket to you. You can activate the bucket on the Storage page in the ApsaraVideo VOD console.
-   You cannot add transcoding templates to the No Transcoding template group.
-   You can create a maximum of 20 transcoding template groups.
-   You can add a maximum of 20 transcoding templates to a transcoding template group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=AddTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AddTranscodeTemplateGroup|The operation that you want to perform. Set the value to **AddTranscodeTemplateGroup**. |
|Name|String|No|transcodetemplate|The name of the transcoding template group.

 -   The name can be up to 128 bytes in length.
-   The value must be encoded in UTF-8. |
|TranscodeTemplateList|String|No|\[\{"Video":\{"Bitrate":"400","Codec":"H.264","Fps":"30"\},"Audio":\{"Codec":"AAC","Bitrate":"64","Definition":"SD","EncryptType":"Private","Container":\{"Format":"m3u8"\},"PackageType":"HLSPackage"\}\}\]|The configurations of the transcoding template. The value is a JSON-formatted string. For more information about the data structure, see the "TranscodeTemplate" section of the [Basic data types](~~52839~~) topic. |
|TranscodeTemplateGroupId|String|No|4c71a339fe\*\*\*\*\*52b4fa6f4527|The ID of the transcoding template group. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

**Note:**

-   If you do not set the **TranscodeTemplateList** parameter in the request, no transcoding process is initiated. Transcoding is not triggered after a video file is uploaded.
-   You must set one of the **TranscodeTemplateGroupId** and **Name** parameters in the request.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|TranscodeTemplateGroupId|String|34e908aa4024a\*\*\*\*\*f7821c31f93a2a|The ID of the transcoding template group. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=AddTranscodeTemplateGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AddTranscodeTemplateGroupResponse>
	  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <TranscodeTemplateGroupId>34e908aa4024a*****f7821c31f93a2a</TranscodeTemplateGroupId>
</AddTranscodeTemplateGroupResponse>
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
|Forbidden.SpecialTemplateGroup

|The transcode template group is using for special purpose.

|403

|The error message returned because the specified transcoding template group is a special one, such as the No Transcoding or Storage Only template group. You cannot add transcoding templates to the special transcoding template group. |
|TrasncodeTemplateGroupExceededMax

|The transcode template group size exceeded maximum.

|400

|The error message returned because the number of transcoding template groups exceeds the upper limit. You can create a maximum of 20 transcoding template groups. |
|TranscodeTemplateExceededMax

|The template transcode template config size exceeded maximum.

|400

|The error message returned because the number of transcoding templates that are added to the specified transcoding template group exceeds the upper limit. You can add a maximum of 20 transcoding templates to a transcoding template group. |
|WatermarkExceededMax

|The watermark size exceeded maximum.

|400

|The error message returned because the number of watermark IDs that are associated with a single transcoding template in the transcoding template group exceeds the upper limit. You can associate a maximum of four watermark IDs with a transcoding template. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

