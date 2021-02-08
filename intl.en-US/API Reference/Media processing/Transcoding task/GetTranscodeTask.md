# GetTranscodeTask

Queries the details of a transcoding job based on the transcoding task ID.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetTranscodeTask&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTranscodeTask|The operation that you want to perform. Set the value to **GetTranscodeTask**. |
|TranscodeTaskId|String|Yes|b1b65ab107e14\*\*\*\*\*3dbb900f6c1fe0|The ID of the transcoding task. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|F4C6D5BE-BF13-45\*\*\*\*\*6C-516EA8906DCD|The ID of the request. |
|TranscodeTask|Struct| |The information about the transcoding task. |
|CompleteTime|String|2019-01-23T12:40:12Z|The time when the transcoding task was complete. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CreationTime|String|2019-01-23T12:35:12Z|The time when the transcoding task was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|TaskStatus|String|Processing|The status of the transcoding task. Valid values:

 -   **Processing**: The transcoding is in progress.
-   **Partial**: The video was partially transcoded.
-   **CompleteAllSucces**: The transcoding task was complete and the video was fully transcoded.
-   **CompleteAllFail**: All the transcoding jobs were complete but the video failed to be transcoded. If an exception occurs in the mezzanine file, no transcoding job is initiated and the transcoding task fails.
-   **CompletePartialSucc**: All the transcoding jobs were complete but the video was partially transcoded. |
|TranscodeJobInfoList|Array of TranscodeJobInfo| |The information about the transcoding job. |
|CompleteTime|String|2019-02-26T08:30:16Z|The time when the transcoding job was complete. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CreationTime|String|2019-02-26T08:27:16Z|The time when the transcoding job was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Definition|String|LD|The definition of the video. Multiple definitions are separated by commas \(,\). Valid values:

 -   **LD**: low definition.
-   **SD**: standard definition.
-   **HD**: high definition.
-   **FHD**: ultra high definition.
-   **OD**: original quality.
-   **2K**: 2K resolution.
-   **4K**: 4K resolution.
-   **SQ**: standard sound quality.
-   **HQ**: high sound quality.
-   **AUTO**: adaptive bitrate. This parameter is returned only when you set the PackageSetting parameter for the transcoding template. For more information, see the PackageSetting parameter in the [Basic data types](~~52839~~) topic.

 **Note:** The value of this parameter only indicates the definition that is configured for the transcoding template and does not indicate the actual resolution range of the output video. |
|ErrorCode|String|200|The error code returned when the transcoding job fails. |
|ErrorMessage|String|ErrorMessage|The error message returned when the transcoding job fails. |
|InputFileUrl|String|http://outin-40564\*\*\*\*\*e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/5b95e568f8e\*\*\*\*\*47f38e/31f1184c-\*\*\*\*\*b2a2-f94-c213f.wmv|The Object Storage Service \(OSS\) URL of the mezzanine file. |
|OutputFile|Struct| |The information about the output file. |
|AudioStreamList|String|"AudioStreamList": "\[\{\\"Bitrate\\":\\"64.533\\",\\"ChannelLayout\\":\\"stereo\\",\\"Channels\\":\\"2\\",\\"CodecLongName\\":\\"AAC \(Advanced Audio Coding\)\\",\\"CodecName\\":\\"aac\\",\\"CodecTag\\":\\"0x6134706d\\",\\"CodecTagString\\":\\"mp4a\\",\\"CodecTimeBase\\":\\"1/44100\\",\\"Duration\\":\\"12.615533\\",\\"Index\\":\\"1\\",\\"Lang\\":\\"und\\",\\"SampleFmt\\":\\"fltp\\",\\"Samplerate\\":\\"44100\\",\\"StartTime\\":\\"-0.046440\\",\\"Timebase\\":\\"1/44100\\"\}\]|The audio streams. |
|Bitrate|String|964|The average bitrate of the output file. Unit: Kbit/s. |
|Duration|String|12|The length of the output file. Unit: seconds. |
|Encryption|String|\{\\"EncryptType\\":\\"AliyunVoDEncryption\\"\}|The encryption configuration used by the output file. Valid values:

 -   **AliyunVoDEncryption**: Alibaba Cloud proprietary cryptography.
-   **HLSEncryption**: HTTP-Live-Streaming \(HLS\) encryption. |
|Filesize|Long|851076|The size of the output file. Unit: byte. |
|Format|String|m3u8|The encapsulation format of the output file. |
|Fps|String|25|The frame rate of the output file. Unit: frames per second. |
|Height|String|360|The height of the output video. Unit: px. |
|OutputFileUrl|String|http://outin-40564\*\*\*\*\*e1403e7.oss-cn-shanghai.aliyuncs.com/883f5d\*\*\*\*\*f20aaa352f/c3be4f073\*\*\*\*\*7d5193ec8-\{DestMd5\}-od-S00000001-200000.mp4|The OSS URL of the output file. |
|SubtitleStreamList|String|\[\]|The subtitle streams. |
|VideoStreamList|String|\[\{\\"AvgFPS\\":\\"30.0\\",\\"Bitrate\\":\\"933.814\\",\\"CodecLongName\\":\\"H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10\\",\\"CodecName\\":\\"h264\\",\\"CodecTag\\":\\"0x31637661\\",\\"CodecTagString\\":\\"avc1\\",\\"CodecTimeBase\\":\\"1/60\\",\\"Dar\\":\\"9:16\\",\\"Duration\\":\\"12.033333\\",\\"Fps\\":\\"30.0\\",\\"HasBFrames\\":\\"2\\",\\"Height\\":\\"360\\",\\"Index\\":\\"0\\",\\"Lang\\":\\"und\\",\\"Level\\":\\"30\\",\\"PixFmt\\":\\"yuv420p\\",\\"Profile\\":\\"High\\",\\"Sar\\":\\"81:256\\",\\"StartTime\\":\\"0.000000\\",\\"Timebase\\":\\"1/15360\\",\\"Width\\":\\"640\\"\}\]|The video streams. |
|WatermarkIdList|List|\["64079a0e3e286\*\*\*\*\*b48a8c9413"\]|The IDs of the watermarks used by the output file. |
|Width|String|640|The width of the output video. Unit: px. |
|Priority|String|6|The priority of the transcoding task. |
|TranscodeJobId|String|38f0e513c88\*\*\*\*\*85515f9d50be188|The ID of the transcoding job. |
|TranscodeJobStatus|String|Transcoding|The status of the transcoding job.

 -   **Transcoding**: The transcoding job is running.
-   **TranscodeSuccess**: The transcoding job was successful.
-   **TranscodeFail**: The transcoding job failed. |
|TranscodeProgress|Long|100|The progress of the transcoding job. Valid values: `0 to 100`. |
|TranscodeTemplateId|String|174b0534fea3\*\*\*\*\*b51c8f0ad1374|The ID of the transcoding template used for transcoding. |
|TranscodeTaskId|String|b1b65ab107e14\*\*\*\*\*3dbb900f6c1fe0|The ID of the transcoding task. |
|TranscodeTemplateGroupId|String|b500c7094bd241\*\*\*\*\*3e9900752d7c3|The ID of the transcoding template group. |
|Trigger|String|Auto|The trigger type. Valid values:

 -   **Auto**: The transcoding task is automatically triggered when the video is uploaded.
-   **Manual**: The transcoding task is triggered after you call the SubmitTranscodeJobs operation. |
|VideoId|String|883f5d98107\*\*\*\*\*b7f20aaa352f|The ID of the video. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetTranscodeTask
&TranscodeTaskId=b1b65ab107e14*****3dbb900f6c1fe0
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetTranscodeTaskResponse>
  <RequestId>F4C6D5BE-BF13-45*****6C-516EA8906DCD</RequestId>
  <TranscodeTask>
        <TranscodeJobInfoList>
              <TranscodeTemplateId>174b0534fea3*****b51c8f0ad1374</TranscodeTemplateId>
              <Priority>6</Priority>
              <InputFileUrl>http://outin-40564*****e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/5b95e568f8e*****47f38e/31f1184c-*****b2a2-f94-c213f.wmv</InputFileUrl>
              <Definition>LD</Definition>
              <CreationTime>2019-02-26T08:27:16Z</CreationTime>
              <TranscodeJobStatus>Transcoding</TranscodeJobStatus>
              <TranscodeJobId>38f0e513c88*****85515f9d50be188</TranscodeJobId>
              <ErrorCode>200</ErrorCode>
              <TranscodeProgress>100</TranscodeProgress>
              <ErrorMessage>ErrorMessage</ErrorMessage>
              <CompleteTime>2019-02-26T08:30:16Z</CompleteTime>
        </TranscodeJobInfoList>
        <TranscodeJobInfoList>
              <OutputFile>
                    <OutputFileUrl>http://outin-40564*****e1403e7.oss-cn-shanghai.aliyuncs.com/883f5d*****f20aaa352f/c3be4f073*****7d5193ec8-{DestMd5}-od-S00000001-200000.mp4</OutputFileUrl>
                    <Fps>25</Fps>
                    <VideoStreamList>[{\"AvgFPS\":\"30.0\",\"Bitrate\":\"933.814\",\"CodecLongName\":\"H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10\",\"CodecName\":\"h264\",\"CodecTag\":\"0x31637661\",\"CodecTagString\":\"avc1\",\"CodecTimeBase\":\"1/60\",\"Dar\":\"9:16\",\"Duration\":\"12.033333\",\"Fps\":\"30.0\",\"HasBFrames\":\"2\",\"Height\":\"360\",\"Index\":\"0\",\"Lang\":\"und\",\"Level\":\"30\",\"PixFmt\":\"yuv420p\",\"Profile\":\"High\",\"Sar\":\"81:256\",\"StartTime\":\"0.000000\",\"Timebase\":\"1/15360\",\"Width\":\"640\"}]</VideoStreamList>
                    <Duration>12</Duration>
                    <AudioStreamList>"AudioStreamList": "[{\"Bitrate\":\"64.533\",\"ChannelLayout\":\"stereo\",\"Channels\":\"2\",\"CodecLongName\":\"AAC (Advanced Audio Coding)\",\"CodecName\":\"aac\",\"CodecTag\":\"0x6134706d\",\"CodecTagString\":\"mp4a\",\"CodecTimeBase\":\"1/44100\",\"Duration\":\"12.615533\",\"Index\":\"1\",\"Lang\":\"und\",\"SampleFmt\":\"fltp\",\"Samplerate\":\"44100\",\"StartTime\":\"-0.046440\",\"Timebase\":\"1/44100\"}]</AudioStreamList>
                    <Encryption>{\"EncryptType\":\"AliyunVoDEncryption\"}</Encryption>
                    <Filesize>851076</Filesize>
                    <Bitrate>964</Bitrate>
                    <WatermarkIdList>["64079a0e3e286*****b48a8c9413"]</WatermarkIdList>
                    <Format>m3u8</Format>
                    <SubtitleStreamList>[]</SubtitleStreamList>
                    <Height>360</Height>
                    <Width>640</Width>
              </OutputFile>
        </TranscodeJobInfoList>
        <Trigger>Auto </Trigger>
        <VideoId>883f5d98107*****b7f20aaa352f</VideoId>
        <TranscodeTemplateGroupId>b500c7094bd241*****3e9900752d7c3</TranscodeTemplateGroupId>
        <CreationTime>2019-01-23T12:35:12Z</CreationTime>
        <TaskStatus>Processing</TaskStatus>
        <CompleteTime>2019-01-23T12:40:12Z</CompleteTime>
        <TranscodeTaskId>b1b65ab107e14*****3dbb900f6c1fe0</TranscodeTaskId>
  </TranscodeTask>
</GetTranscodeTaskResponse>
```

`JSON` format

```
{
	"RequestId": "F4C6D5BE-BF13-45*****6C-516EA8906DCD",
	"TranscodeTask": {
		"TranscodeJobInfoList": [{
			"TranscodeTemplateId": "174b0534fea3*****b51c8f0ad1374",
			"Priority": "6",
			"InputFileUrl": "http://outin-40564*****e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/5b95e568f8e*****47f38e/31f1184c-*****b2a2-f94-c213f.wmv",
			"Definition": "LD",
			"CreationTime": "2019-02-26T08:27:16Z",
			"TranscodeJobStatus": "Transcoding",
			"TranscodeJobId": "38f0e513c88*****85515f9d50be188",
			"ErrorCode": "200",
			"TranscodeProgress": "100",
			"ErrorMessage": "ErrorMessage",
			"CompleteTime": "2019-02-26T08:30:16Z"
		}, {
			"OutputFile": {
				"OutputFileUrl": "http://outin-40564*****e1403e7.oss-cn-shanghai.aliyuncs.com/883f5d*****f20aaa352f/c3be4f073*****7d5193ec8-{DestMd5}-od-S00000001-200000.mp4",
				"Fps": "25",
				"VideoStreamList": "[{\\\"AvgFPS\\\":\\\"30.0\\\",\\\"Bitrate\\\":\\\"933.814\\\",\\\"CodecLongName\\\":\\\"H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10\\\",\\\"CodecName\\\":\\\"h264\\\",\\\"CodecTag\\\":\\\"0x31637661\\\",\\\"CodecTagString\\\":\\\"avc1\\\",\\\"CodecTimeBase\\\":\\\"1/60\\\",\\\"Dar\\\":\\\"9:16\\\",\\\"Duration\\\":\\\"12.033333\\\",\\\"Fps\\\":\\\"30.0\\\",\\\"HasBFrames\\\":\\\"2\\\",\\\"Height\\\":\\\"360\\\",\\\"Index\\\":\\\"0\\\",\\\"Lang\\\":\\\"und\\\",\\\"Level\\\":\\\"30\\\",\\\"PixFmt\\\":\\\"yuv420p\\\",\\\"Profile\\\":\\\"High\\\",\\\"Sar\\\":\\\"81:256\\\",\\\"StartTime\\\":\\\"0.000000\\\",\\\"Timebase\\\":\\\"1/15360\\\",\\\"Width\\\":\\\"640\\\"}]",
				"Duration": "12",
				"AudioStreamList": "\"AudioStreamList\": \"[{\\\"Bitrate\\\":\\\"64.533\\\",\\\"ChannelLayout\\\":\\\"stereo\\\",\\\"Channels\\\":\\\"2\\\",\\\"CodecLongName\\\":\\\"AAC (Advanced Audio Coding)\\\",\\\"CodecName\\\":\\\"aac\\\",\\\"CodecTag\\\":\\\"0x6134706d\\\",\\\"CodecTagString\\\":\\\"mp4a\\\",\\\"CodecTimeBase\\\":\\\"1/44100\\\",\\\"Duration\\\":\\\"12.615533\\\",\\\"Index\\\":\\\"1\\\",\\\"Lang\\\":\\\"und\\\",\\\"SampleFmt\\\":\\\"fltp\\\",\\\"Samplerate\\\":\\\"44100\\\",\\\"StartTime\\\":\\\"-0.046440\\\",\\\"Timebase\\\":\\\"1/44100\\\"}]",
				"Encryption": "{\\\"EncryptType\\\":\\\"AliyunVoDEncryption\\\"}",
				"Filesize": "851076",
				"Bitrate": "964",
				"WatermarkIdList": "[\"64079a0e3e286*****b48a8c9413\"]",
				"Format": "m3u8",
				"SubtitleStreamList": "[]",
				"Height": "360",
				"Width": "640"
			}
		}],
		"Trigger": "Auto ",
		"VideoId": "883f5d98107*****b7f20aaa352f",
		"TranscodeTemplateGroupId": "b500c7094bd241*****3e9900752d7c3",
		"CreationTime": "2019-01-23T12:35:12Z",
		"TaskStatus": "Processing",
		"CompleteTime": "2019-01-23T12:40:12Z",
		"TranscodeTaskId": "b1b65ab107e14*****3dbb900f6c1fe0"
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
|NoSuchResource

|The specified resource %s does not exist.

|404

|The error message returned because the specified information does not exist. %s indicates the specified information. |

