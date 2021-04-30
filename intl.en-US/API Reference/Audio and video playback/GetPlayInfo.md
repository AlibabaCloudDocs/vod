# GetPlayInfo

Queries the streaming URL of a media file, such as a video or audio file, based on the video ID.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetPlayInfo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetPlayInfo|The operation that you want to perform. Set the value to **GetPlayInfo**. |
|VideoId|String|Yes|93ab850b4f6\*\*\*\*\*54b6e91d24d81d4|The ID of the video. |
|Formats|String|No|mp4,mp3|The format of the video stream. Separate multiple formats with commas \(,\). Valid values:

 -   **mp4**
-   **m3u8**
-   **mp3**
-   **mpd**

 **Note:** If you do not set this parameter, ApsaraVideo VOD returns video streams in all the preceding formats by default. However, video streams in the MPD format are returned only if the MPD container format is configured in the transcoding template. For more information, see the Container parameter in the [TranscodeTemplate](~~52839~~) table. |
|AuthTimeout|Long|No|1800|The validity period of the streaming URL. Unit: seconds.

 -   If the OutputType parameter is set to **cdn**:
    -   The streaming URL has a validity period only if URL signing is enabled. Otherwise, the streaming URL is permanently valid.
    -   Minimum value: **1**.
    -   Maximum value: unlimited.
    -   Default value: If you do not set this parameter, the default validity period that is specified in URL signing is used.
-   If the OutputType parameter is set to **oss**:
    -   The image URL has a validity period only if the permissions on the Object Storage Service \(OSS\) bucket are private. Otherwise, the image URL is permanently valid.
    -   Minimum value: **1**.
    -   Maximum value: **2592000** \(30 days\). The maximum value is limited to reduce security risks of the origin.
    -   Default value: If you do not set this parameter, the default value is **3600**. |
|OutputType|String|No|cdn|The type of the streaming URL. Valid values:

 -   **oss**: OSS URL
-   **cdn** \(default\): CDN URL

 **Note:** If you specify an OSS URL for the video stream, the video stream must be in the MP4 format. |
|StreamType|String|No|video|The type of the video stream. Separate multiple types with commas \(,\). Valid values:

 -   **video**
-   **audio**

 If you do not set this parameter, both video and audio streams are returned by default. |
|ReAuthInfo|String|No|\{"uid":"12345","rand":"abckljd"\}|The CDN reauthentication configuration. The value is a JSON string. If CDN reauthentication is enabled, you can use this parameter to set the uid and rand fields for URL signing. For more information, see [URL authentication](~~57007~~). |
|Definition|String|No|FD|The definition of the video stream. Separate multiple definitions with commas \(,\). Valid values:

 -   **FD**: low definition
-   **LD**: standard definition
-   **SD**: high definition
-   **HD**: ultra high definition
-   **OD**: original quality
-   **2K**: 2K resolution
-   **4K**: 4K resolution
-   **SQ**: standard sound quality
-   **HQ**: high sound quality
-   **AUTO**: adaptive bitrate

 **Note:** If you do not set this parameter, ApsaraVideo VOD returns video streams in all the preceding definitions by default. However, video streams for adaptive bitrate streaming are returned only if the PackageSetting parameter is set in the transcoding template. For more information, see the PackageSetting parameter in the [TranscodeTemplate](~~52839~~) table. |
|ResultType|String|No|Single|The type of the returned data. Valid values:

 -   **Single** \(default\): Only one latest transcoded stream is returned for each definition and format.
-   **Multiple**: All transcoded streams are returned for each definition and format. |
|PlayConfig|String|No|\{"PlayDomain":"vod.test\_domain","XForwardedFor":"yqCD7Fp1uqChoVj/sl/p5Q==","PreviewTime":"20","MtsHlsUriToken":"yqCD7Fp1uqChoVjslp5Q"\}|The custom playback configuration. The value is a JSON string. You can specify a domain name for playback. For more information, see [PlayConfig](~~86952~~).

 **Note:** If you do not set the PlayConfig parameter or the PlayDomain parameter that is nested under the PlayConfig parameter, the default domain name configured in ApsaraVideo VOD is used in this operation. If no default domain name is configured, the domain names are queried in reverse chronological order based on the time when the domain names were last modified. The latest domain name that was modified is used as the streaming domain name. To ensure that the returned domain name meets your requirements, we recommend that you set a default streaming domain name in the console. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|52c7e33c-0c17-47\*\*\*\*\*c1-efd6f26d368d|The ID of the request. |
|PlayInfoList|Array of PlayInfo| |The information about the video stream. |
|PlayInfo| | | |
|Bitrate|String|992.7800|The bitrate of the video stream. Unit: Kbit/s. |
|CreationTime|String|2017-06-26T05:38:48Z|The time when the video stream was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Definition|String|LD|The definition of the video stream. Valid values:

 -   **LD**: low definition
-   **SD**: standard definition
-   **HD**: high definition.
-   **FHD**: ultra high definition
-   **OD**: original quality
-   **2K**: 2K resolution
-   **4K**: 4K resolution
-   **SQ**: standard sound quality
-   **HQ**: high sound quality |
|Duration|String|3.1667|The duration of the video stream. Unit: seconds. |
|Encrypt|Long|1|Indicates whether the video stream was encrypted. Valid values:

 -   **0**: no
-   **1**: yes |
|EncryptType|String|AliyunVoDEncryption|The type of encryption that was performed on the video stream. Valid values:

 -   **AliyunVoDEncryption**: Alibaba Cloud proprietary cryptography
-   **HLSEncryption**: HTTP-Live-Streaming \(HLS\) encryption |
|Format|String|mp4|The format of the video stream. If the media file is a video file, the following valid values are included:

 -   **mp4**
-   **m3u8**

 **Note:** If the media file is an audio-only file, the value is **mp3**. |
|Fps|String|30.0032|The frame rate of the video stream. Unit: frames per second. |
|Height|Long|960|The height of the video stream. Unit: pixel. |
|JobId|String|fd1c76fc806b\*\*\*\*\*194405528706d29|The job ID for transcoding the media stream. This ID uniquely identifies a media stream. |
|ModificationTime|String|2017-06-26T05:40:48Z|The time when the video stream was updated. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|NarrowBandType|String|0|The type of Narrowband HD™. Valid values:

 -   **0**: normal transcoding
-   **1.0**: Narrowband HD™ 1.0
-   **2.0**: Narrowband HD™ 2.0

 This parameter only takes effect when a definition that is available in the built-in Narrowband HD™ 1.0 transcoding template is specified. For more information, see the Definition parameter in the [TranscodeTemplate](~~52839~~) table. |
|PlayURL|String|http://vod.aliyunsample.com/ABEBDE15CC479FD4D1329/52a53151eba5226f8e2da3b55bc57c49.m3u8?auth\_key=abdf2123-6783232\*\*\*\*|The streaming URL of the video stream. |
|Size|Long|418112|The size of the video stream.Unit: byte. |
|Specification|String|H264.LD|The specifications of transcoded audio and video streams. For more information about the value range, see [Output specifications](~~124671~~). |
|Status|String|Normal|The status of the video stream. Valid values:

 -   **Normal**: The video stream can be played.
-   **Invisible**: The video stream is blocked. |
|StreamType|String|video|The type of the video stream. If the media stream is a video stream, the value is **video**. If the media stream is an audio-only stream, the value is **audio**. |
|WatermarkId|String|dgfn26457856\*\*\*\*|The ID of the watermark that is associated with the media stream. |
|Width|Long|540|The width of the video stream. Unit: pixel. |
|VideoBase|Struct| |The basic information about the video. |
|CoverURL|String|http://image.example.com/sample.jpg?auth\_key=2333232-atb\*\*\*\*|The URL of the video thumbnail. |
|CreationTime|String|2017-06-26T06:38:48Z|The time when the video file was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Duration|String|3.1667|The duration of the video. Unit: seconds. |
|MediaType|String|video|The type of the media file. Valid values:

 -   **video**: video
-   **audio** |
|Status|String|Normal|The status of the video. For more information about the value range and description, see the [Status](~~52839~~) table. |
|Title|String|ApsaraVideo VOD|The title of the video. |
|VideoId|String|93ab850b4f6\*\*\*\*\*54b6e91d24d81d4|The ID of the video. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetPlayInfo
&VideoId=93ab850b4f6*****54b6e91d24d81d4
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetPlayInfoResponse>
      <VideoBase>
            <Status>Normal</Status>
            <VideoId>93ab850b4f6*****54b6e91d24d81d4</VideoId>
            <CreationTime>2017-06-26T05:38:48Z</CreationTime>
            <MediaType>video</MediaType>
            <Title>ApsaraVideo VOD</Title>
            <Duration>3.1667</Duration>
            <CoverURL>http://image.example.com/sample.jpg?auth_key=2333232-atb****</CoverURL>
      </VideoBase>
      <RequestId>52c7e33c-0c17-47*****c1-efd6f26d368d</RequestId>
      <PlayInfoList>
            <PlayInfo>
                  <Status>Normal</Status>
                  <StreamType>video</StreamType>
                  <Size>418112</Size>
                  <WatermarkId>dgfn26457856****</WatermarkId>
                  <Fps>30.0032</Fps>
                  <Definition>LD</Definition>
                  <Specification>H264.LD</Specification>
                  <ModificationTime>2017-06-26T05:40:48Z</ModificationTime>
                  <Duration>3.1667</Duration>
                  <Bitrate>992.7800</Bitrate>
                  <Encrypt>1</Encrypt>
                  <Format>mp4</Format>
                  <EncryptType>AliyunVoDEncryption</EncryptType>
                  <NarrowBandType>0</NarrowBandType>
                  <PlayURL>http://vod.aliyunsample.com/ABEBDE15CC479FD4D1329/52a53151eba5226f8e2da3b55bc57c49.m3u8?auth_key=abdf2123-6783232****</PlayURL>
                  <CreationTime>2017-06-26T06:38:48Z</CreationTime>
                  <Height>960</Height>
                  <Width>540</Width>
                  <JobId>fd1c76fc806b*****194405528706d29</JobId>
            </PlayInfo>
      </PlayInfoList>
</GetPlayInfoResponse>
```

`JSON` format

```
{
	"VideoBase": {
		"Status": "Normal",
		"VideoId": "93ab850b4f6*****54b6e91d24d81d4",
		"CreationTime": "2017-06-26T05:38:48Z",
		"MediaType": "video",
		"Title": "ApsaraVideo VOD",
		"Duration": "3.1667",
		"CoverURL": "http://image.example.com/sample.jpg?auth_key=2333232-atb****"
	},
	"RequestId": "52c7e33c-0c17-47*****c1-efd6f26d368d",
	"PlayInfoList": {
		"PlayInfo": [{
			"Status": "Normal",
			"StreamType": "video",
			"Size": "418112",
			"WatermarkId": "dgfn26457856****",
			"Fps": "30.0032",
			"Definition": "LD",
			"Specification": "H264.LD",
			"ModificationTime": "2017-06-26T05:40:48Z",
			"Duration": "3.1667",
			"Bitrate": "992.7800",
			"Encrypt": "1",
			"Format": "mp4",
			"EncryptType": "AliyunVoDEncryption",
			"NarrowBandType": "0",
			"PlayURL": "http://vod.aliyunsample.com/ABEBDE15CC479FD4D1329/52a53151eba5226f8e2da3b55bc57c49.m3u8?auth_key=abdf2123-6783232****",
			"CreationTime": "2017-06-26T06:38:48Z",
			"Height": "960",
			"Width": "540",
			"JobId": "fd1c76fc806b*****194405528706d29"
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
|Forbidden.IllegalStatus

|Status of the video is illegal. Current Status is %s.

|403

|The error message returned because the video status is invalid, where %s indicates the current video status. Only videos in the **Normal** state can be played. |
|InvalidVideo.NotFound

|The video does not exist.

|404

|The error message returned because the video does not exist. |
|InvalidVideo.NoneStream

|The video has no stream to play for the request parameter 'Formats: mp4, Definition: LD, StreamType: video'.

|404

|The error message returned because no transcoded stream that meets the specified filter criteria is available for playback. Check whether the [transcoding configuration](~~86068~~) matches the filter criteria. |
|Forbidden.AliyunVoDEncryption

|Currently only the AliyunVoDEncryption stream exists, you must use the Aliyun player to play or set the value of ResultType to Multiple.

|403

|The error message returned because only transcoded stream files that are encrypted by using Alibaba Cloud proprietary cryptography exist. You must use ApsaraVideo Player to play the files or set the **ResultType** parameter to **Multiple**. |

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

