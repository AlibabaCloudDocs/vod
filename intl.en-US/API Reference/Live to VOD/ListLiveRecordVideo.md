# ListLiveRecordVideo

Queries live-to-VOD videos.

**Note:** You can query a maximum of 5,000 videos based on the specified filter condition.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ListLiveRecordVideo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListLiveRecordVideo|The operation that you want to perform. Set the value to **ListLiveRecordVideo**. |
|StreamName|String|No|live-test|The name of the recorded live stream. |
|DomainName|String|No|example.com|The domain name of the recorded live stream. |
|AppName|String|No|testApp|The name of the application that was used to record the live stream. |
|PageNo|Integer|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: **100**. Default value: **10**. |
|SortBy|String|No|CreationTime:Desc|The sorting rule of results. Valid values:

-   **CreationTime:Desc**: sorts the results based on the creation time in descending order. This is the default value.
-   **CreationTime:Asc**: sorts the results based on the creation time in ascending order. |
|StartTime|String|No|2017-01-11T12:00:00Z|The beginning of the time range to query. The query is performed based on the time range during which the required live streams were recorded. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|EndTime|String|No|2017-01-11T13:00:00Z|The end of the time range to query. The query is performed based on the time range during which the required live streams were recorded. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LiveRecordVideoList|Array of LiveRecordVideo| |The list of videos. |
|LiveRecordVideo| | | |
|AppName|String|testApp|The name of the application. |
|DomainName|String|example.com|The domain name. |
|PlaylistId|String|\*\*\*\*|The ID of the playlist. |
|RecordEndTime|String|2017-12-08T08:44:56Z|The end of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|RecordStartTime|String|2017-12-08T07:40:56Z|The beginning of the time range in which data was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|StreamName|String|live-test|The name of the live stream. |
|Video|Struct| |The information about the video. |
|CateId|Integer|78|The ID of the video category. |
|CateName|String|Category name|The name of the video category. |
|CoverURL|String|https://image.example.com/coversample.jpg|The thumbnail URL of the video. |
|CreationTime|String|2017-12-08T07:40:56Z|The time when the video was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Description|String|Description of the ApsaraVideo VOD video|The description of the video. |
|Duration|Float|135.6|The duration of the video. Unit: seconds. |
|ModifyTime|String|2017-12-08T09:40:56Z|The last time when the video was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Size|Long|10897890|The size of the mezzanine file. Unit: byte. |
|Snapshots|List|\{"Snapshot":\["http://image.example.com/snapshot/sample000001.jpg? auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/sample00002.jpg?auth\_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52"\]\}|The array of video snapshot URLs. |
|Status|String|Normal|The status of the video. Valid values:

-   **Uploading:**: indicates that the video is being uploaded.
-   **UploadFail**: indicates that the video failed to be uploaded.
-   **UploadSucces**: indicates that the video was uploaded.
-   **Transcoding**: indicates that the video is being transcoded.
-   **TranscodeFail**: indicates that the video failed to be transcoded.
-   **Blocked**: indicates that the video is blocked.
-   **Normal**: indicates that the video is in a normal state. |
|Tags|String|Tag 1, Tag 2|The tags of the video. Separate multiple tags with commas \(,\). |
|TemplateGroupId|String|1|The ID of the transcoding template group. |
|Title|String|Title of the ApsaraVideo VOD video|The title of the video. |
|VideoId|String|93ab850b4f6f\*\*\*\*\*54b6e91d24d81d4|The ID of the video. |
|RequestId|String|25818875-5F78-4A13-\*\*\*\*-D7393642CA58|The ID of the request. |
|Total|Integer|123|The total number of videos returned. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ListLiveRecordVideo
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListLiveRecordVideoResponse>
  <RequestId>25818875-5F78-4A13-****-D7393642CA58</RequestId>
  <Total>123</Total>
  <LiveRecordVideoList>
        <LiveRecordVideo>
              <PlaylistId>****</PlaylistId>
              <StreamName>live-test</StreamName>
              <RecordStartTime>2017-12-08T07:40:56Z</RecordStartTime>
              <RecordEndTime>2017-12-08T08:40:56Z</RecordEndTime>
              <DomainName>example.com</DomainName>
              <AppName>testApp</AppName>
        </LiveRecordVideo>
        <LiveRecordVideo>
              <Video>
                    <Status>Normal</Status>
                    <ModifyTime>2017-12-08T09:40:56Z</ModifyTime>
                    <Description>Description of the ApsaraVideo VOD video</Description>
                    <VideoId>93ab850b4f6f*****54b6e91d24d81d4</VideoId>
                    <Size>10897890</Size>
                    <Title>Title of the ApsaraVideo VOD video</Title>
                    <Duration>135.6</Duration>
                    <CateName>Category name</CateName>
                    <CateId>78</CateId>
                    <CreationTime>2017-12-08T07:40:56Z</CreationTime>
                    <CoverURL>https://image.example.com/coversample.jpg</CoverURL>
                    <Snapshots>
                          <Snapshot>{"Snapshot":["http://image.example.com/snapshot/sample000001.jpg? auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52","http://image.example.com/snapshot/sample00002.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52"]}</Snapshot>
                    </Snapshots>
                    <Tags>Tag 1, Tag 2</Tags>
                    <TemplateGroupId>1</TemplateGroupId>
              </Video>
        </LiveRecordVideo>
  </LiveRecordVideoList>
</ListLiveRecordVideoResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A13-****-D7393642CA58",
    "Total": "123",
    "LiveRecordVideoList": {
        "LiveRecordVideo": [{
            "PlaylistId": "****",
            "StreamName": "live-test",
            "RecordStartTime": "2017-12-08T07:40:56Z",
            "RecordEndTime": "2017-12-08T08:40:56Z",
            "DomainName": "example.com",
            "AppName": "testApp"
        }, {
            "Video": {
                "Status": "Normal",
                "ModifyTime": "2017-12-08T09:40:56Z",
                "Description": "Description of the ApsaraVideo VOD video",
                "VideoId": "93ab850b4f6f*****54b6e91d24d81d4",
                "Size": "10897890",
                "Title": "Title of the ApsaraVideo VOD video",
                "Duration": "135.6",
                "CateName": "Category name",
                "CateId": "78",
                "CreationTime": "2017-12-08T07:40:56Z",
                "CoverURL": "https://image.example.com/coversample.jpg",
                "Snapshots": {
                    "Snapshot": "{\"Snapshot\":[\"http://image.example.com/snapshot/sample000001.jpg? auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e273334f52\",\"http://image.example.com/snapshot/sample00002.jpg?auth_key=1498476426-0-0-f00b9455c49a423ce69cf4e272434f52\"]}"
                },
                "Tags": "Tag 1, Tag 2",
                "TemplateGroupId": "1"
            }
        }]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

The following table describes the errors that are specific to this operation. For more information about errors common to all operations, see [Common errors](~~52841~~).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|IpsIsEmpty

|The specified “Ips” can not be empty.

|400

|The error message returned because the Ips parameter is not specified. |
|IpsExceededMax

|The specified Ips count has exceeded 100.

|403

|The error message returned because more than 100 IP addresses are added to a group. |
|SecurityIpGroupExceededMax

|The audit security group count has exceeded 10.

|403

|The error message returned because the number of review security groups exceeds the upper limit. |

