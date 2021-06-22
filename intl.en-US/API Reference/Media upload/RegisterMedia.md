# RegisterMedia

Registers media assets.

You can call this operation to register audio and video files in Object Storage Service \(OSS\) buckets that are used for ApsaraVideo VOD. After a media asset is registered, you can submit a transcoding job or snapshot job based on the media ID. For more information, see [SubmitTranscodeJobs](~~68570~~) and [SubmitSnapshotJob](~~72213~~).

**Note:**

-   You can register a maximum of 10 OSS media files that have the same OSS URL at a time.
-   After a media asset is registered, this operation does not automatically trigger a transcoding job if the transcoding template group ID is not specified. If the transcoding template group ID is specified, the system uses the specified template group to transcode the media asset. This process is different from video upload.
-   If you submit a media file that is registered, this operation returns only the unique media ID that is associated with the media file, without other processing.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=RegisterMedia&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RegisterMedia|The operation that you want to perform. Set the value to **RegisterMedia**. |
|RegisterMetadatas|String|Yes|\[\{"FileURL":"https://bucketName.oss-cn-shanghai.aliyuncs.com/video/test/video.m3u8","Title":"VideoName"\}\]|The metadata of the media asset that you want to register. The value is a JSON string. You can specify the metadata for a maximum of 10 media assets at a time. For more information about the parameter structure, see the RegisterMetadata table. |
|TemplateGroupId|String|No|ca3a8f6e49c8\*\*\*\*\*7b65806709586|The ID of the transcoding template group. You can obtain the ID by calling the [AddTranscodeTemplateGroup](~~102665~~) operation.

 **Note:** If this parameter is specified, the specified template group is used for transcoding. Log on to the [ApsaraVideo VOD](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.20.68924c07zG2sdx#/settings/transcode/list) console. On the **Transcode** page, view the ID of the transcoding template group. |
|UserData|String|No|\{"Extend":\{"localId":"\*\*\*\*","test":"www"\}\}|The custom configurations. The value is a JSON string, which supports the configuration such as callbacks. For more information, see [UserData](~~86952#section_6fg_qll_v3w~~). |
|WorkflowId|String|No|637adc2b7ba\*\*\*\*\*51a83d841606f8|The ID of the workflow. |

## RegisterMetadata

The following table describes the metadata of the media asset that you want to register.

|Parameter

|Type

|Required

|Description |
|-----------|------|----------|-------------|
|FileURL

|String

|Yes

|The OSS URL of the media file. The URL can be up to 1,024 bytes in length. The file name must be globally unique. If a file name is repeatedly registered, the unique media ID that is associated with the file name is returned. |
|Title

|String

|Yes

|The title of the media asset. The title can be up to 128 bytes in length. The value must be encoded in UTF-8. |
|Description

|String

|No

|The description of the media asset. The description can be up to 1,024 bytes in length. The value must be encoded in UTF-8. |
|Tags

|String

|No

|The list of one or more tags of the file system. A tag can be up to 32 bytes in length and a maximum of 16 tags can be specified. Separate multiple tags with commas \(,\). The value must be encoded in UTF-8. |
|CoverURL

|String

|No

|The URL of the thumbnail. The description can be up to 1,024 bytes in length. |
|CateId

|Long

|No

|The ID of the category. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|FailedFileURLs|List|\["http://\*\*\*\*.oss-cn-shanghai.aliyuncs.com/vod\_sample\_03.mp4"\]|The URL list of media files failed to be registered. |
|RegisteredMediaList|Array of RegisteredMedia| |The list of media files that are registered, including newly registered and repeatedly registered media files. |
|FileURL|String|http://\*\*\*\*.oss-cn-shanghai.aliyuncs.com/vod\_sample\_01.mp4|The OSS URL of the media file. |
|MediaId|String|d97af32828084\*\*\*\*\*d1896683b1aa38|The ID of the media file that is registered with ApsaraVideo VOD. If the registered media file is an audio or video file, this parameter corresponds to the VideoId parameter of ApsaraVideo VOD. |
|NewRegister|Boolean|false|Indicates whether the media file is newly registered or repeatedly registered. Valid values:

 -   **true**: indicates that the media file is newly registered.
-   **false**: indicates that the media file is repeatedly registered. |
|RequestId|String|14F43C5C-8033-4\*\*\*\*\*48B-AD04F64E5098|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=RegisterMedia
&RegisterMetadatas={"Title":"ceshi"}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RegisterMediaResponse>
      <RequestId>14F43C5C-8033-43E7-B48B-AD04F64E5098</RequestId>
      <RegisteredMediaList>
            <MediaId>d97af328280842229aed1896683b1aa38</MediaId>
            <FileURL>http://****.oss-cn-shanghai.aliyuncs.com/vod_sample_01.mp4</FileURL>
            <NewRegister>true</NewRegister>
      </RegisteredMediaList>
      <RegisteredMediaList>
            <MediaId>d97af328280842229aed1896683b1aa38</MediaId>
            <FileURL>http://****.oss-cn-shanghai.aliyuncs.com/vod_sample_02.mp4</FileURL>
            <NewRegister>false</NewRegister>
      </RegisteredMediaList>
      <FailedFileURLs>http://****.oss-cn-shanghai.aliyuncs.com/vod_sample_03.mp4</FailedFileURLs>
</RegisterMediaResponse>
```

`JSON` format

```
{
 "RequestId":"14F43C5C-8033-43E7-B48B-AD04F64E5098",
 "RegisteredMediaList": [
      {
     "MediaId":"d97af328280842229aed1896683b1aa38",
     "FileURL":"http://****.oss-cn-shanghai.aliyuncs.com/vod_sample_01.mp4",
     "NewRegister":true
      },
    {
     "MediaId":"d97af328280842229aed1896683b1aa38",
     "FileURL":"http://*****.oss-cn-shanghai.aliyuncs.com/vod_sample_02.mp4",
     "NewRegister":false
      }
  ],
   "FailedFileURLs":[
      "http://****.oss-cn-shanghai.aliyuncs.com/vod_sample_03.mp4"
  ]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

