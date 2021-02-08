# GetVideoInfo

Queries the basic information about a video. The basic information includes the title, description, duration, thumbnail URL, status, creation time, size, snapshots, category, and tags of the video.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetVideoInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetVideoInfo|The operation that you want to perform. Set the value to **GetVideoInfo**. |
|VideoId|String|Yes|9b73864d75f1\*\*\*\*\*d231e9001cd5f8|The ID of the video. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|Video|Struct| |The information about the video. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|AuditStatus|String|Normal|The review status of the video. Valid values:

 -   **Normal**: The video is approved.
-   **Blocked**: The video is blocked. |
|CateId|Long|781111|The ID of the video category. |
|CateName|String|Category name|The name of the video category. |
|CoverURL|String|https://image.example.com/\*\*\*\*.jpg|The URL of the video thumbnail. |
|CreationTime|String|2017-11-14T09:15:50Z|The time when the video file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CustomMediaInfo|String|\{"aaa":"test"\}|The information about the custom media asset. |
|Description|String|Video description in ApsaraVideo VOD|The description of the video. |
|Duration|Float|135.6|The duration of the video. Unit: seconds. |
|ModificationTime|String|2017-11-14T10:15:50Z|The time when the video file was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RegionId|String|cn-shanghai|The region ID of the Object Storage Service \(OSS\) bucket. |
|Size|Long|10897890|The size of the video mezzanine file. Unit: byte. |
|Snapshots|List|\["http://image.example.com/snapshot/\*\*\*\*.jpg? auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/\*\*\*\*.jpg?auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52",...\]|The URL array of video snapshots. |
|Status|String|Normal|The status of the video. Valid values:

 -   **Uploading**: The video is being uploaded.
-   **UploadFail**: The video fails to be uploaded.
-   **UploadSucc**: The video is uploaded.
-   **Transcoding**: The video is being transcoded.
-   **TranscodeFail**: The video fails to be transcoded.
-   **Blocked**: The video is blocked.
-   **Normal**: The video can be played. |
|StorageLocation|String|out-201703232251\*\*\*\*.oss-cn-shanghai.aliyuncs.com|The OSS bucket where the video file is stored. |
|Tags|String|Tag 1,Tag 2|The tags of the video. Multiple tags are separated by commas \(,\). |
|TemplateGroupId|String|9ae2af636ca64835b0c10412f44891f2|The ID of the template group. |
|Title|String|Video title in ApsaraVideo VOD|The title of the video. |
|VideoId|String|9b73864d75f1\*\*\*\*\*d231e9001cd5f8|The ID of the video. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetVideoInfo
&VideoId=9b73864d75f1*****d231e9001cd5f8
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetVideoInfoResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <Video>
        <Status>Normal</Status>
        <Description>Video description in ApsaraVideo VOD</Description>
        <VideoId>9b73864d75f1*****d231e9001cd5f8</VideoId>
        <Size>10897890</Size>
        <Title>Video title in ApsaraVideo VOD</Title>
        <ModificationTime>2017-11-14T10:15:50Z</ModificationTime>
        <Duration>135.6</Duration>
        <CateName>Category name</CateName>
        <CateId>781111</CateId>
        <AuditStatus>Normal</AuditStatus>
        <AppId>app-****</AppId>
        <CustomMediaInfo>{"aaa":"test"}</CustomMediaInfo>
        <CreationTime>2017-11-14T09:15:50Z</CreationTime>
        <CoverURL>https://image.example.com/****.jpg</CoverURL>
        <RegionId>cn-shanghai</RegionId>
        <StorageLocation>out-201703232251****.oss-cn-shanghai.aliyuncs.com</StorageLocation>
        <Snapshots>
              <Snapshot>["http://image.example.com/snapshot/****.jpg? auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/****.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52",...] </Snapshot>
        </Snapshots>
        <Tags>Tag 1,Tag 2</Tags>
        <TemplateGroupId>9ae2af636ca64835b0c10412f44891f2</TemplateGroupId>
  </Video>
</GetVideoInfoResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "Video": {
        "Status": "Normal",
        "Description": "Video description in ApsaraVideo VOD",
        "VideoId": "9b73864d75f1*****d231e9001cd5f8",
        "Size": "10897890",
        "Title": "Video title in ApsaraVideo VOD",
        "ModificationTime": "2017-11-14T10:15:50Z",
        "Duration": "135.6",
        "CateName": "Category name",
        "CateId": "781111",
        "AuditStatus": "Normal",
        "AppId": "app-****",
        "CustomMediaInfo": "{\"aaa\":\"test\"}",
        "CreationTime": "2017-11-14T09:15:50Z",
        "CoverURL": "https://image.example.com/****.jpg",
        "RegionId": "cn-shanghai",
        "StorageLocation": "out-201703232251****.oss-cn-shanghai.aliyuncs.com",
        "Snapshots": {
            "Snapshot": "[\"http://image.example.com/snapshot/****.jpg? auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52\",\"http://image.example.com/snapshot/****.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52\",...]"
        },
        "Tags": "Tag 1,Tag 2",
        "TemplateGroupId": "9ae2af636ca64835b0c10412f44891f2"
    }
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

