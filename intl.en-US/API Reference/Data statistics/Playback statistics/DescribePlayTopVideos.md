# DescribePlayTopVideos

Queries daily playback statistics on top videos, including video views, unique visitors, and total playback duration.

**Note:**

-   This operation is available only in the **China \(Shanghai\)**region.
-   You can query playback statistics on top 1,000 videos at most on a specified day. Top videos are sorted in descending order based on video views.
-   You can call this operation to query only playback statistics collected from videos that are played by using ApsaraVideo Player SDKs.
-   Playback statistics for the previous day are generated at 09:00 on the current day, in UTC+8.
-   You can query data that is generated since January 1, 2018. The maximum time range to query is 180 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribePlayTopVideos&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribePlayTopVideos|The operation that you want to perform. Set the value to **DescribePlayTopVideos**. |
|BizDate|String|Yes|2016-06-29T13:00:00Z|The time to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|PageNo|Long|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Long|No|100|The number of entries to return on each page. Valid values:

-   Default value: **100**.
-   Maximum value: **1000**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageSize|Long|100|The number of entries returned per page. |
|PageNo|Long|1|The page number of the returned page. |
|TotalNum|Long|2|The total number of entries that were collected in playback statistics on top videos. |
|TopPlayVideos|Array of TopPlayVideoStatis| |The details of daily playback statistics on each top video. |
|TopPlayVideoStatis| | | |
|VideoId|String|2a8d4cb9ecbb487681473a15\*\*\*\*8fda|The ID of the video. |
|PlayDuration|String|4640369|The playback duration. Unit: milliseconds. |
|Title|String|Four streams \(two streams encrypted\): LD-HLS-encrypted + SD-MP4 + HD-H|The title of the video. |
|VV|String|107|The number of video views. |
|UV|String|1|The number of unique visitors. |
|RequestId|String|4B0BCF9F-2FD5-4817-\*\*\*\*-7BEBBE3AF90B"|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribePlayTopVideos
&BizDate=2016-06-29T13:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribePlayTopVideosResponse>
      <TopPlayVideos>
            <TopPlayVideoStatis>
                  <VideoId>2a8d4cb9ecbb487681473**53aba8fda</VideoId>
                  <VV>107</VV>
                  <Title>Four streams (two streams encrypted): LD-HLS-encrypted + SD-MP4 + HD-H</Title>
                  <UV>1</UV>
                  <PlayDuration>4640369</PlayDuration>
            </TopPlayVideoStatis>
            <TopPlayVideoStatis>
                  <VideoId>cca9dbd11b7045808cc9b**c56f5bad2</VideoId>
                  <VV>33</VV>
                  <Title>Two streams (both streams encrypted): SD-HLS-encrypted + UHD-HLS-encrypted</Title>
                  <UV>1</UV>
                  <PlayDuration>4689369</PlayDuration>
            </TopPlayVideoStatis>
      </TopPlayVideos>
      <PageSize>1000</PageSize>
      <PageNo>1</PageNo>
      <Total>150</Total>
      <RequestId>4B0BCF9F-2FD5-4817-****-7BEBBE3AF90B</RequestId>
</DescribePlayTopVideosResponse>
```

`JSON` format

```
{
    "TopPlayVideos": {
        "TopPlayVideoStatis": [
            {
                "VideoId": "2a8d4cb9ecbb487681473**53aba8fda", 
                "VV": "107", 
                "Title": "Four streams (two streams encrypted): LD-HLS-encrypted + SD-MP4 + HD-H", 
                "UV": "1",
                "PlayDuration":"4640369"
            }, 
            {
                "VideoId": "cca9dbd11b7045808cc9b**c56f5bad2", 
                "VV": "33", 
                "Title": "Two streams (both streams encrypted): LD-HLS-encrypted + UHD-HLS-encrypted", 
                "UV": "1",
                "PlayDuration":"4689369"
            }
           
        ]
    }, 
    "PageSize": "1000",
    "PageNo":  "1",
    "Total": "150",
    "RequestId": "4B0BCF9F-2FD5-4817-****-7BEBBE3AF90B"
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
|InternalError

|The request processing has failed due to some unknown error.

|500

|The error message returned because an unknown error has occurred. |
|InvalidBizDate.Malformed

|Specified BizDate is malformed.

|400

|The error message returned because the format of the time that is specified by the BizDate parameter in invalid. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|InvalidBizDate.BeyondCurrent

|EndTime beyond current time.

|400

|The error message returned because the time that is specified by the BizDate parameter is later than the current time. |

