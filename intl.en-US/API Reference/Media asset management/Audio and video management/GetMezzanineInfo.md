# GetMezzanineInfo

Queries the information about the mezzanine file of an audio or video. The information includes the mezzanine file URL, resolution, and bitrate of the audio or video.

**Note:** You can obtain the complete mezzanine file information only after a stream is transcoded.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetMezzanineInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetMezzanineInfo|The operation that you want to perform. Set the value to **GetMezzanineInfo**. |
|VideoId|String|Yes|1f1a6fc03ca04\*\*\*\*\*814031b8a6559e|The ID of the video. |
|AuthTimeout|Long|No|3600|The validity period of the mezzanine file URL. Unit: seconds. Default value: **1800**. Minimum value: **1**.

 -   If the OutputType parameter is set to **cdn**:
    -   The mezzanine file URL has a validity period only if URL signing is enabled. Otherwise, the mezzanine file URL is permanently valid.
    -   Minimum value: **1**.
    -   Maximum Value: unlimited.
    -   Default value: If you do not set this parameter, the default validity period that is specified in URL signing is used.

 -   If the OutputType parameter is set to **oss**:
    -   The mezzanine file URL has a validity period only if the permissions on the Object Storage Service \(OSS\) bucket are private. Otherwise, the mezzanine file URL is permanently valid.
    -   Minimum value: **1**.
    -   Maximum value: **2592000** \(30 days\). The maximum value is limited to reduce security risks of the origin.
    -   Default value: If you do not set this parameter, the default value is **3600**. |
|OutputType|String|No|oss|The type of the mezzanine file URL. Valid values:

 -   **oss**: OSS URL
-   **cdn** \(default\): Content Delivery Network \(CDN\) URL

 **Note:** If the mezzanine file is stored in a bucket of the in type, only an OSS URL is returned. |
|AdditionType|String|No|video|The type of additional information. Separate multiple values with commas \(,\). By default, only the basic information is returned. Valid values:

 -   **video**: video stream information
-   **audio**: audio stream information |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|Mezzanine|Struct| |The information about the mezzanine file. |
|AudioStreamList|Array of AudioStream| |The information about the audio stream. |
|Bitrate|String|62.885|The bitrate. |
|ChannelLayout|String|mono|The output layout of the sound channels. Valid values:

 -   **mono**: mono sound channel
-   **stereo**: two sound channels |
|Channels|String|1|The number of sound channels. |
|CodecLongName|String|AAC \(Advanced Audio Coding\)|The full name of the codec format. |
|CodecName|String|aac|The short name of the codec format. |
|CodecTag|String|0x6134706d|The tag of the codec format. |
|CodecTagString|String|mp4a|The tag string of the codec format. |
|CodecTimeBase|String|1/44100|The codec time base. |
|Duration|String|3.227574|The duration of the audio stream. |
|Index|String|0|The sequence number of the audio stream, which specifies the position of the audio stream in all audio streams. |
|Lang|String|und|The language. |
|NumFrames|String|1|The total number of frames. |
|SampleFmt|String|fltp|The sampling format. |
|SampleRate|String|44100|The sample rate. |
|StartTime|String|2017-01-11T12:00:00Z|The beginning of the time range that was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Timebase|String|0.000000|The time base. |
|Bitrate|String|771.2280|The bitrate of the file. Unit: Kbit/s. |
|CreationTime|String|2017-11-14T09:15:50Z|The time when the file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Duration|String|42.4930|The duration of the file. Unit: seconds. |
|FileName|String|cbf317e6c908cd1a224bd85d46978\*\*\*\*.mp4|The name of the file. |
|FileURL|String|http://example.com/customerTrans/e2bf0614af0254c744a6422806ad8cff/457D396A-15FB9D03164-1389-0829-084-\*\*\*\*.mp4?Expires=1513173337&OSSAccessKeyId=LTAIJ1n\*\*\*\*\*7cAL&Signature=ngisNAr27V%2FXBtNysLbt9ebYhzU%3D|The URL of the file. |
|Fps|String|25.0000|The frame rate of the file. Unit: frames per second. |
|Height|Long|540|The height of the file. Unit: pixel. |
|OutputType|String|oss|The type of the mezzanine file URL. Valid values:

 -   **oss**: OSS URL
-   **cdn** \(default\): CDN URL

 **Note:** If you specify an OSS URL for the video stream, the video stream must be in the MP4 format. |
|Size|Long|4096477|The size of the file. Unit: byte. |
|Status|String|Normal|The status of the file. Valid values:

 -   **Uploading**: The file is being uploaded. This is the initial status.
-   **Normal**: The file is uploaded.
-   **UploadFail**: The file fails to be uploaded.
-   **Deleted**: The file is deleted. |
|VideoId|String|73ad78c6a6cb446\*\*\*\*\*0f24c0e24d65|The ID of the video. |
|VideoStreamList|Array of VideoStream| |The information about the video stream. |
|AvgFPS|String|30.0|The average frame rate. |
|Bitrate|String|500|The bitrate of the file. Unit: Kbit/s. |
|CodecLongName|String|H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10|The full name of the codec format. |
|CodecName|String|h264|The short name of the codec format. |
|CodecTag|String|0x31637661|The tag of the codec format. |
|CodecTagString|String|avc1|The tag string of the codec format. |
|CodecTimeBase|String|1/60|The codec time base. |
|Dar|String|0:1|The display aspect ratio. |
|Duration|String|3.166667|The duration of the video stream. |
|Fps|String|30.0|The target frame rate. |
|HasBFrames|String|0|Indicates whether the video stream contains bidirectional frames \(B-frames\). |
|Height|String|320|The height of the video resolution. |
|Index|String|1|The sequence number of the video stream, which indicates the position of the video stream in all video streams. |
|Lang|String|und|The language. |
|Level|String|30|The codec level. |
|NumFrames|String|0|The total number of frames. |
|PixFmt|String|yuv420p|The pixel format. |
|Profile|String|Main|The codec profile. |
|Rotate|String|90|The rotation angle of the video. Valid values: **\[0, 360\)**. |
|Sar|String|0:1|The sample aspect ratio. |
|StartTime|String|2017-01-11T12:00:00Z|The beginning of the time range that was queried. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Timebase|String|0.000000|The time base. |
|Width|String|568|The width of the video resolution. |
|Width|Long|960|The width of the file. Unit: pixel. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetMezzanineInfo
&VideoId=1f1a6fc03ca04*****814031b8a6559e
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetMezzanineInfoResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
  <Mezzanine>
        <Status>Normal</Status>
        <VideoId>73ad78c6a6cb446*****0f24c0e24d65</VideoId>
        <CRC64>461bb6d0f24c0e24d65</CRC64>
        <Size>4096477</Size>
        <FileName>cbf317e6c908cd1a224bd85d46978****.mp4</FileName>
        <Fps>25.0000</Fps>
        <Duration>42.4930</Duration>
        <VideoStreamList>
              <CodecTag>0x31637661</CodecTag>
              <CodecTimeBase>1/60</CodecTimeBase>
              <Rotate>90</Rotate>
              <Sar>0:1</Sar>
              <StartTime>2017-01-11T12:00:00Z</StartTime>
              <Fps>30.0</Fps>
              <Lang>und</Lang>
              <Duration>3.166667</Duration>
              <Index>1</Index>
              <PixFmt>yuv420p</PixFmt>
              <Bitrate>500</Bitrate>
              <CodecName>h264</CodecName>
              <AvgFPS>30.0</AvgFPS>
              <Profile>Main</Profile>
              <Timebase>0.000000</Timebase>
              <HasBFrames>0</HasBFrames>
              <CodecTagString>avc1</CodecTagString>
              <Dar>0:1</Dar>
              <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
              <Level>30</Level>
              <Height>320</Height>
              <NumFrames>0</NumFrames>
              <Width>568</Width>
        </VideoStreamList>
        <AudioStreamList>
              <CodecTag>0x6134706d</CodecTag>
              <CodecTimeBase>1/44100</CodecTimeBase>
              <ChannelLayout>mono</ChannelLayout>
              <StartTime>2017-01-11T12:00:00Z</StartTime>
              <Lang>und</Lang>
              <Duration>3.227574</Duration>
              <Index>0</Index>
              <SampleFmt>fltp</SampleFmt>
              <Bitrate>62.885</Bitrate>
              <CodecName>aac</CodecName>
              <Channels>1</Channels>
              <Timebase>0.000000</Timebase>
              <CodecTagString>mp4a</CodecTagString>
              <SampleRate>44100</SampleRate>
              <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
              <NumFrames>1</NumFrames>
        </AudioStreamList>
        <Bitrate>771.2280</Bitrate>
        <PreprocessStatus>UnPreprocess</PreprocessStatus>
        <FileURL>http://example.com/customerTrans/e2bf0614af0254c744a6422806ad8cff/457D396A-15FB9D03164-1389-0829-084-****.mp4?Expires=1513173337&amp;OSSAccessKeyId=LTAIJ1n*****7cAL&amp;Signature=ngisNAr27V%2FXBtNysLbt9ebYhzU%3D</FileURL>
        <CreationTime>2017-11-14T09:15:50Z</CreationTime>
        <Height>540</Height>
        <Width>960</Width>
        <OutputType>oss</OutputType>
  </Mezzanine>
</GetMezzanineInfoResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "Mezzanine": {
        "Status": "Normal",
        "VideoId": "73ad78c6a6cb446*****0f24c0e24d65",
        "CRC64": "461bb6d0f24c0e24d65",
        "Size": "4096477",
        "FileName": "cbf317e6c908cd1a224bd85d46978****.mp4",
        "Fps": "25.0000",
        "Duration": "42.4930",
        "VideoStreamList": [{
            "CodecTag": "0x31637661",
            "CodecTimeBase": "1/60",
            "Rotate": "90",
            "Sar": "0:1",
            "StartTime": "2017-01-11T12:00:00Z",
            "Fps": "30.0",
            "Lang": "und",
            "Duration": "3.166667",
            "Index": "1",
            "PixFmt": "yuv420p",
            "Bitrate": "500",
            "CodecName": "h264",
            "AvgFPS": "30.0",
            "Profile": "Main",
            "Timebase": "0.000000",
            "HasBFrames": "0",
            "CodecTagString": "avc1",
            "Dar": "0:1",
            "CodecLongName": "H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10",
            "Level": "30",
            "Height": "320",
            "NumFrames": "0",
            "Width": "568"
        }],
        "AudioStreamList": [{
            "CodecTag": "0x6134706d",
            "CodecTimeBase": "1/44100",
            "ChannelLayout": "mono",
            "StartTime": "2017-01-11T12:00:00Z",
            "Lang": "und",
            "Duration": "3.227574",
            "Index": "0",
            "SampleFmt": "fltp",
            "Bitrate": "62.885",
            "CodecName": "aac",
            "Channels": "1",
            "Timebase": "0.000000",
            "CodecTagString": "mp4a",
            "SampleRate": "44100",
            "CodecLongName": "AAC (Advanced Audio Coding)",
            "NumFrames": "1"
        }],
        "Bitrate": "771.2280",
        "PreprocessStatus": "UnPreprocess",
        "FileURL": "http://example.com/customerTrans/e2bf0614af0254c744a6422806ad8cff/457D396A-15FB9D03164-1389-0829-084-****.mp4?Expires=1513173337&OSSAccessKeyId=LTAIJ1n*****7cAL&Signature=ngisNAr27V%2FXBtNysLbt9ebYhzU%3D",
        "CreationTime": "2017-11-14T09:15:50Z",
        "Height": "540",
        "Width": "960",
        "OutputType": "oss"
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

|The error message returned because the specified video ID does not exist. |
|InvalidFile.NotFound

|The file does not exist.

|404

|The error message returned because the specified video mezzanine file does not exist. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

