# GetTranscodeTask {#doc_api_vod_GetTranscodeTask .reference}

调用GetTranscodeTask根据转码任务ID查询转码作业详细信息。

 **\_** 

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetTranscodeTask&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTranscodeTask|系统规定参数，取值：**GetTranscodeTask**。

 |
|TranscodeTaskId|String|是|ttttttt|转码任务ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|F4C6D5BE-BF13-4561-9F6C-516EA8906DCD|请求ID。

 |
|TranscodeTask| | |转码任务信息。

 |
|CompleteTime|String|019-01-23T12:35:12Z|转码任务完成时间。

 |
|CreationTime|String|019-01-23T12:35:12Z|转码任务创建时间。

 |
|TaskStatus|String|Processing|转码任务状态。

 |
|TranscodeJobInfoList| | |转码作业信息。

 |
|CompleteTime|String|2019-02-26T08:27:16Z|转码作业完成时间。

 |
|CreationTime|String|2019-02-26T08:27:16Z|转码作业创建时间。

 |
|Definition|String|LD|清晰度。

 **说明：** 该值为转码模板配置的清晰度标记，不表示转码输出文件实际的分辨率范围。

 |
|ErrorCode|String|200|转码失败错误码。

 |
|ErrorMessage|String|ErrorMessage|转码失败错误信息。

 |
|InputFileUrl|String|http://outin-40564284ef051d300163e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/d96a00e94e1e586af9bc1a1974ad/477e0344-16928ea4056-0003-b2a2-f94-c213f.mp4|转码源文件的OSS地址。

 |
|OutputFile| | |转码输出文件的信息。

 |
|AudioStreamList|String|"AudioStreamList": "\[\{\\"Bitrate\\":\\"64.533\\",\\"ChannelLayout\\":\\"stereo\\",\\"Channels\\":\\"2\\",\\"CodecLongName\\":\\"AAC \(Advanced Audio Coding\)\\",\\"CodecName\\":\\"aac\\",\\"CodecTag\\":\\"0x6134706d\\",\\"CodecTagString\\":\\"mp4a\\",\\"CodecTimeBase\\":\\"1/44100\\",\\"Duration\\":\\"12.615533\\",\\"Index\\":\\"1\\",\\"Lang\\":\\"und\\",\\"SampleFmt\\":\\"fltp\\",\\"Samplerate\\":\\"44100\\",\\"StartTime\\":\\"-0.046440\\",\\"Timebase\\":\\"1/44100\\"\}\]|音频流列表。

 |
|Bitrate|String|964|转码输出文件平均码率，单位：kbps。

 |
|Duration|String|12|转码输出文件时长，单位：秒。

 |
|Encryption|String|\{\\"EncryptType\\":\\"AliyunVoDEncryption\\"\}|转码输出文件使用的加密配置。

 |
|Filesize|Long|851076|转码输出文件大小，单位：Byte。

 |
|Format|String|m3u8|转码输出文件的封装格式。

 |
|Fps|String|25|转码输出文件的帧率，单位：N帧/秒。

 |
|Height|String|360|转码输出文件视频画面高，单位：px。

 |
|OutputFileUrl|String|http://outin-40564284ef0511e8b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/e1e63748f833a89b68552e54d5f7/94c4553de59a4615ab926c7e9105732a-83d70e6c4f6a871e004f924434e3-fd-encrypt-stream.m3u8|转码输出文件的OSS地址。

 |
|SubtitleStreamList|String|\[\]|字幕流列表。

 |
|VideoStreamList|String|\[\{\\"AvgFPS\\":\\"30.0\\",\\"Bitrate\\":\\"933.814\\",\\"CodecLongName\\":\\"H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10\\",\\"CodecName\\":\\"h264\\",\\"CodecTag\\":\\"0x31637661\\",\\"CodecTagString\\":\\"avc1\\",\\"CodecTimeBase\\":\\"1/60\\",\\"Dar\\":\\"9:16\\",\\"Duration\\":\\"12.033333\\",\\"Fps\\":\\"30.0\\",\\"HasBFrames\\":\\"2\\",\\"Height\\":\\"360\\",\\"Index\\":\\"0\\",\\"Lang\\":\\"und\\",\\"Level\\":\\"30\\",\\"PixFmt\\":\\"yuv420p\\",\\"Profile\\":\\"High\\",\\"Sar\\":\\"81:256\\",\\"StartTime\\":\\"0.000000\\",\\"Timebase\\":\\"1/15360\\",\\"Width\\":\\"640\\"\}\]|视频流列表。

 |
|WatermarkIdList| |\["64079a0e3e286d23b48a8c9413"\]|转码输出文件使用的水印ID列表。

 |
|Width|String|640|转码输出文件视频画面宽，单位：px。

 |
|Priority|String|6|转码任务优先级。

 |
|TranscodeJobId|String|ce8fbd628fb3a3001db739a51263|转码作业ID。

 |
|TranscodeJobStatus|String|Transcoding|转码作业状态。

 -   Transcoding\(转码中\)
-   TranscodeSuccess\(转码成功\)
-   TranscodeFail\(转码失败\)

 |
|TranscodeProgress|Long|100|转码作业处理进度，取值范围`[0,100]`。

 |
|TranscodeTemplateId|String|0ff6d65db7760ccc643434f38ff|转码使用的转码模板ID。

 |
|TranscodeTaskId|String|c3be4f073c3f4534893e7d5193ec8|转码任务ID。

 |
|TranscodeTemplateGroupId|String|5b95e56c688f8e04f70b70b47f38e|转码使用的模板组ID。

 |
|Trigger|String|Auto|触发类型。

 |
|VideoId|String|883f5d98107f403fab7f20aaa352f|视频ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetTranscodeTask
&TranscodeTaskId=ttttttt
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetTranscodeTaskResponse>
  <RequestId>F4C6D5BE-BF13-4561-9F6C-516EA8906DCD</RequestId>
	  <TranscodeTask>
		    <CreationTime>2019-01-23T12:35:12Z</CreationTime>
		    <TranscodeTemplateGroupId>5b95e56c688f8e04f70b70b47f38e</TranscodeTemplateGroupId>
		    <VideoId>883f5d98107f403fab7f20aaa352f</VideoId>
		    <TranscodeTaskId>c3be4f073c3f4534893e7d5193ec8</TranscodeTaskId>
		    <TaskStatus>CompleteAllSucc</TaskStatus>
		    <CompleteTime>2019-01-23T12:35:12Z</CompleteTime>
		    <TranscodeJobInfoList>
			      <InputFileUrl>http://outin-40564284ef0511e8b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/5b95e568f8e04f7c350b70b47f38e/31f1184c-1687ab4e899-0003-b2a2-f94-c213f.wmv</InputFileUrl>
			      <TranscodeJobStatus>TranscodeFail</TranscodeJobStatus>
			      <OutputFile>
				        <SubtitleStreamList>[]</SubtitleStreamList>
				        <AudioStreamList>[]</AudioStreamList>
				        <Filesize>0</Filesize>
				        <Duration>0</Duration>
				        <VideoStreamList>[]</VideoStreamList>
				        <Encryption>{}</Encryption>
				        <Height>0</Height>
				        <Width>0</Width>
				        <Fps>0</Fps>
				        <OutputFileUrl>http://outin-40564284ef0511e8b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/883f5d98107f403faa0ab7f20aaa352f/c3be4f073c3f4535b24893e7d5193ec8-{DestMd5}-od-S00000001-200000.mp4</OutputFileUrl>
				        <Bitrate>0</Bitrate>
			      </OutputFile>
			      <TranscodeJobId>e046ea644e8c983731f2f1061462</TranscodeJobId>
			      <TranscodeProgress>20</TranscodeProgress>
			      <Priority>6</Priority>
			      <FinishTime>2019-01-23T12:35:06Z</FinishTime>
			      <ErrorMessage>The resource operated InputFile is bad</ErrorMessage>
			      <TranscodeTemplateId>f5ab0194c1944eba374ea18665b3714d</TranscodeTemplateId>
			      <CreationTime>2019-01-23T12:35:05Z</CreationTime>
			      <ErrorCode>InvalidParameter.ResourceContentBad</ErrorCode>
			      <Definition>OD</Definition>
		    </TranscodeJobInfoList>
		    <TranscodeJobInfoList>
			      <CreationTime>2019-02-26T08:27:16Z</CreationTime>
			      <TranscodeJobStatus>TranscodeSuccess</TranscodeJobStatus>
			      <InputFileUrl>http://outin-40564284ef0511e8b2d3e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/d96a00e9486af05f69bc1a1974ad/477e0344-16928ea4056-0003-b2a2-f94-c213f.mp4</InputFileUrl>
			      <OutputFile>
				        <Format>m3u8</Format>
				        <Encryption>{"EncryptType":"AliyunVoDEncryption"}</Encryption>
				        <VideoStreamList>[{"AvgFPS":"25.0","Bitrate":"487.954","CodecLongName":"H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10","CodecName":"h264","CodecTag":"0x001b","CodecTagString":"[27][0][0][0]","CodecTimeBase":"1/50","Dar":"9:16","Duration":"12.080000","Fps":"25.0","HasBFrames":"2","Height":"360","Index":"0","Level":"30","PixFmt":"yuv420p","Profile":"High","Sar":"81:256","StartTime":"1.480000","Timebase":"1/90000","Width":"640"}]</VideoStreamList>
				        <Height>360</Height>
				        <SubtitleStreamList>[]</SubtitleStreamList>
				        <Filesize>851076</Filesize>
				        <AudioStreamList>[{"Bitrate":"62.015","ChannelLayout":"stereo","Channels":"2","CodecLongName":"AAC (Advanced Audio Coding)","CodecName":"aac","CodecTag":"0x000f","CodecTagString":"[15][0][0][0]","CodecTimeBase":"1/44100","Duration":"12.379978","Index":"1","SampleFmt":"fltp","Samplerate":"44100","StartTime":"1.433556","Timebase":"1/90000"}]</AudioStreamList>
				        <Duration>12</Duration>
				        <Width>640</Width>
				        <Fps>25</Fps>
				        <OutputFileUrl>http://outin-40564284ef0511e8b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/e1e63748f833a89b68552e54d5f7/94c4553de59a4615ab926c7e9105732a-83d70e6c4f6a871e004f924434e3-fd-encrypt-stream.m3u8</OutputFileUrl>
				        <Bitrate>549</Bitrate>
			      </OutputFile>
			      <TranscodeProgress>100</TranscodeProgress>
			      <TranscodeJobId>cbc090458ee87abd0e0dbd6871a39</TranscodeJobId>
			      <TranscodeTemplateId>fa0b39136499c5494c63680ddcfd</TranscodeTemplateId>
			      <Definition>LD</Definition>
			      <Priority>6</Priority>
			      <CompleteTime>2019-02-26T08:27:19Z</CompleteTime>
		    </TranscodeJobInfoList>
		    <TranscodeJobInfoList>
			      <CreationTime>2019-02-26T08:27:16Z</CreationTime>
			      <TranscodeJobStatus>TranscodeSuccess</TranscodeJobStatus>
			      <InputFileUrl>http://outin-40564284ef051d300163e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/d96a00e94e1e586af9bc1a1974ad/477e0344-16928ea4056-0003-b2a2-f94-c213f.mp4</InputFileUrl>
			      <OutputFile>
				        <Format>mp4</Format>
				        <Encryption>{}</Encryption>
				        <VideoStreamList>[{"AvgFPS":"30.0","Bitrate":"933.814","CodecLongName":"H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10","CodecName":"h264","CodecTag":"0x31637661","CodecTagString":"avc1","CodecTimeBase":"1/60","Dar":"9:16","Duration":"12.033333","Fps":"30.0","HasBFrames":"2","Height":"360","Index":"0","Lang":"und","Level":"30","PixFmt":"yuv420p","Profile":"High","Sar":"81:256","StartTime":"0.000000","Timebase":"1/15360","Width":"640"}]</VideoStreamList>
				        <Height>360</Height>
				        <Filesize>1520439</Filesize>
				        <AudioStreamList>[{"Bitrate":"64.533","ChannelLayout":"stereo","Channels":"2","CodecLongName":"AAC (Advanced Audio Coding)","CodecName":"aac","CodecTag":"0x6134706d","CodecTagString":"mp4a","CodecTimeBase":"1/44100","Duration":"12.615533","Index":"1","Lang":"und","SampleFmt":"fltp","Samplerate":"44100","StartTime":"-0.046440","Timebase":"1/44100"}]</AudioStreamList>
				        <WatermarkIdList>64079a0e3e286d23b48a8c9413</WatermarkIdList>
				        <Duration>12</Duration>
				        <Width>640</Width>
				        <Fps>30</Fps>
				        <OutputFileUrl>http://outin-40564284ef0511e8b2d3001603e7.oss-cn-shanghai.aliyuncs.com/e1e63748f8c3a89b68552e54d5f7/94c4553de59a4615ab926c7e9105732a-38a82b62eb175bd55ea4c3f560a2c-fd.mp4</OutputFileUrl>
				        <Bitrate>964</Bitrate>
			      </OutputFile>
			      <TranscodeProgress>100</TranscodeProgress>
			      <TranscodeJobId>ce8fbd628fb3a3001db739a51263</TranscodeJobId>
			      <TranscodeTemplateId>0ff6d65db7760ccc643434f38ff</TranscodeTemplateId>
			      <Definition>LD</Definition>
			      <Priority>6</Priority>
			      <CompleteTime>2019-02-26T08:27:20Z</CompleteTime>
		    </TranscodeJobInfoList>
	  </TranscodeTask>
</GetTranscodeTaskResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TranscodeTask":{
		"TranscodeJobInfoList":[
			{
				"CreationTime":"2019-01-23T12:35:05Z",
				"TranscodeJobStatus":"TranscodeFail",
				"ErrorMessage":"The resource operated InputFile is bad",
				"FinishTime":"2019-01-23T12:35:06Z",
				"InputFileUrl":"http://outin-40564284ef0511e8b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/5b95e568f8e04f7c350b70b47f38e/31f1184c-1687ab4e899-0003-b2a2-f94-c213f.wmv",
				"TranscodeProgress":20,
				"TranscodeJobId":"e046ea644e8c983731f2f1061462",
				"OutputFile":{
					"SubtitleStreamList":"[]",
					"Filesize":0,
					"AudioStreamList":"[]",
					"WatermarkIdList":[],
					"Duration":"0",
					"Encryption":"{}",
					"VideoStreamList":"[]",
					"Height":"0",
					"Width":"0",
					"Fps":"0",
					"OutputFileUrl":"http://outin-40564284ef0511e8b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/883f5d98107f403faa0ab7f20aaa352f/c3be4f073c3f4535b24893e7d5193ec8-{DestMd5}-od-S00000001-200000.mp4",
					"Bitrate":"0"
				},
				"TranscodeTemplateId":"f5ab0194c1944eba374ea18665b3714d",
				"ErrorCode":"InvalidParameter.ResourceContentBad",
				"Definition":"OD",
				"Priority":"6"
			},
			{
				"CreationTime":"2019-02-26T08:27:16Z",
				"TranscodeJobStatus":"TranscodeSuccess",
				"InputFileUrl":"http://outin-40564284ef0511e8b2d3e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/d96a00e9486af05f69bc1a1974ad/477e0344-16928ea4056-0003-b2a2-f94-c213f.mp4",
				"TranscodeJobId":"cbc090458ee87abd0e0dbd6871a39",
				"TranscodeProgress":100,
				"OutputFile":{
					"Format":"m3u8",
					"Encryption":"{\"EncryptType\":\"AliyunVoDEncryption\"}",
					"VideoStreamList":"[{\"AvgFPS\":\"25.0\",\"Bitrate\":\"487.954\",\"CodecLongName\":\"H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10\",\"CodecName\":\"h264\",\"CodecTag\":\"0x001b\",\"CodecTagString\":\"[27][0][0][0]\",\"CodecTimeBase\":\"1/50\",\"Dar\":\"9:16\",\"Duration\":\"12.080000\",\"Fps\":\"25.0\",\"HasBFrames\":\"2\",\"Height\":\"360\",\"Index\":\"0\",\"Level\":\"30\",\"PixFmt\":\"yuv420p\",\"Profile\":\"High\",\"Sar\":\"81:256\",\"StartTime\":\"1.480000\",\"Timebase\":\"1/90000\",\"Width\":\"640\"}]",
					"Height":"360",
					"SubtitleStreamList":"[]",
					"Filesize":851076,
					"AudioStreamList":"[{\"Bitrate\":\"62.015\",\"ChannelLayout\":\"stereo\",\"Channels\":\"2\",\"CodecLongName\":\"AAC (Advanced Audio Coding)\",\"CodecName\":\"aac\",\"CodecTag\":\"0x000f\",\"CodecTagString\":\"[15][0][0][0]\",\"CodecTimeBase\":\"1/44100\",\"Duration\":\"12.379978\",\"Index\":\"1\",\"SampleFmt\":\"fltp\",\"Samplerate\":\"44100\",\"StartTime\":\"1.433556\",\"Timebase\":\"1/90000\"}]",
					"WatermarkIdList":[],
					"Duration":"12",
					"Width":"640",
					"Fps":"25",
					"OutputFileUrl":"http://outin-40564284ef0511e8b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/e1e63748f833a89b68552e54d5f7/94c4553de59a4615ab926c7e9105732a-83d70e6c4f6a871e004f924434e3-fd-encrypt-stream.m3u8",
					"Bitrate":"549"
				},
				"TranscodeTemplateId":"fa0b39136499c5494c63680ddcfd",
				"CompleteTime":"2019-02-26T08:27:19Z",
				"Priority":"6",
				"Definition":"LD"
			},
			{
				"CreationTime":"2019-02-26T08:27:16Z",
				"TranscodeJobStatus":"TranscodeSuccess",
				"InputFileUrl":"http://outin-40564284ef051d300163e1403e7.oss-cn-shanghai.aliyuncs.com/customerTrans/d96a00e94e1e586af9bc1a1974ad/477e0344-16928ea4056-0003-b2a2-f94-c213f.mp4",
				"TranscodeJobId":"ce8fbd628fb3a3001db739a51263",
				"TranscodeProgress":100,
				"OutputFile":{
					"Format":"mp4",
					"AudioStreamList":"[{\"Bitrate\":\"64.533\",\"ChannelLayout\":\"stereo\",\"Channels\":\"2\",\"CodecLongName\":\"AAC (Advanced Audio Coding)\",\"CodecName\":\"aac\",\"CodecTag\":\"0x6134706d\",\"CodecTagString\":\"mp4a\",\"CodecTimeBase\":\"1/44100\",\"Duration\":\"12.615533\",\"Index\":\"1\",\"Lang\":\"und\",\"SampleFmt\":\"fltp\",\"Samplerate\":\"44100\",\"StartTime\":\"-0.046440\",\"Timebase\":\"1/44100\"}]",
					"Filesize":1520439,
					"WatermarkIdList":[
						"64079a0e3e286d23b48a8c9413"
					],
					"Duration":"12",
					"VideoStreamList":"[{\"AvgFPS\":\"30.0\",\"Bitrate\":\"933.814\",\"CodecLongName\":\"H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10\",\"CodecName\":\"h264\",\"CodecTag\":\"0x31637661\",\"CodecTagString\":\"avc1\",\"CodecTimeBase\":\"1/60\",\"Dar\":\"9:16\",\"Duration\":\"12.033333\",\"Fps\":\"30.0\",\"HasBFrames\":\"2\",\"Height\":\"360\",\"Index\":\"0\",\"Lang\":\"und\",\"Level\":\"30\",\"PixFmt\":\"yuv420p\",\"Profile\":\"High\",\"Sar\":\"81:256\",\"StartTime\":\"0.000000\",\"Timebase\":\"1/15360\",\"Width\":\"640\"}]",
					"Encryption":"{}",
					"Height":"360",
					"Width":"640",
					"Fps":"30",
					"OutputFileUrl":"http://outin-40564284ef0511e8b2d3001603e7.oss-cn-shanghai.aliyuncs.com/e1e63748f8c3a89b68552e54d5f7/94c4553de59a4615ab926c7e9105732a-38a82b62eb175bd55ea4c3f560a2c-fd.mp4",
					"Bitrate":"964"
				},
				"TranscodeTemplateId":"0ff6d65db7760ccc643434f38ff",
				"CompleteTime":"2019-02-26T08:27:20Z",
				"Priority":"6",
				"Definition":"LD"
			}
		],
		"CreationTime":"2019-01-23T12:35:12Z",
		"TranscodeTemplateGroupId":"5b95e56c688f8e04f70b70b47f38e",
		"TranscodeTaskId":"c3be4f073c3f4534893e7d5193ec8",
		"VideoId":"883f5d98107f403fab7f20aaa352f",
		"TaskStatus":"CompleteAllSucc",
		"CompleteTime":"2019-01-23T12:35:12Z"
	},
	"RequestId":"F4C6D5BE-BF13-4561-9F6C-516EA8906DCD"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

