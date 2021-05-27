# CreateUploadVideo

Obtains a URL and a credential for uploading a video and generates the video ID.

**Note:** This operation also supports audio. For more information, see [Upload URLs and credentials](~~55397~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=CreateUploadVideo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateUploadVideo|The operation that you want to perform. Set the value to **CreateUploadVideo**. |
|FileName|String|Yes|D:\\\*\*\*\*.mp4|The name of the video file that you want to upload.

 -   The name must contain a file name extension, which is not case-sensitive.
-   For more information about the supported file name extensions, see [Overview](~~55396~~). |
|Title|String|Yes|UploadTest|The title of the video.

 -   The title can be up to 128 characters in length.
-   The value must be encoded in UTF-8. |
|CoverURL|String|No|https://\*\*\*\*\*test.cn/image/D22F553\*\*\*\*\*TEST.jpeg|The URL of the custom video thumbnail. |
|Description|String|No|UploadTest|The description of the video.

 -   The description can be up to 1,024 characters in length.
-   The value must be encoded in UTF-8. |
|FileSize|Long|No|123|The size of the video. Unit: byte. |
|CateId|Long|No|6771111|The category ID of the video.

 Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Categories**. On the Categories page, you can view the category IDs or modify categories. |
|Tags|String|No|tag1,tag2|The tag of the video.

 -   A maximum of 16 tags can be specified.
-   Separate multiple tags with commas \(,\).
-   Each tag can be up to 32 characters in length.
-   The value must be encoded in UTF-8. |
|UserData|String|No|\{"MessageCallback":\{"CallbackURL":"http://test.test.com"\},"Extend":\{"localId":"\*\*\*\*\*","test":"www"\}\}|The custom configurations, including callback configurations and upload acceleration configurations. The value is a JSON string. For more information, see the "UserData" section of the [Request parameters](~~86952~~) topic.

 **Note:**

-   The callback configurations take effect only when you specify the HTTP callback URL and select the specific callback events in the ApsaraVideo VOD console.
-   To use the upload acceleration feature, submit a [ticket](https://ticket-intl.console.aliyun.com/#/ticket/createIndex). For more information, see [Upload instructions](~~55396~~). |
|TemplateGroupId|String|No|405477f9e21\*\*\*\*\*d19ea2c7c854|The ID of the transcoding template group.

 **Note:** If this parameter is set to a specific value, the specified template group is used for transcoding. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.16.6948257eaZ4m54#/settings/transcode/list). In the left-side navigation pane, choose **Configuration Management** \> **Media Processing** \> **Transcode**. On the Transcode page, you can view the IDs of transcoding template groups. |
|WorkflowId|String|No|405477f9e21\*\*\*\*\*d19ea2c7c854|The ID of the workflow.

 **Note:** If both the WorkflowId and TemplateGroupId parameters are set, the value of the WorkflowId parameter takes a higher priority. For more information, see [Workflows](~~115347~~). |
|StorageLocation|String|No|out-\*\*\*\*.oss-cn-shanghai.aliyuncs.com|The storage location.

 If this parameter is set to a specific value, the video is uploaded to the specified storage location. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Storage**. On the Storage page, you can view the storage locations. |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |

**Note:**

-   If you use the No Transcoding template group to upload videos, only the videos in the format of MP4, FLV, MP3, or M3U8 can be played. Videos in the other formats are supported only for storage. You can know the video format based on the file name extension in the value of the FileName parameter. If you want to use ApsaraVideo Player, make sure that the version is V3.1.0 or later.
-   If the No Transcoding template group is used, only the [FileUploadComplete](~~55630~~) but not the [TranscodeComplete](~~55636~~) event notification is returned after the video is uploaded.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|VideoId|String|93ab850b4f6f\*\*\*\*\*54b6e91d24d81d4|The ID of the video. |
|UploadAddress|String|eyJTZWN1cml0\*\*\*\*\*a2VuIjoiQ0FJU3p3TjF|The upload URL. |
|UploadAuth|String|eyJFbmRw\*\*\*\*\*b2ludCI6Im|The upload credential. |

**Note:**

-   This operation does not upload videos. It generates the [upload URL and credential](~~55397~~) that are required when you upload a video. Then, you can decode the URL and credential by using the [Base64 algorithm](~~55397~~), and use Object Storage Service \(OSS\) SDKs to upload the video to a specified bucket. For more information, see [Upload videos by using the OSS native SDK](~~61388~~).
-   If the video upload credential expires after 3,000 seconds, you can call the [RefreshUploadVideo](~~55408~~) operation to obtain a new upload credential.

## Examples

Sample requests

```
https://vod.aliyuncs.com]/?Action=CreateUploadVideo
&FileName=D:\****.mp4
&Title=UploadTest
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateUploadVideoResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
      <VideoId>93ab850b4f6f*****54b6e91d24d81d4</VideoId>
      <UploadAddress>eyJTZWN1cml0*****a2VuIjoiQ0FJU3p3TjF</UploadAddress>
      <UploadAuth>eyJFbmRw*****b2ludCI6Im</UploadAuth>
</CreateUploadVideoResponse>
```

`JSON` format

```
{
     "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
     "VideoId": "93ab850b4f6f*****54b6e91d24d81d4",
     "UploadAddress": "eyJTZWN1cml0*****a2VuIjoiQ0FJU3p3TjF",
     "UploadAuth": "eyJFbmRw*****b2ludCI6Im"    
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
|InvalidFileName.Extension

|The specified FileName's extension is illegal.

|400

|The error message returned because the file name extension in the value of the FileName parameter is invalid. For more information about file name extensions supported by ApsaraVideo VOD, see [Overview](~~55396~~). |
|IllegalCharacters

|The specified $Parameter contains illegal emoticon or special characters.

|400

|The error message returned because the value of a request parameter such as Title, Description, or Tags contains emoticons. |
|LengthExceededMax

|The specified $Parameter length has exceeded $MaxLength bytes.

|400

|The error message returned because the value length of a request parameter such as Title, Description, or Tags exceeds the upper limit. For more information about the length limit of parameter values, see the description of the request parameters in this topic. |
|TagsExceededMax

|The specified Tags count has exceeded 16.

|400

|The error message returned because more than 16 tags were specified for the video. |
|InvalidTemplateGroupId.NotFound

|The TemplateGroupId does not exist.

|404

|The error message returned because the specified template group ID does not exist. |
|InvalidStorage.NotFound

|The StorageLocation does not exist.

|404

|The error message returned because the specified storage location does not exist. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). Choose **Configuration Management** \> **Media Management** \> **Storage**. On the Storage page, check whether the storage location exists. |
|Forbidden.InitFailed

|Initialization of your account has failed while opening service.

|403

|The error message returned because your account failed to be initialized when the service was activated. |
|AddVideoFailed

|Adding video has failed due to some unknown error.

|503

|The error message returned because the video ID failed to be generated. Try again later. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

