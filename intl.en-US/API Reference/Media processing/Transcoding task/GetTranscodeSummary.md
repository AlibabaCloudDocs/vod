# GetTranscodeSummary

Queries the transcoding summary of one or more videos based on the video ID. The transcoding summary includes the transcoding status and transcoding progress. A video may be transcoded for multiple times. This operation returns only the latest transcoding summary.

**Note:** You can call the [ListTranscodeTask](~~109120~~) operation to query historical transcoding tasks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetTranscodeSummary&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTranscodeSummary|The operation that you want to perform. Set the value to **GetTranscodeSummary**. |
|VideoIds|String|Yes|"d4860fcc6a\*\*\*\*\*e9fed52e893824,e1db68cc58664\*\*\*\*\*4b83e562bcd9,hhhhhhh"|The ID of the video. Separate multiple IDs with commas \(,\). You can query the transcoding summary of up to 10 videos at a time. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NonExistVideoIds|List|\["hhhhhhh"\]|The IDs of videos that were not found. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |
|TranscodeSummaryList|Array of TranscodeSummary| |The transcoding summary of the video. |
|CompleteTime|String|2019-01-23T12:40:12Z|The time when the transcoding task was complete. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CreationTime|String|2019-01-23T12:35:12Z|The time when the transcoding task was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|TranscodeJobInfoSummaryList|Array of TranscodeJobInfoSummary| |The summaries of transcoding jobs. |
|Bitrate|String|749|The average bitrate of the output video. Unit: Kbit/s. |
|CompleteTime|String|2019-02-27T03:40:51Z|The time when the transcoding job was complete. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|CreationTime|String|2019-02-27T03:34:46Z|The time when the transcoding job was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Duration|String|12|The duration of the output video. Unit: seconds. |
|ErrorCode|String|200|The error code returned when the transcoding job fails. |
|ErrorMessage|String|ErrorMessage|The error message returned when the transcoding job fails. |
|Filesize|Long|1144259|The size of the output video. Unit: byte. |
|Format|String|mp4|The encapsulation format of the output video. |
|Fps|String|30|The frame rate of the output video. Unit: frames per second. |
|Height|String|960|The height of the output video. Unit: px. |
|TranscodeJobStatus|String|Transcoding|The status of the transcoding job. Valid values:

 -   **Transcoding**: The transcoding job is running.
-   **TranscodeSuccess**: The transcoding job was successful.
-   **TranscodeFail**: The transcoding job failed. |
|TranscodeProgress|Long|100|The progress of the transcoding job. Valid values: `0 to 100`. |
|TranscodeTemplateId|String|57496724ae2\*\*\*\*\*0968d6e08acc8f6|The ID of the transcoding template. |
|WatermarkIdList|List|\["af2afe4761992c\*\*\*\*\*d947dae97337"\]|The watermarks used for transcoding. |
|Width|String|544|The width of the output video. Unit: px. |
|TranscodeStatus|String|Processing|The transcoding status. Valid values:

 -   **Processing**: The transcoding is in progress.
-   **Partial**: The video was partially transcoded.
-   **CompleteAllSucc**: All the transcoding jobs were complete and the video was fully transcoded.
-   **CompleteAllFail**: All the transcoding jobs were complete but the video failed to be transcoded. If an exception occurs in the mezzanine file, no transcoding job is initiated and the transcoding task fails.
-   **CompletePartialSucc**: All the transcoding jobs were complete but the video was partially transcoded. |
|TranscodeTemplateGroupId|String|44f9e406bbb\*\*\*\*\*736a9abe876ecc0|The ID of the transcoding template group. |
|VideoId|String|e1db68cc58664\*\*\*\*\*4b83e562bcd9|The ID of the video. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetTranscodeSummary
&VideoIds="d4860fcc6a*****e9fed52e893824,e1db68cc58664*****4b83e562bcd9,hhhhhhh"
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetTranscodeSummaryResponse>
  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <TranscodeSummaryList>
		    <VideoId>e1db68cc58664*****4b83e562bcd9</VideoId>
		    <TranscodeStatus>Processing</TranscodeStatus>
		    <TranscodeTemplateGroupId>44f9e406bbb*****736a9abe876ecc0</TranscodeTemplateGroupId>
		    <CreationTime>2019-01-23T12:35:12Z</CreationTime>
		    <CompleteTime>2019-01-23T12:40:12Z</CompleteTime>
		    <TranscodeJobInfoSummaryList>
			      <Format>mp4</Format>
			      <Encryption>{}</Encryption>
			      <TranscodeProgress>100</TranscodeProgress>
			      <Height>960</Height>
			      <CreationTime>2019-02-27T03:34:46Z</CreationTime>
			      <CompleteTime>2019-02-27T03:40:51Z</CompleteTime>
			      <TranscodeJobStatus>TranscodeSuccess</TranscodeJobStatus>
			      <Filesize>1144259</Filesize>
			      <WatermarkIdList>af2afe4761992c*****d947dae97337</WatermarkIdList>
			      <Duration>12</Duration>
			      <TranscodeTemplateId>57496724ae2*****0968d6e08acc8f6</TranscodeTemplateId>
			      <Width>544</Width>
			      <Fps>30</Fps>
			      <Bitrate>749</Bitrate>
			      <Definition>LD</Definition>
		    </TranscodeJobInfoSummaryList>
		    <TranscodeJobInfoSummaryList>
			      <Format>m3u8</Format>
			      <Encryption>{"EncryptType":"AliyunVoDEncryption"}</Encryption>
			      <TranscodeProgress>100</TranscodeProgress>
			      <Height>640</Height>
			      <CreationTime>2019-02-27T03:34:46Z</CreationTime>
			      <CompleteTime>2019-02-27T03:40:50Z</CompleteTime>
			      <TranscodeJobStatus>TranscodeSuccess</TranscodeJobStatus>
			      <Filesize>759520</Filesize>
			      <Duration>12</Duration>
			      <TranscodeTemplateId>4733b3a55b27*****82dae36ac22d34</TranscodeTemplateId>
			      <Width>360</Width>
			      <Fps>25</Fps>
			      <Bitrate>499</Bitrate>
			      <Definition>LD</Definition>
		    </TranscodeJobInfoSummaryList>
	  </TranscodeSummaryList>
	  <NonExistVideoIds>hhhhhhh</NonExistVideoIds>
</GetTranscodeSummaryResponse>
```

`JSON` format

```
{
  "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
  "TranscodeSummaryList":[
    {
      "VideoId":"e1db68cc58664*****4b83e562bcd9",
      "TranscodeStatus":"Processing",
      "TranscodeTemplateGroupId":"44f9e406bbb*****736a9abe876ecc0",
      "CreationTime":"2019-01-23T12:35:12Z",
      "CompleteTime":"2019-01-23T12:40:12Z",
      "TranscodeJobInfoSummaryList": [
        {
          "Format": "mp4",
          "Encryption": "{}",
          "TranscodeProgress": 100,
          "Height": "960",
          "CreationTime": "2019-02-27T03:34:46Z",
          "CompleteTime": "2019-02-27T03:40:51Z",  
          "TranscodeJobStatus": "TranscodeSuccess",
          "Filesize": 1144259,
          "WatermarkIdList": [
            "af2afe4761992c*****d947dae97337"
          ],
          "Duration": "12",
          "TranscodeTemplateId": "57496724ae2*****0968d6e08acc8f6",
          "Width": "544",
          "Fps": "30",
          "Bitrate": "749",
          "Definition": "LD"
        },
        {
          "Format": "m3u8",
          "Encryption": "{\"EncryptType\":\"AliyunVoDEncryption\"}",
          "TranscodeProgress": 100,
          "Height": "640",
          "CreationTime": "2019-02-27T03:34:46Z",
          "CompleteTime": "2019-02-27T03:40:50Z",
          "TranscodeJobStatus": "TranscodeSuccess",
          "Filesize": 759520,
          "Duration": "12",
          "TranscodeTemplateId": "4733b3a55b27*****82dae36ac22d34",
          "Width": "360",
          "Fps": "25",
          "Bitrate": "499",
          "Definition": "LD"
        }
  ]
}],
  "NonExistVideoIds":["hhhhhhh"]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

