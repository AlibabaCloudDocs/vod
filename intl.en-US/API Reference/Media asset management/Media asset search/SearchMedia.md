# SearchMedia

Queries the information about media assets such as videos, audio, images, and auxiliary media assets.

## Limits on the maximum number of data records that can be queried by using different methods

-   Method 1: To traverse all the first 5,000 data records that meet the specified filter criteria, you must set the PageNo and PageSize parameters to traverse data by page. If the number of data records that meet the specified filter criteria exceeds 5,000, use Method 2 to traverse all data.
-   Method 2: You can use this method to traverse only the data of video and audio files. To traverse all the data records that meet the specified filter criteria, you must set the PageNo, PageSize, and ScrollToken parameters to traverse data by page. The total number of data records from the current page to the desired page cannot exceed 1,200. Assume that the PageSize parameter is set to **20**.
    -   When the PageNo parameter is set to **1**, you can page down to traverse data records from page 1 to page **60** at most.
    -   When the PageNo parameter is set to **2**, you can page down to traverse data records from page 2 to page **61** at most.
    -   When the PageNo parameter is set to **61**, you can page up to traverse data records from page 61 to page **2** at most or page down to traverse data records from page 61 to page **120** at most.

## Debugging

[For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SearchMedia&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchMedia|The operation that you want to perform. Set the value to **SearchMedia**. |
|SearchType|String|No|video|The type of media asset that you want to query. Valid values:

 -   **video** \(default\): video
-   **audio**: audio
-   **image**: image
-   **attached**: auxiliary media asset |
|Fields|String|No|Title,CoverURL|The media asset fields that are returned in the query results.

 By default, only the basic media asset fields are returned. You can specify additional media asset fields that need to be returned in the request. For more information, see [Usage](~~99179~~). |
|Match|String|No|field = value|The filter criteria. For more information about the syntax, see [Media asset search protocol](~~86991~~). |
|SortBy|String|No|CreationTime:Desc|The sort field and order. Separate multiple sort fields with commas \(,\). Valid values:

 -   **CreationTime:Desc** \(default\): The results are sorted in reverse chronological order based on the creation time.
-   **CreationTime:Asc**: The results are sorted in chronological order based on the creation time.

 **Note:**

-   For more information about the sort field, see [Sort field](~~99179~~).
-   To obtain the first 5,000 data records that meet the specified filter criteria, you can specify a maximum of three sort fields.
-   To obtain all the data records that meet the specified filter criteria, you can specify only one sort field. |
|PageNo|Integer|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Integer|No|10|The number of entries to return on each page. Default value: **10**. Maximum value: **100**. |
|ScrollToken|String|No|vfdvbf454|The pagination identifier.

 **Note:** This parameter only takes effect when you query the data of video and audio files. The value is a string of 32 characters. You must set this parameter to traverse all data. The first query request does not contain this parameter. The value of this parameter is returned each time data records that meet the specified filter criteria are found. The value is used to record the current position of queried data. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MediaList|Array of Media| |The information about the media asset. |
|AttachedMedia|Struct| |The information about the auxiliary media asset. For more information, see [AttachedMedia](~~86991~~). |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|BusinessType|String|watermark|The type of business. Valid values:

 -   **watermark**
-   **subtitle**
-   **material** |
|Categories|Array of Category| |The list of category IDs. |
|CateId|Long|10027394|The ID of the category. |
|CateName|String|Test|The name of the category. |
|Level|Long|1|The level of the category. |
|ParentId|Long|-1|The ID of the parent category. |
|CreationTime|String|2018-07-19T03:45:25Z|The time when the auxiliary media asset file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Test|The description of the auxiliary media asset. |
|MediaId|String|a82a2cd7d4e147b\*\*\*\*\*a0ed6c1ee372|The ID of the auxiliary media asset. |
|ModificationTime|String|2018-07-19T03:48:25Z|The time when the auxiliary media asset file was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Status|String|Normal|The status of the auxiliary media asset. Valid values:

 -   **Uploading**: The auxiliary media asset is being uploaded. This is the initial status.
-   **Normal**: The auxiliary media asset is uploaded.
-   **UploadFail**: The auxiliary media asset fails to be uploaded. |
|StorageLocation|String|outin-bfefbb90a47c11\*\*\*\*\*7426.oss-cn-shanghai.aliyuncs.com|The Object Storage Service \(OSS\) bucket where the auxiliary media asset is stored. |
|Tags|String|Test|The tag of the auxiliary media asset. |
|Title|String|Test|The title of the auxiliary media asset. |
|URL|String|https://examp.com/\*\*\*\*.png|The URL of the auxiliary media asset. |
|Audio|Struct| |The information about the audio. For more information, see [Audio](~~86991~~). |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|AudioId|String|a82a2cd7d4e147bb\*\*\*\*\*ed6c1ee372|The ID of the audio. |
|CateId|Long|10000123|The ID of the category. |
|CateName|String|ceshi|The name of the category. |
|CoverURL|String|http://example.com/atest\*\*\*\*.jpg|The URL of the thumbnail. |
|CreationTime|String|2018-07-19T03:45:25Z|The time when the audio file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|The description of the audio.|The description of the audio. |
|DownloadSwitch|String|on|The download switch. The audio can be downloaded offline only when the download switch is turned on. Valid values:

 -   **on** \(default\): The audio can be downloaded offline.
-   **off**: The audio cannot be downloaded offline. |
|Duration|Float|123|The duration of the audio. |
|MediaSource|String|general|The audio source. Valid values:

 -   **general**: The audio is uploaded by using ApsaraVideo VOD.
-   **short\_video**: The audio is uploaded to ApsaraVideo VOD by using the short video SDK. For more information, see Short video SDK.
-   **editing**: The audio is uploaded to ApsaraVideo VOD after online editing and production. For more information, see Video production.
-   **live**: The audio live streams are recorded and uploaded to ApsaraVideo VOD. |
|ModificationTime|String|2018-07-19T03:48:25Z|The time when the audio file was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|PreprocessStatus|String|UnPreprocess|The preprocessing status. Only preprocessed videos can be used for live streaming in the production studio. Valid values:

 -   **UnPreprocess**: No preprocessing is performed.
-   **Preprocessing**: Preprocessing is being performed.
-   **PreprocessSucceed**: Preprocessing is complete.
-   **PreprocessFailed**: Preprocessing fails. |
|Size|Long|123|The size of the audio. |
|Snapshots|List|\{"http://sample.aliyun.com/cover02.jpg"\}|The list of automatic snapshots. |
|SpriteSnapshots|List|\{"http://sample.aliyun.com/cover02.jpg"\}|The list of sprite snapshots. |
|Status|String|Normal|The status of the audio. Valid values:

 -   **Uploading**: The audio is being uploaded.
-   **Normal**: The audio is uploaded.
-   **UploadFail**: The audio fails to be uploaded.
-   **Delete**: The audio is deleted. |
|StorageLocation|String|outin-aaa\*\*\*\*\*aa.oss-cn-shanghai.aliyuncs.com|The OSS bucket where the audio is stored. |
|Tags|String|tag1,tag2|The tags of the audio. |
|Title|String|Audio|The title of the audio. |
|TranscodeMode|String|FastTranscode|The transcoding mode. Valid values:

 -   **FastTranscode** \(default\): The audio is immediately transcoded after it is uploaded. You cannot play the audio before it is transcoded.
-   **NoTranscode**: The audio can be played without being transcoded. You can immediately play the audio after it is uploaded.
-   **AsyncTranscode**: The audio can be immediately played and asynchronously transcoded after it is uploaded. |
|CreationTime|String|2018-07-19T03:45:25Z|The time when the audio file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Image|Struct| |The information about the image. For more information, see [Image](~~86991~~). |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|CateId|Long|1000123|The ID of the category. |
|CateName|String|Beautification image 1|The name of the category. |
|CreationTime|String|2018-07-19T03:45:25Z|The time when the image file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Image test|The description of the image. |
|ImageId|String|11130843741\*\*\*\*\*se99wqmoes|The ID of the image. |
|ModificationTime|String|2018-07-19T03:48:25Z|The time when the image file was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Status|String|Uploading|The status of the image.

 -   **Uploading**: The image is being uploaded. This is the initial status.
-   **Normal**: The image is uploaded.
-   **UploadFail**: The image fails to be uploaded. |
|StorageLocation|String|outin-bfefbb90a47c\*\*\*\*\*\*163e1c7426.oss-cn-shanghai.aliyuncs.com|The OSS bucket where the image is stored. |
|Tags|String|tag1|The tag of the image. |
|Title|String|image1|The title of the image. |
|URL|String|https://examle.com/\*\*\*\*.png|The URL of the image. |
|MediaId|String|a82a2cd7d4e147bb\*\*\*\*\*ed6c1ee372|The ID of the media. |
|MediaType|String|video|The type of the media. Valid values:

 -   **video**: video
-   **audio**: audio
-   **image**: image
-   **attached**: auxiliary media asset |
|Video|Struct| |The information about the video. For more information, see [Video](~~86991~~). |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|CateId|Long|10000123|The ID of the category. |
|CateName|String|video1|The name of the category. |
|CoverURL|String|https://aaa.com/a.png|The URL of the thumbnail. |
|CreationTime|String|2018-07-19T03:45:25Z|The time when the video file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Video test|The description of the video. |
|DownloadSwitch|String|on|The download switch. The video can be downloaded offline only when the download switch is turned on. Valid values:

 -   **on** \(default\): The video can be downloaded offline.
-   **off**: The video cannot be downloaded offline. |
|Duration|Float|123|The duration of the video. Unit: seconds. |
|MediaSource|String|general|The video source. Valid values:

 -   **general**: The video is uploaded by using ApsaraVideo VOD.
-   **short\_video**: The video is uploaded by using the short video SDK.
-   **editing**: The video is produced after online editing.
-   **live**: The video live streams are recorded and uploaded. |
|ModificationTime|String|2018-07-19T03:48:25Z|The time when the video file was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|PreprocessStatus|String|Preprocessing|The preprocessing status. Valid values:

 -   **UnPreprocess**: No preprocessing is performed.
-   **Preprocessing**: Preprocessing is being performed.
-   **PreprocessSucceed**: Preprocessing is complete.
-   **PreprocessFailed**: Preprocessing fails. |
|Size|Long|123|The size of the video. |
|Snapshots|List|\{"http://sample.aliyun.com/cover02.jpg"\}|The list of automatic snapshots. |
|SpriteSnapshots|List|\{"http://sample.aliyun.com/cover02.jpg"\}|The list of sprite snapshots. |
|Status|String|UploadSucc|The status of the video. Valid values:

 -   **Uploading**: The video is being uploaded.
-   **UploadFail**: The video fails to be uploaded.
-   **UploadSucc**: The video is uploaded.
-   **Transcoding**: The video is being transcoded.
-   **TranscodeFail**: The video fails to be transcoded.
-   **Blocked**: The video is blocked.
-   **Normal**: The video can be played. |
|StorageLocation|String|outin-bfefbb90a47c\*\*\*\*\*\*163e1c7426.oss-cn-shanghai.aliyuncs.com|The OSS bucket where the video is stored. |
|Tags|String|tag1|The tag of the video. |
|Title|String|ceshi|The title of the video. |
|TranscodeMode|String|FastTranscode|The transcoding mode. Valid values:

 -   **FastTranscode** \(default\): The video is immediately transcoded after it is uploaded. You cannot play the video before it is transcoded.
-   **NoTranscode**: The video can be played without being transcoded. You can immediately play the video after it is uploaded.
-   **AsyncTranscode**: The video can be immediately played and asynchronously transcoded after it is uploaded. |
|VideoId|String|a82a2asdasqadaf3\*\*\*\*\*faa0ed6c1ee372|The ID of the video. |
|RequestId|String|3E0CEF83-FB09-4E\*\*\*\*\*34-BA1451814B03|The ID of the request. |
|ScrollToken|String|24e0fba7188fa\*\*\*\*\*e707e146esa54|The pagination identifier. |
|Total|Long|10|The total number of data records that meet the specified filter criteria. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SearchMedia
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchMediaResponse>
      <MediaList>
            <CreationTime>2018-07-20T04:29:04Z</CreationTime>
            <MediaType>video</MediaType>
            <MediaId>afab53f582cf422f8*****1cf0425815</MediaId>
            <Video>
                  <CoverURL>http://sample.aliyun.com/cover01.jpg</CoverURL>
                  <CreationTime>2018-07-20T04:29:04Z</CreationTime>
                  <Status>Normal</Status>
                  <ModificationTime>2018-07-20T06:14:29Z</ModificationTime>
                  <VideoId>afab53f582cf422f8*****1cf0425815</VideoId>
                  <Title>Test title 01</Title>
            </Video>
      </MediaList>
      <MediaList>
            <CreationTime>2018-07-19T03:45:25Z</CreationTime>
            <MediaType>video</MediaType>
            <MediaId>a82a2cd7d4e147b*****ed6c1ee372</MediaId>
            <Video>
                  <CoverURL>http://sample.aliyun.com/cover02.jpg</CoverURL>
                  <CreationTime>2018-07-19T03:45:25Z</CreationTime>
                  <Status>Normal</Status>
                  <ModificationTime>2018-07-20T06:45:53Z</ModificationTime>
                  <VideoId>a82a2cd7d4e147b*****ed6c1ee372</VideoId>
                  <Title>Test title 02</Title>
            </Video>
      </MediaList>
      <MediaList>
            <CreationTime>2018-07-05T02:43:55Z</CreationTime>
            <MediaType>video</MediaType>
            <MediaId>62da1c9832e4*****4dce0eac3d2a</MediaId>
            <Video>
                  <CoverURL>http://sample.aliyun.com/cover03.jpg</CoverURL>
                  <CreationTime>2018-07-05T02:43:55Z</CreationTime>
                  <Status>Normal</Status>
                  <ModificationTime>2018-07-05T05:41:29Z</ModificationTime>
                  <VideoId>62da1c9832e4*****4dce0eac3d2a</VideoId>
                  <Title>Test title 03</Title>
            </Video>
      </MediaList>
      <RequestId>3E0CEF83-FB09-4E*****34-BA1451814B03</RequestId>
      <ScrollToken>24e0fba7188*****e707e146esa54</ScrollToken>
      <Total>10</Total>
</SearchMediaResponse>
```

`JSON` format

```
{
    "MediaList": [{
        "CreationTime": "2018-07-20T04:29:04Z",
        "MediaType": "video",
        "MediaId": "afab53f582cf422f8*****1cf0425815",
        "Video": {
            "CoverURL": "http://sample.aliyun.com/cover01.jpg",
            "CreationTime": "2018-07-20T04:29:04Z",
            "Status": "Normal",
            "ModificationTime": "2018-07-20T06:14:29Z",
            "VideoId": "afab53f582cf422f8*****1cf0425815",
            "Title": "Test title 01"
        }
    },
    {
        "CreationTime": "2018-07-19T03:45:25Z",
        "MediaType": "video",
        "MediaId": "a82a2cd7d4e147b*****ed6c1ee372",
        "Video":{
            "CoverURL": "http://sample.aliyun.com/cover02.jpg",
            "CreationTime": "2018-07-19T03:45:25Z",
            "Status": "Normal",
            "ModificationTime": "2018-07-20T06:45:53Z",
            "VideoId": "a82a2cd7d4e147b*****ed6c1ee372",
            "Title": "Test title 02"
        }
    },
    {
        "CreationTime": "2018-07-05T02:43:55Z",
        "MediaType": "video",
        "MediaId": "62da1c9832e4*****4dce0eac3d2a",
        "Video": {
            "CoverURL": "http://sample.aliyun.com/cover03.jpg",
            "CreationTime": "2018-07-05T02:43:55Z",
            "Status": "Normal",
            "ModificationTime": "2018-07-05T05:41:29Z",
            "VideoId": "62da1c9832e4*****4dce0eac3d2a",
            "Title": "Test title 03"
        }
    }],
    "RequestId": "3E0CEF83-FB09-4E*****34-BA1451814B03",
    "ScrollToken": "24e0fba7188*****e707e146esa54",
    "Total": 10
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
|SortByExceededMax

|The SortBy parameter only supports one sort field when traversing all data.

|400

|The error message returned because more than one sort field is specified to traverse all data. |
|ErrorMatchSyntax

|The parameter Match.%s has an error syntax, please check it.

|400

|The error message returned because the syntax of the Match parameter is invalid. Check the syntax and try again. |
|InvalidScrollToken.Expired

|The ScrollToken is expired, please refresh it.

|400

|The error message returned because the value of the ScrollToken parameter is invalid. Obtain data again from Page 1. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

