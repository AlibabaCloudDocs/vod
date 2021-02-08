# DescribePlayVideoStatis

Queries daily playback statistics on a video in a specified time range.

**Note:**

-   This operation is available only in the **China \(Shanghai\)** region.
-   You can call this operation to query only playback statistics collected from videos that are played by using ApsaraVideo Player SDKs.
-   Playback statistics for the previous day are generated at 09:00 on the current day, in UTC+8.
-   You can query only data in the last 730 days. The maximum time range to query is 180 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DescribePlayVideoStatis&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribePlayVideoStatis|The operation that you want to perform. Set the value to **DescribePlayVideoStatis**. |
|StartTime|String|Yes|2016-06-29T13:00:00Z|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|EndTime|String|Yes|2016-06-30T13:00:00Z|The end of the time range to query. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|VideoId|String|Yes|2a8d4cb9ecbb487681473\*\*\*\*aba8fda|The ID of the video. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A92D3600-A3E7-43D6-\*\*\*\*-B6E3B4A1FE6B|The ID of the request. |
|VideoPlayStatisDetails|Array of VideoPlayStatisDetail| |The details of daily playback statistics on the video. |
|VideoPlayStatisDetail| | | |
|Date|String|20170120|The date when the statistics were generated. The date follows the *yyyy-MM-dd* format. |
|PlayDuration|String|967277|The playback duration. Unit: milliseconds. |
|PlayRange|String|<=1m:79.2%;\>1<=5m:16.7%;\>5<=10m:4.2%|The distribution of the playback duration. |
|Title|String|Four streams \(one stream encrypted\): LD-HLS + SD-MP4 + HD-HLS-encrypted + UHD-MP4|The title of the video. |
|VV|String|24|The number of video views. |
|UV|String|1|The number of unique visitors. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DescribePlayVideoStatis
&StartTime=2016-06-29T13:00:00Z
&EndTime=2016-06-30T13:00:00Z
&VideoId=2a8d4cb9ecbb487681473****aba8fda
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribePlayVideoStatisResponse>
      <RequestId>A92D3600-A3E7-43D6-****-B6E3B4A1FE6B</RequestId>
      <VideoPlayStatisDetails>
            <VideoPlayStatisDetail>
                  <Date>20180101</Date>
                  <PlayDuration>3288</PlayDuration>
                  <PlayRange>&lt;=1m:79.2%;&gt;1&lt;=5m:16.7%;&gt;5&lt;=10m:4.2%</PlayRange>
                  <Title>Four streams (one stream encrypted): LD-HLS + SD-MP4 + HD-HLS-encrypted + UHD-MP4</Title>
                  <UV>1</UV>
                  <VV>1</VV>
            </VideoPlayStatisDetail>
            <VideoPlayStatisDetail>
                  <Date>20180102</Date>
                  <PlayDuration>967277</PlayDuration>
                  <PlayRange>&lt;=1m:79.2%;&gt;1&lt;=5m:16.7%;&gt;5&lt;=10m:4.2%</PlayRange>
                  <Title>Four streams (one stream encrypted): LD-HLS + SD-MP4 + HD-HLS-encrypted + UHD-MP4</Title>
                  <UV>1</UV>
                  <VV>24</VV>
            </VideoPlayStatisDetail>
      </VideoPlayStatisDetails>
</DescribePlayVideoStatisResponse>
```

`JSON` format

```
{
    "RequestId":"A92D3600-A3E7-43D6-****-B6E3B4A1FE6B",
    "VideoPlayStatisDetails":{
        "VideoPlayStatisDetail":[
            {
                "Date":"20180101",
                "PlayDuration":"3288",
                "PlayRange":"<=1m:79.2%;>1<=5m:16.7%;>5<=10m:4.2%",
                "Title": "Four streams (one stream encrypted): LD-HLS + SD-MP4 + HD-HLS-encrypted ​​​+ UHD-MP4",
                "UV":"1",
                "VV":"1"
            },
            {
                "Date":"20180102",
                "PlayDuration":"967277",
                "PlayRange":"<=1m:79.2%;>1<=5m:16.7%;>5<=10m:4.2%",
                "Title": "Four streams (one stream encrypted): LD-HLS + SD-MP4 + HD-HLS-encrypted ​​​+ UHD-MP4",
                "UV":"1",
                "VV":"24"
            }
        ]
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
|InternalError

|The request processing has failed due to some unknown error.

|500

|The error message returned because an unknown error has occurred. |
|InvalidStartTime.Malformed

|Specified StartTime is malformed.

|400

|The error message returned because the format of the start time is invalid. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|InvalidEndTime.Malformed

|Specified EndTime is malformed.

|400

|The error message returned because the format of the end time is invalid. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|InvalidEndTime.BeyondCurrent

|EndTime beyond current time.

|400

|The error message returned because the end time is later than the current time. |
|InvalidEndTime.Mismatch

|StartTime or EndTime is mismatch.

|400

|The error message returned because the time range that is specified by the StartTime and EndTime parameters is invalid. |

