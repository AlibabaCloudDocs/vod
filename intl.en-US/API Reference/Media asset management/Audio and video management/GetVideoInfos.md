# GetVideoInfos

Queries the information about multiple videos at a time.

**Note:** You can call this operation to obtain the basic information about multiple videos at a time based on video IDs. The basic information includes the title, description, duration, thumbnail URL, status, creation time, size, snapshots, category, and tags of each video.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetVideoInfos&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetVideoInfos|The operation that you want to perform. Set the value to **GetVideoInfos**. |
|VideoIds|String|Yes|7753d144efd\*\*\*\*\*8e649c6c45fe0579,7753d144efd74d\*\*\*\*\*6c45fe0570|The list of video IDs. Separate multiple IDs with commas \(,\). A maximum of 20 IDs can be specified. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NonExistVideoIds|List|\["b4039216985f43\*\*\*\*\*82a4ed2884"\]|The IDs of the videos that do not exist. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|VideoList|Array of Video| |The information about the video. |
|AppId|String|6985f4312a5382a4ed\*\*\*\*|The ID of the application. |
|CateId|Long|78|The ID of the video category. |
|CateName|String|Category name|The name of the video category. |
|CoverURL|String|https://image.example.com/\*\*\*\*.jpg|The URL of the video thumbnail. |
|CreationTime|String|2017-06-26T05:38:48Z|The time when the video file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Video description in ApsaraVideo VOD|The description of the video. |
|Duration|Float|120|The duration of the video. Unit: seconds. |
|ModificationTime|String|2017-06-26T06:38:48Z|The time when the video file was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Size|Long|453|The size of the video mezzanine file. Unit: byte. |
|Snapshots|List|\["http://image.example.com/snapshot/\*\*\*\*.jpg? auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/\*\*\*\*.jpg?auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52",...\]|The URL array of video snapshots. |
|Status|String|Normal|The status of the video. By default, videos in all states are returned. Multiple states are separated by commas \(,\). Valid values:

 -   **Uploading**: The video is being uploaded.
-   **UploadFail**: The video fails to be uploaded.
-   **UploadSucc**: The video is uploaded.
-   **Transcoding**: The video is being transcoded.
-   **TranscodeFail**: The video fails to be transcoded.
-   **Blocked**: The video is blocked.
-   **Normal**: The video can be played. |
|StorageLocation|String|out-\*\*\*\*.oss-cn-shanghai.aliyuncs.com|The Object Storage Service \(OSS\) bucket where the video file is stored. |
|Tags|String|Tag 1,Tag 2|The tags of the video. Multiple tags are separated by commas \(,\). |
|TemplateGroupId|String|b4039216985f4312a5382a4ed\*\*\*\*|The ID of the template group that was used to transcode the video. |
|Title|String|Video title in ApsaraVideo VOD|The title of the video. |
|VideoId|String|93ab850b4f6f44\*\*\*\*\*6e91d24d81d4|The ID of the video. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetVideoInfos
&VideoIds=7753d144efd*****8e649c6c45fe0579,7753d144efd74d*****6c45fe0570
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetVideoInfosResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <NonExistVideoIds>["b4039216985f43*****82a4ed2884"]</NonExistVideoIds>
  <VideoList>
        <Status>Normal</Status>
        <Description>Video description in ApsaraVideo VOD</Description>
        <VideoId>93ab850b4f6f44*****6e91d24d81d4</VideoId>
        <Size>453</Size>
        <DownloadSwitch>on</DownloadSwitch>
        <Title>Video title in ApsaraVideo VOD</Title>
        <ModificationTime>2017-06-26T06:38:48Z</ModificationTime>
        <Duration>120</Duration>
        <CateName>Category name</CateName>
        <CateId>78</CateId>
        <PreprocessStatus>UnPreprocess</PreprocessStatus>
        <AppId>6985f4312a5382a4ed****</AppId>
        <CustomMediaInfo>{"aa":123}</CustomMediaInfo>
        <CreationTime>2017-06-26T05:38:48Z</CreationTime>
        <CoverURL>https://image.example.com/****.jpg</CoverURL>
        <RegionId>cn-shanghai</RegionId>
        <StorageLocation>out-****.oss-cn-shanghai.aliyuncs.com</StorageLocation>
        <Tags>Tag 1,Tag 2</Tags>
        <TemplateGroupId>b4039216985f4312a5382a4ed****</TemplateGroupId>
  </VideoList>
  <VideoList>
        <ThumbnailList>
              <URL>http://test.aliyun.com/7bb18e5afc740939575f1fd694c57e4/covers/webvtt/****.vtt</URL>
        </ThumbnailList>
  </VideoList>
  <VideoList>
        <Snapshots>["http://image.example.com/snapshot/****.jpg? auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/****.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52",...] </Snapshots>
  </VideoList>
</GetVideoInfosResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "NonExistVideoIds": "[\"b4039216985f43*****82a4ed2884\"]",
    "VideoList": [{
        "Status": "Normal",
        "Description": "Video description in ApsaraVideo VOD",
        "VideoId": "93ab850b4f6f44*****6e91d24d81d4",
        "Size": "453",
        "DownloadSwitch": "on",
        "Title": "Video title in ApsaraVideo VOD",
        "ModificationTime": "2017-06-26T06:38:48Z",
        "Duration": "120",
        "CateName": "Category name",
        "CateId": "78",
        "PreprocessStatus": "UnPreprocess",
        "AppId": "6985f4312a5382a4ed****",
        "CustomMediaInfo": "{\"aa\":123}",
        "CreationTime": "2017-06-26T05:38:48Z",
        "CoverURL": "https://image.example.com/****.jpg",
        "RegionId": "cn-shanghai",
        "StorageLocation": "out-****.oss-cn-shanghai.aliyuncs.com",
        "Tags": "Tag 1,Tag 2",
        "TemplateGroupId": "b4039216985f4312a5382a4ed****"
    }, {
        "ThumbnailList": [{
            "URL": "http://test.aliyun.com/7bb18e5afc740939575f1fd694c57e4/covers/webvtt/****.vtt"
        }]
    }, {
        "Snapshots": "[\"http://image.example.com/snapshot/****.jpg? auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52\",\"http://image.example.com/snapshot/****.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52\",...]"
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
|InvalidVideo.NotFound

|The video does not exist.

|404

|The error message returned because the video does not exist. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

