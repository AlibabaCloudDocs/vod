# GetTranscodeTemplateGroup

Queries the details of a transcoding template group based on the ID of the transcoding template group.

**Note:** This operation returns the information about the specified transcoding template group and the configurations of all the transcoding templates in the group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTranscodeTemplateGroup|The operation that you want to perform. Set the value to **GetTranscodeTemplateGroup**. |
|TranscodeTemplateGroupId|String|Yes|a591f697c7167\*\*\*\*\*6ae1502142d0|The ID of the transcoding template group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|6730AC93-7B12-4B\*\*\*\*\*7F-49EE1FE8BC49|The ID of the request. |
|TranscodeTemplateGroup|Struct| |The information about the transcoding template group. |
|AppId|String|app-\*\*\*\*|The ID of the application. |
|CreationTime|String|2018-12-12T10:20:51Z|The time when the template group was created. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|IsDefault|String|NotDefault|Indicates whether the template group is the default one. Valid values:

 -   **Default**: The template group is the default one.
-   **NotDefault**: The template group is not the default one. |
|Locked|String|Enabled|Indicates whether the template group is locked. Valid values:

 -   **Disabled**: The template group is not locked.
-   **Enabled**: The template group is locked. |
|ModifyTime|String|2018-12-12T11:20:51Z|The time when the template group was modified. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Name|String|test|The name of the template group. |
|TranscodeTemplateGroupId|String|a59b11f697c716\*\*\*\*\*6ae1502142d0|The ID of the transcoding template group. |
|TranscodeTemplateList|Array of TranscodeTemplate| |The configurations of the transcoding templates. |
|Audio|String|\{\\"Codec\\":\\"AAC\\",\\"Remove\\":\\"false\\",\\"Bitrate\\":\\"44\\",\\"Samplerate\\":\\"32000\\",\\"Channels\\":\\"2\\",\\"Profile\\":\\"aac\_low\\"\}|The transcoding configurations of the audio stream. The value is a JSON-formatted string. |
|Clip|String|\{\\"TimeSpan\\":\{\\"Seek\\":\\"1\\",\\"Duration\\":\\"5\\"\}|The clipping configurations of the video. The value is a JSON-formatted string. For example, you can set this parameter if you want to extract 5 seconds of content from a video to generate a new video. |
|Container|String|"Format":"m3u8"|The format of the container used to encapsulate audio and video streams. The value is a JSON-formatted string. |
|Definition|String|SD|Valid values for the definition of a common transcoding template:

 -   **LD**: low definition.
-   **SD**: standard definition.
-   **HD**: high definition.
-   **FHD**: ultra high definition.
-   **OD**: original quality.
-   **2K**
-   **4K**
-   **SQ**: standard sound quality.
-   **HQ**: high sound quality.

 Valid values for the definition of a Narrowband HD™ 1.0 transcoding template:

 -   **LD-NBV1**: low definition.
-   **SD-NBV1**: standard definition.
-   **HD-NBV1**: high definition.
-   **FHD-NBV1**: ultra high definition.
-   **2K-NBV1**
-   **4K-NBV1**

 **Note:**

-   You cannot modify the definition of transcoding templates.
-   You cannot modify the system parameters, such as the video resolution, audio resolution, and bitrate, of Narrowband HD™ 1.0 transcoding templates.
-   You can create only Narrowband HD™ 1.0 transcoding templates that support the FLV, M3U8 \(HLS\), and MP4 output formats. |
|EncryptSetting|String|"EncryptType":"Private"|The encryption configuration used for transcoding. |
|MuxConfig|String|"Segment": \{ "Duration":"6" \}|The transcoding segment configurations. This parameter must be returned if HTTP-Live-Streaming \(HLS\) encryption is used. The value is a JSON-formatted string. |
|PackageSetting|String|"PackageType":"HLSPackage","PackageConfig":\{ "BandWidth":"900000" \}|The packaging configurations. Only HLS packaging and DASH packaging are supported. The value is a JSON-formatted string. |
|Rotate|String|90|The video rotation identifier. It is used to control the image rotation angle. For example, if you set this parameter to 180, the video image is turned upside down. Valid values: `0 to 360`. |
|SubtitleList|String|\[\{"SubtitleUrl":"http://outin-test.oss-cn-shanghai.aliyuncs.com/subtitles/c737fece-14f1-4364-b107-d5f7f8edde0e.ass","CharEncode":"utf-8"\}\]|The subtitle configurations. The value is a JSON-formatted string. |
|TemplateName|String|test|The name of the transcoding template. |
|TransConfig|String|\{"IsCheckReso":"true","IsCheckResoFail":"false","IsCheckVideoBitrate":"false","IsCheckVideoBitrateFail":"false","IsCheckAudioBitrate":"false","IsCheckAudioBitrateFail":"false"\}|The conditional transcoding configurations. This parameter can be used if you want to determine the basic logic based on the bitrate and resolution of the mezzanine file before the video is transcoded. The value is a JSON-formatted string. |
|TranscodeFileRegular|String|\{MediaId\}/transcoce\_1|The custom output path of transcoded files. |
|TranscodeTemplateId|String|696d29a11erc057\*\*\*\*\*a3acc398d02f4|The ID of the transcoding template. |
|Type|String|Normal|The type of the template. Valid values:

 -   **Normal**: a common transcoding template. This is the default value. The PackageSetting parameter cannot be set for this type of template.
-   **VideoPackage**: a video stream package template. If this type of template is used, ApsaraVideo VOD transcodes a video into video streams in different bitrates and packages these video streams with a file. The PackageSetting parameter must be set for this type of template.
-   **SubtitlePackage**: a subtitle package template. If this type of template is used, ApsaraVideo VOD adds the subtitle information to the output file generated by packaging the multi-bitrate video streams of the corresponding video. You must set the PackageSetting parameter for a subtitle package template and associate the subtitle package template with a video stream package template. A template group can contain only one subtitle package template. |
|Video|String|\{"Codec":"H.264","Bitrate":"900","Width":"960","Remove":"false","Fps":"30"\}|The transcoding configurations of the video stream. The value is a JSON-formatted string. |
|WatermarkIds|List|"USER\_DEFAULT\_WATERMARK","ddddddddd"|The ID of the associated watermark. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetTranscodeTemplateGroup
&TranscodeTemplateGroupId=a591f697c7167*****6ae1502142d0
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetTranscodeTemplateGroupResponse>
  <RequestId>6730AC93-7B12-4B*****7F-49EE1FE8BC49</RequestId>
  <TranscodeTemplateGroup>
        <IsDefault>NotDefault</IsDefault>
        <Locked>Enabled</Locked>
        <ModifyTime>2018-12-12T11:20:51Z</ModifyTime>
        <AppId>app-****</AppId>
        <TranscodeTemplateGroupId>a59b11f697c716*****6ae1502142d0</TranscodeTemplateGroupId>
        <TranscodeMode>FastTranscode</TranscodeMode>
        <TranscodeTemplateList>
              <TailSlateList>[{"TailUrl":"http://outin-test.oss-cn-shanghai.aliyuncs.com/tailslates/b6e9ceed-b665-426f-9d9a-277f0f****.mov"}]</TailSlateList>
              <PackageSetting>"PackageType":"HLSPackage","PackageConfig":{   "BandWidth":"900000"  }</PackageSetting>
              <Rotate>90</Rotate>
              <UserData>{}</UserData>
              <Definition>SD</Definition>
              <TranscodeFileRegular>{MediaId}/transcoce_1</TranscodeFileRegular>
              <EncryptSetting>"EncryptType":"Private"</EncryptSetting>
              <Clip>{\"TimeSpan\":{\"Seek\":\"1\",\"Duration\":\"5\"}</Clip>
              <Type>Normal</Type>
              <Container>"Format":"m3u8"</Container>
              <TranscodeTemplateId>696d29a11erc057*****a3acc398d02f4</TranscodeTemplateId>
              <TransConfig>{"IsCheckReso":"true","IsCheckResoFail":"false","IsCheckVideoBitrate":"false","IsCheckVideoBitrateFail":"false","IsCheckAudioBitrate":"false","IsCheckAudioBitrateFail":"false"}</TransConfig>
              <Video>{"Codec":"H.264","Bitrate":"900","Width":"960","Remove":"false","Fps":"30"}</Video>
              <TemplateName>test</TemplateName>
              <SubtitleList>[{"SubtitleUrl":"http://outin-test.oss-cn-shanghai.aliyuncs.com/subtitles/c737fece-14f1-4364-b107-d5f7f8edde0e.ass","CharEncode":"utf-8"}]</SubtitleList>
              <Audio>{\"Codec\":\"AAC\",\"Remove\":\"false\",\"Bitrate\":\"44\",\"Samplerate\":\"32000\",\"Channels\":\"2\",\"Profile\":\"aac_low\"}</Audio>
              <MuxConfig>"Segment": { "Duration":"6" }</MuxConfig>
              <OpeningList>[{"OpenUrl":"http://outin-test.oss-cn-shanghai.aliyuncs.com/tailslates/b6e9ceed-b665-426f-9d9a-277f0f****.mov"}]</OpeningList>
        </TranscodeTemplateList>
        <TranscodeTemplateList>
              <WatermarkIds>"USER_DEFAULT_WATERMARK","ddddddddd"</WatermarkIds>
        </TranscodeTemplateList>
        <CreationTime>2018-12-12T10:20:51Z</CreationTime>
        <Name>test</Name>
  </TranscodeTemplateGroup>
</GetTranscodeTemplateGroupResponse>
```

`JSON` format

```
{
	"RequestId": "6730AC93-7B12-4B*****7F-49EE1FE8BC49",
	"TranscodeTemplateGroup": {
		"IsDefault": "NotDefault",
		"Locked": "Enabled",
		"ModifyTime": "2018-12-12T11:20:51Z",
		"AppId": "app-****",
		"TranscodeTemplateGroupId": "a59b11f697c716*****6ae1502142d0",
		"TranscodeMode": "FastTranscode",
		"TranscodeTemplateList": [{
			"TailSlateList": "[{\"TailUrl\":\"http://outin-test.oss-cn-shanghai.aliyuncs.com/tailslates/b6e9ceed-b665-426f-9d9a-277f0f****.mov\"}]",
			"PackageSetting": "\"PackageType\":\"HLSPackage\",\"PackageConfig\":{   \"BandWidth\":\"900000\"  }",
			"Rotate": "90",
			"UserData": "{}",
			"Definition": "SD",
			"TranscodeFileRegular": "{MediaId}/transcoce_1",
			"EncryptSetting": "\"EncryptType\":\"Private\"",
			"Clip": "{\\\"TimeSpan\\\":{\\\"Seek\\\":\\\"1\\\",\\\"Duration\\\":\\\"5\\\"}",
			"Type": "Normal",
			"Container": "\"Format\":\"m3u8\"",
			"TranscodeTemplateId": "696d29a11erc057*****a3acc398d02f4",
			"TransConfig": "{\"IsCheckReso\":\"true\",\"IsCheckResoFail\":\"false\",\"IsCheckVideoBitrate\":\"false\",\"IsCheckVideoBitrateFail\":\"false\",\"IsCheckAudioBitrate\":\"false\",\"IsCheckAudioBitrateFail\":\"false\"}",
			"Video": "{\"Codec\":\"H.264\",\"Bitrate\":\"900\",\"Width\":\"960\",\"Remove\":\"false\",\"Fps\":\"30\"}",
			"TemplateName": "test",
			"SubtitleList": "[{\"SubtitleUrl\":\"http://outin-test.oss-cn-shanghai.aliyuncs.com/subtitles/c737fece-14f1-4364-b107-d5f7f8edde0e.ass\",\"CharEncode\":\"utf-8\"}]",
			"Audio": "{\\\"Codec\\\":\\\"AAC\\\",\\\"Remove\\\":\\\"false\\\",\\\"Bitrate\\\":\\\"44\\\",\\\"Samplerate\\\":\\\"32000\\\",\\\"Channels\\\":\\\"2\\\",\\\"Profile\\\":\\\"aac_low\\\"}",
			"MuxConfig": "\"Segment\": { \"Duration\":\"6\" }",
			"OpeningList": "[{\"OpenUrl\":\"http://outin-test.oss-cn-shanghai.aliyuncs.com/tailslates/b6e9ceed-b665-426f-9d9a-277f0f****.mov\"}]"
		}, {
			"WatermarkIds": "\"USER_DEFAULT_WATERMARK\",\"ddddddddd\""
		}],
		"CreationTime": "2018-12-12T10:20:51Z",
		"Name": "test"
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
|InvalidTranscodeTemplateGroup.NotFound

|The transcode template group does not exist.

|404

|The error message returned because the specified transcoding template group does not exist. |

## SDK examples

We recommend that you use [server SDKs](~~101789~~) to call this operation. You can view the sample code of different languages to call this operation by clicking the following links:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

