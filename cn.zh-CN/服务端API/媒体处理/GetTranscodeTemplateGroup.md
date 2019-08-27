# GetTranscodeTemplateGroup {#doc_api_vod_GetTranscodeTemplateGroup .reference}

调用GetTranscodeTemplateGroup根据转码模板组ID查询转码配置的详细信息。

**说明：** 获取单个模板组信息，同时会返回该模板组下所有转码模板的配置信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTranscodeTemplateGroup|系统规定参数，取值：**GetTranscodeTemplateGroup**。

 |
|TranscodeTemplateGroupId|String|是|a591f697c71676f73e6ae1502142d0|转码模板组ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|6730AC93-7B12-4BA8-857F-49EE1FE8BC49|请求ID。

 |
|TranscodeTemplateGroup| | |转码模板组数据。

 |
|AppId|String|app-xxxxx|应用ID。

 |
|CreationTime|String|2018-12-12T10:20:51Z|模板组的创建时间。

 |
|IsDefault|String|NotDefault|是否是默认模板组。取值：

 -   **Default**：默认模板组
-   **NotDefault**：非默认模板组

 |
|Locked|String|Enabled|模板组是否处理锁定状态

 |
|ModifyTime|String|2018-12-12T10:20:51Z|模板组的修改时间。

 |
|Name|String|test|模板组的名称。

 |
|TranscodeMode|String|FastTranscode|转码模式。

 |
|TranscodeTemplateGroupId|String|a59b11f697c71676f73e6ae1502142d0|转码模板组ID。

 |
|TranscodeTemplateList| | |转码模板配置信息列表。

 |
|Audio|String|\{\\"Codec\\":\\"AAC\\",\\"Remove\\":\\"false\\",\\"Bitrate\\":\\"44\\",\\"Samplerate\\":\\"32000\\",\\"Channels\\":\\"2\\",\\"Profile\\":\\"aac\_low\\"\}|音频流转码配置参数\(JSON字符串\)。

 |
|Clip|String|\{\\"TimeSpan\\":\{\\"Seek\\":\\"1\\",\\"Duration\\":\\"5\\"\}|视频裁剪配置\(JSON字符串\)，例如：需要截取视频中的5s内容，用于生成一个新的视频，则可设置该参数。

 |
|Container|String|"Format":"m3u8"|封装音视频码流的容器格式\(JSON字符串\)。

 |
|Definition|String|SD|普通转码模板清晰度标记：

 -   LD\(流畅\)
-   SD\(标清\)
-   HD\(高清\)
-   FHD\(超清\)
-   OD\(原画，即转封装\)
-   2K
-   4K
-   SQ\(普通音质\)
-   HQ\(高音质\)

 窄带高清1.0内置转码模板清晰度标记：

 -   LD-NBV1\(流畅\)
-   SD-NBV1\(标清\)
-   HD-NBV1\(高清\)
-   FHD-NBV1\(超清\)
-   2K-NBV1
-   4K-NBV1

 **说明：** 1. 所有转码模板不支持清晰度标记修改。

 2. 窄带高清1.0转码模板音视频分辨率、码率等参数为系统内置，不支持修改。

 3. 窄带高清1.0转码模板创建只支持FLV、M3U8\(HLS\)、MP4格式。

 |
|EncryptSetting|String|"EncryptType":"Private"|转码加密配置信息。

 |
|MuxConfig|String|"Segment": \{ "Duration":"6" \}|转码的分片设置参数，HLS必传\(JSON字符串\)。

 |
|OpeningList|String|\[\{"OpenUrl":"http://outin-test.oss-cn-shanghai.aliyuncs.com/tailslates/b6e9ceed-b665-426f-9d9a-277f0f85075b.mov"\}\]|开板素材OSS地址列表。

 |
|PackageSetting|String|"PackageType":"HLSPackage","PackageConfig":\{ "BandWidth":"900000" \}|打包配置，只支持HLS自适应码流打包、DASH打包 \(JSON字符串\)。

 |
|Rotate|String|90|视频旋转标参数，控制画面的旋转角度。例如：设置180，则视频画面将上下颠倒。取值范围：`[0,360]`。

 |
|SubtitleList|String|\[\{"SubtitleUrl":"http://outin-test.oss-cn-shanghai.aliyuncs.com/subtitles/c737fece-14f1-4364-b107-d5f7f8edde0e.ass","CharEncode":"utf-8"\}\]|字幕配置 \(JSON字符串\)。

 |
|TailSlateList|String|\[\{"TailUrl":"http://outin-test.oss-cn-shanghai.aliyuncs.com/tailslates/b6e9ceed-b665-426f-9d9a-277f0f85075b.mov"\}\]|尾板素材OSS地址列表

 |
|TemplateName|String|test|转码模板名称。

 |
|TransConfig|String|\{"IsCheckReso":"true","IsCheckResoFail":"false","IsCheckVideoBitrate":"false","IsCheckVideoBitrateFail":"false","IsCheckAudioBitrate":"false","IsCheckAudioBitrateFail":"false"\}|条件转码参数，如需要根据源片码率、分辨率进行基本逻辑判断再输出转码视频，则可设置该参数 \(JSON字符串\)。

 |
|TranscodeFileRegular|String|\{MediaId\}/transcoce\_1|自定义转码输出路径。

 |
|TranscodeTemplateId|String|696d29a11erc057f7d3a3acc398d02f4|转码模板ID。

 |
|Video|String|\{"Codec":"H.264","Bitrate":"900","Width":"960","Remove":"false","Fps":"30"\}|视频流转码配置参数\(JSON字符串\)。

 |
|WatermarkIds| |"USER\_DEFAULT\_WATERMARK","ddddddddd"|关联的水印ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetTranscodeTemplateGroup
&TranscodeTemplateGroupId=a591f697c71676f73e6ae1502142d0
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetTranscodeTemplateGroupResponse>
  <RequestId>6730AC93-7B12-4BA8-857F-49EE1FE8BC49</RequestId>
	  <TranscodeTemplateGroup>
		    <TranscodeTemplateGroupId>a59b11f697c71676f73e6ae1502142d0</TranscodeTemplateGroupId>
		    <Name>test</Name>
		    <CreationTime>2018-12-12T10:20:51Z</CreationTime>
		    <IsDefault>Default</IsDefault>
		    <ModifyTime>2018-12-12T13:02:32Z</ModifyTime>
		    <TranscodeTemplateList>
			      <TranscodeTemplateId>696d29a11erc057f7d3a3acc398d02f4</TranscodeTemplateId>
			      <TemplateName>111111</TemplateName>
			      <TransConfig>{"IsCheckAudioBitrate":"false","IsCheckAudioBitrateFail":"false","IsCheckVideoBitrateFail":"false","IsCheckReso":"false","IsCheckVideoBitrate":"false","IsCheckResoFail":"false"}</TransConfig>
			      <WatermarkIds>e0841e47d1551907ab32b50780df4431</WatermarkIds>
			      <WatermarkIds>dddd1e47d1551907ab32b50780df4431</WatermarkIds>
			      <Audio>{"Codec":"AAC","Remove":"false","Bitrate":"44","Samplerate":"32000","Channels":"2","Profile":"aac_low"}</Audio>
			      <Container>{"Format":"mp4"}</Container>
			      <Video>{"Bufsize":"6000","ScanMode":"progressive","Preset":"medium","Fps":"25","LongShortMode":"true","Gop":"250","Remove":"false","PixFmt":"yuv420p","Bitrate":"400","Profile":"high","Codec":"H.264","Maxrate":"700","Crf":"26","Width":"640"}</Video>
			      <Definition>LD</Definition>
		    </TranscodeTemplateList>
	  </TranscodeTemplateGroup>
</GetTranscodeTemplateGroupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TranscodeTemplateGroup":{
		"CreationTime":"2018-12-12T10:20:51Z",
		"Name":"test",
		"TranscodeTemplateGroupId":"a59b11f697c71676f73e6ae1502142d0",
		"TranscodeTemplateList":[
			{
				"TemplateName":"111111",
				"TransConfig":"{\"IsCheckAudioBitrate\":\"false\",\"IsCheckAudioBitrateFail\":\"false\",\"IsCheckVideoBitrateFail\":\"false\",\"IsCheckReso\":\"false\",\"IsCheckVideoBitrate\":\"false\",\"IsCheckResoFail\":\"false\"}",
				"TranscodeTemplateId":"696d29a11erc057f7d3a3acc398d02f4",
				"WatermarkIds":[
					"e0841e47d1551907ab32b50780df4431",
					"dddd1e47d1551907ab32b50780df4431"
				],
				"Audio":"{\"Codec\":\"AAC\",\"Remove\":\"false\",\"Bitrate\":\"44\",\"Samplerate\":\"32000\",\"Channels\":\"2\",\"Profile\":\"aac_low\"}",
				"Video":"{\"Bufsize\":\"6000\",\"ScanMode\":\"progressive\",\"Preset\":\"medium\",\"Fps\":\"25\",\"LongShortMode\":\"true\",\"Gop\":\"250\",\"Remove\":\"false\",\"PixFmt\":\"yuv420p\",\"Bitrate\":\"400\",\"Profile\":\"high\",\"Codec\":\"H.264\",\"Maxrate\":\"700\",\"Crf\":\"26\",\"Width\":\"640\"}",
				"Container":"{\"Format\":\"mp4\"}",
				"Definition":"LD"
			}
		],
		"IsDefault":"Default",
		"ModifyTime":"2018-12-12T13:02:32Z"
	},
	"RequestId":"6730AC93-7B12-4BA8-857F-49EE1FE8BC49"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

