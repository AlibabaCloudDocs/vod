# GetVideoList

Queries the information about videos based on query conditions.

**Note:** In a single request, you can obtain the information about a maximum of first **5,000** video records that meet the specified filter criteria, such as the video status and category. We recommend that you set the StartTime and EndTime parameters to narrow down the time range for queries and perform multiple queries. For more information about how to query the information about more videos or even all videos, see [SearchMedia](~~86044~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetVideoList&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetVideoList|The operation that you want to perform. Set the value to **GetVideoList**. |
|CateId|Long|No|7249287|The ID of the video category. |
|Status|String|No|Uploading,Normal|The status of the video. By default, you can obtain videos in all states. Separate multiple states with commas \(,\). Valid values:

 -   **Uploading**: The video is being uploaded.
-   **UploadFail**: The video fails to be uploaded.
-   **UploadSucc**: The video is uploaded.
-   **Transcoding**: The video is being transcoded.
-   **TranscodeFail**: The video fails to be transcoded.
-   **Blocked**: The video is blocked.
-   **Normal**: The video can be played. |
|PageNo|Integer|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Integer|No|10|Optional. The number of entries to return on each page. Default value: **10**. Maximum value: **100**. |
|SortBy|String|No|CreationTime:Asc|The method for sorting the results. Valid values:

 -   **CreationTime:Desc** \(default\): The results are sorted in reverse chronological order based on the creation time.
-   **CreationTime:Asc**: The results are sorted in chronological order based on the creation time. |
|StartTime|String|No|2017-01-11T12:00:00Z|The beginning of the time range for querying videos based on their creation time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|EndTime|String|No|2017-01-11T12:59:00Z|The end of the time range for querying videos based on their creation time. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|StorageLocation|String|No|out-\*\*\*\*.oss-cn-shanghai.aliyuncs.com|The Object Storage Service \(OSS\) bucket where the video file is stored. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|Total|Integer|100|The total number of videos. |
|VideoList|Array of Video| |The information about the video. The information about a maximum of first 5,000 video records can be obtained in a single request. |
|Video| | | |
|AppId|String|app-1000000|The ID of the application. Default value: **app-1000000**. |
|CateId|Long|78|The ID of the video category. |
|CateName|String|Category name|The name of the video category. |
|CoverURL|String|https://image.example.com/\*\*\*\*.jpg|The URL of the video thumbnail. |
|CreationTime|String|2017-11-14T09:15:50Z|The time when the video file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Video description in ApsaraVideo VOD|The description of the video. |
|Duration|Float|135.6|The duration of the video. Unit: seconds. |
|ModificationTime|String|2017-11-14T09:16:50Z|The time when the video file was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Size|Long|10897890|The size of the video mezzanine file. Unit: byte. |
|Snapshots|List|\["http://image.example.com/snapshot/\*\*\*\*.jpg? auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/\*\*\*\*.jpg?auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52"\]|The URL array of video snapshots. |
|Status|String|Normal|The status of the video. By default, videos in all states are returned. Multiple states are separated by commas \(,\). Valid values:

 -   **Uploading**: The video is being uploaded.
-   **UploadFail**: The video fails to be uploaded.
-   **UploadSucc**: The video is uploaded.
-   **Transcoding**: The video is being transcoded.
-   **TranscodeFail**: The video fails to be transcoded.
-   **Blocked**: The video is blocked.
-   **Normal**: The video can be played. |
|StorageLocation|String|out-\*\*\*\*.oss-cn-shanghai.aliyuncs.com|The OSS bucket where the video file is stored. |
|Tags|String|Tag 1,Tag 2|The tags of the video. Multiple tags are separated by commas \(,\). |
|Title|String|Video title in ApsaraVideo VOD|The title of the video. |
|VideoId|String|9ae2af636ca6\*\*\*\*\*c10412f44891fc|The ID of the video. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetVideoList
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetVideoListResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <Total>100</Total>
  <VideoList>
        <Video>
              <Status>Normal</Status>
              <Description>Video description in ApsaraVideo VOD</Description>
              <VideoId>9ae2af636ca6*****c10412f44891fc</VideoId>
              <Size>10897890</Size>
              <Title>Video title in ApsaraVideo VOD</Title>
              <ModificationTime>2017-11-14T09:16:50Z</ModificationTime>
              <Duration>135.6</Duration>
              <CateName>Category name</CateName>
              <CateId>78</CateId>
              <AppId>app-1000000</AppId>
              <CreationTime>2017-11-14T09:15:50Z</CreationTime>
              <CoverURL>https://image.example.com/****.jpg</CoverURL>
              <StorageLocation>out-****.oss-cn-shanghai.aliyuncs.com</StorageLocation>
              <Tags>Tag 1,Tag 2</Tags>
        </Video>
        <Video>
              <Snapshots>
                    <Snapshot>["http://image.example.com/snapshot/****.jpg? auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/****.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52"]</Snapshot>
              </Snapshots>
        </Video>
  </VideoList>
</GetVideoListResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "Total": "100",
    "VideoList": {
        "Video": [{
            "Status": "Normal",
            "Description": "Video description in ApsaraVideo VOD",
            "VideoId": "9ae2af636ca6*****c10412f44891fc",
            "Size": "10897890",
            "Title": "Video title in ApsaraVideo VOD",
            "ModificationTime": "2017-11-14T09:16:50Z",
            "Duration": "135.6",
            "CateName": "Category name",
            "CateId": "78",
            "AppId": "app-1000000",
            "CreationTime": "2017-11-14T09:15:50Z",
            "CoverURL": "https://image.example.com/****.jpg",
            "StorageLocation": "out-****.oss-cn-shanghai.aliyuncs.com",
            "Tags": "Tag 1,Tag 2",
        }, {
            "Snapshots": {
                "Snapshot": "[\"http://image.example.com/snapshot/****.jpg? auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52\",\"http://image.example.com/snapshot/****.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52\"]"
            }
        }]
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
|VideoListExceededMax

|The video list exceeded maximum.

|400

|The error message returned because the total number of query results exceeds the upper limit. |
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

