# UploadMediaByURL

Uploads multiple media files based on the URLs of mezzanine files to ApsaraVideo VOD at a time.

After the media files are uploaded, you can receive an UploadByURLComplete event notification. For more information, see [UploadByURLComplete](~~86326~~).

You can query the upload status by calling the GetURLUploadInfos operation. For more information, see [GetURLUploadInfos](~~106830~~).

**Note:**

-   After an upload job is submitted, the job is asynchronously executed on the cloud. All submitted upload jobs are queued for execution. You can check the job status based on the URL and video ID returned in the event notification.
-   The UploadMediaByURL operation is suitable for scenarios where you relocate a site with no specific timeliness requirement. Videos are usually uploaded within several hours or days after the jobs are submitted. If you need to upload videos in real time, we recommend that you use server upload SDKs to upload videos on your on-premises device in real time. For more information, see [SDK download](~~51992~~).
-   The UploadMediaByURL operation is available only in the **China \(Shanghai\)** region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=UploadMediaByURL&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UploadMediaByURL|The operation that you want to perform. Set the value to **UploadMediaByURL**. |
|UploadURLs|String|Yes|https://\*\*\*\*.mp4|The URL of the video mezzanine file.

 -   The URL must contain a file name extension, for example, mp4 in `https://****.mp4`.
    -   If the URL does not contain a file name extension, you can enter one by setting the nested parameter FileExtension under the UploadMetadatas parameter.
    -   If the URL contains a file name extension and the FileExtension parameter is set, the value of the FileExtension parameter is used.
    -   For more information about the supported file name extensions, see [Overview](~~55396~~).
-   URL encoding is required. Separate multiple URLs with commas \(,\). You can enter a maximum of 20 URLs.
-   Special characters may cause video upload failures. Therefore, encode URLs before you separate them with commas \(,\). |
|TemplateGroupId|String|No|ca3a8f6e49\*\*\*\*\*57b65806709586|The ID of the transcoding template group.

 -   Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.16.6948257eaZ4m54#/settings/transcode/list). In the left-side navigation pane, choose **Configuration Management** \> **Media Processing** \> **Transcode**. On the Transcode page, you can view the ID of the template group.
-   If this parameter is set to a specific value, the specified template group is used for transcoding.
-   You can also set the nested parameter TemplateGroupId under the UploadMetadatas parameter. |
|StorageLocation|String|No|outin-bfefbb90a47c\*\*\*\*\*\*163e1c7426.oss-cn-shanghai.aliyuncs.com|The storage location of the video.

 Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Storage**. On the Storage page, you can view the storage location. If you do not specify the storage location, the default bucket is used. |
|UploadMetadatas|String|No|\{"SourceURL":"http://test.com/a.mp4","Title":"urlUploadTest"\}|The metadata of the videos to be uploaded. The value is a JSON string.

 -   This parameter takes effect only when the value of the nested parameter SourceURL matches the URL specified by the UploadURLs parameter.
-   The JSON-formatted data, for example, `[UploadMetadata, UploadMetadata,…]`, must be converted into a JSON string.
-   For more information, see the **"UploadMetadata"** section. |
|UserData|String|No|\{"MessageCallback":\{"CallbackURL":"http://test.test.com"\},"Extend":\{"localId":"xxx","test":"www"\}\}|The custom configurations, including callback configurations and upload acceleration configurations. The value is a JSON string. For more information, see the "UserData" section of the [Request parameters](~~86952#UserData~~) topic.

 **Note:**

-   The callback configurations take effect only when you specify the HTTP callback URL and select the specific callback events in the ApsaraVideo VOD console.
-   To use the upload acceleration feature, submit a [ticket](https://ticket-intl.console.aliyun.com/#/ticket/createIndex). For more information, see [Upload instructions](~~55396~~). |
|AppId|String|No|app-\*\*\*\*|The ID of the application. Default value: **app-1000000**. For more information, see [Overview](~~113600~~). |
|WorkflowId|String|No|e1e243b4254\*\*\*\*\*8248197d6f74f9|The ID of the workflow.

 **Note:** If both the WorkflowId and TemplateGroupId parameters are set, the value of the WorkflowId parameter takes effect. For more information, see [Workflows](~~115347~~). |

## UploadMetadata

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|SourceURL

|String

|Yes

|The URL of the video mezzanine file to be uploaded. |
|Title

|String

|Yes

|The title of the video. The title can be up to 128 bytes in length. The value must be encoded in UTF-8. |
|FileSize

|String

|No

|The size of the file. |
|Description

|String

|No

|The description of the video. The description can be up to 1,024 bytes in length. The value must be encoded in UTF-8. |
|CoverURL

|String

|No

|The URL of the custom video thumbnail. |
|CateId

|String

|No

|The category ID of the video. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.15.6948257eaZ4m54#/vod/settings/censored). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Categories**. On the Categories page, you can view the category IDs or modify categories. |
|Tags

|String

|No

|The tag of the video. Each tag can be up to 32 bytes in length. A maximum of 16 tags can be specified. Separate multiple tags with commas \(,\). The value must be encoded in UTF-8. |
|TemplateGroupId

|String

|No

|The ID of the transcoding template group. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.16.6948257eaZ4m54#/settings/transcode/list). In the left-side navigation pane, choose **Configuration Management** \> **Media Processing** \> **Transcode**. On the Transcode page, you can view the ID of the template group. If this parameter is set to a specific value, the specified template group is used for transcoding. If both the request parameter TemplateGroupId and the nested parameter TemplateGroupId are set, the value of the nested parameter takes effect. |
|WorkflowId

|String

|No

|The ID of the workflow. If both the WorkflowId and TemplateGroupId parameters are set, the value of the WorkflowId parameter takes effect. For more information, see [Workflows](~~115347~~). |
|FileExtension

|String

|No

|The file name extension of the video. For more information about the supported file name extensions, see [Overview](~~55396~~). |

**Note:**

-   Nested parameters such as Title, Description, and Tags under the UploadMetadata parameter cannot contain emoticons.
-   If you use the **No Transcoding** template group to upload videos, only the videos in the format of MP4, FLV, MP3, or M3U8 can be played. If you want to use ApsaraVideo Player, the version must be 3.1.0 or later.
-   If the No Transcoding template group is used, only the [FileUploadComplete](~~55630~~) but not the [TranscodeComplete](~~55636~~) event notification is returned after the video is uploaded.
-   In addition to the FileUploadComplete and TranscodeComplete event notifications, ApsaraVideo VOD sends an [UploadByURLComplete](~~86326~~) event notification after the video is uploaded.
-   If you specify multiple media files at a time, ApsaraVideo VOD sends event notifications for each media file after the media file is uploaded.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|UploadJobs|Array of UploadJob| |The information about the upload jobs. |
|JobId|String|ad90a501b1b94\*\*\*\*\*fb72374ad005046|The ID of the upload job. |
|SourceURL|String|http://\*\*\*\*.mp4|The URL of the mezzanine file uploaded by the upload job. |

**Note:**

-   This operation is used to asynchronously upload videos. Upload jobs are queued for execution after they are submitted. The completion time of an upload job varies based on the number of jobs in the queue.

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=UploadMediaByURL
&UploadURLs=https://****.mp4
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UploadMediaByURLResponse>
	  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <UploadJobs>
		    <JobId>ad90a501b1b94*****fb72374ad005046</JobId>
		    <SourceURL>http://****.mp4</SourceURL>
	  </UploadJobs>
</UploadMediaByURLResponse>
```

`JSON` format

```
{
    "RequestId":"25818875-5F78-4A*****F6-D7393642CA58",
    "UploadJobs":[
        {
            "SourceURL":"http://****.mp4",
            "JobId":"ad90a501b1b94*****fb72374ad005046"
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
|InvalidParameter.UploadURLs

|The specified parameter UploadURLs is not valid.

|400

|The error message returned because the UploadURLs parameter is invalid. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

