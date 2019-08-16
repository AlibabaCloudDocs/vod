# GetTranscodeSummary {#doc_api_vod_GetTranscodeSummary .reference}

调用GetTranscodeSummary根据视频ID查询视频转码摘要，包括视频转码状态、转码进展等汇总信息。由于可能存在多次转码，故该接口只返回最近一次的转码摘要。

**说明：** 如要查询历史转码任务信息，可调用**ListTranscodeTask**接口。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetTranscodeSummary&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTranscodeSummary|系统规定参数，取值：**GetTranscodeSummary**。

 |
|VideoIds|String|是|"ddddddddd,ggggggg,hhhhhhh"|视频ID，多个用英文逗号分隔，最多支持10个。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NonExistVideoIds| |\["ggggggg","ddddddddd"\]|不存在的视频ID列表。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|TranscodeSummaryList| | |视频转码基础信息列表。

 |
|CompleteTime|String|2019-01-23T12:35:12Z|转码任务完成时间，UTC时间：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|CreationTime|String|2019-01-23T12:35:12Z|转码任务创建时间，UTC时间：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|TranscodeJobInfoSummaryList| | |转码作业摘要信息列表。

 |
|Bitrate|String|749|转码输出视频的平均码率，单位：kbps。

 |
|CompleteTime|String|2019-02-27T03:34:51Z|转码作业完成事件，UTC时间：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|CreationTime|String|2019-02-27T03:34:46Z|转码作业创建时间，UTC时间：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|Definition|String|LD|清晰度。

 **说明：** 该值为转码模板配置的清晰度标记，不表示转码输出文件实际的分辨率范围。

 |
|Duration|String|12|转码输出视频时长，单位：秒。

 |
|Encryption|String|\{\\"EncryptType\\":\\"AliyunVoDEncryption\\"\}|加密配置。

 |
|ErrorCode|String|200|转码失败的错误码。

 |
|ErrorMessage|String|ErrorMessage|转码失败的错误信息。

 |
|Filesize|Long|1144259|转码输出视频的文件大小，单位：Byte。

 |
|Format|String|mp4|转码输出视频的封装格式。

 |
|Fps|String|30|转码输出视频的帧率，单位：N帧/秒。

 |
|Height|String|960|转码输出视频的画面高，单位：px。

 |
|TranscodeJobStatus|String|Transcoding|转码作业状态。取值：

 -   **Transcoding**：转码中
-   **TranscodeSuccess**：转码成功
-   **TranscodeFail**：转码失败

 |
|TranscodeProgress|Long|100|转码进度，取值范围：`[0,100]`。

 |
|TranscodeTemplateId|String|0ff6d65db780ccc643434f38ff|使用的转码模板ID。

 |
|WatermarkIdList| |\["64079a0e3ea5c223b48a8c9413"\]|转码使用的水印列表。

 |
|Width|String|544|转码输出视频的画面宽，单位：px。

 |
|TranscodeStatus|String|Processing|转码处理状态。取值：

 -   **Processing**：处理中
-   **Partial**：部分转码完成
-   **CompleteAllSucc**：全部处理完成，且全部转码成功
-   **CompleteAllFail**：全部处理完成，且全部转码失败,如果源片有问题，则不会发起任何转码作业，整个转码任务失败
-   **CompletePartialSucc**：全部转码完成，但仅部分转码成功

 |
|TranscodeTemplateGroupId|String|uuuuuuuuuu|转码使用的模板组ID。

 |
|Trigger|String|Auto|触发类型。取值：

 -   Auto ：上传视频，自动触发。
-   Manual ：SubmitTranscodeJobs接口触发。

 |
|VideoId|String|hhhhhhhhh|视频ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetTranscodeSummary
&VideoIds="ddddddddd,ggggggg,hhhhhhh"
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetTranscodeSummaryResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <TranscodeSummaryList>
		    <VideoId>hhhhhhhhh</VideoId>
		    <TranscodeStatus>Processing</TranscodeStatus>
		    <TranscodeTemplateGroupId>uuuuuuuuuu</TranscodeTemplateGroupId>
		    <CreationTime>2019-01-23T12:35:12Z</CreationTime>
		    <CompleteTime>2019-01-23T12:35:12Z</CompleteTime>
		    <TranscodeJobInfoSummaryList>
			      <Format>mp4</Format>
			      <Encryption>{}</Encryption>
			      <TranscodeProgress>100</TranscodeProgress>
			      <Height>960</Height>
			      <CreationTime>2019-02-27T03:34:46Z</CreationTime>
			      <CompleteTime>2019-02-27T03:34:51Z</CompleteTime>
			      <TranscodeJobStatus>TranscodeSuccess</TranscodeJobStatus>
			      <Filesize>1144259</Filesize>
			      <WatermarkIdList>64079a0e3ea5c223b48a8c9413</WatermarkIdList>
			      <Duration>12</Duration>
			      <TranscodeTemplateId>0ff6d65db780ccc643434f38ff</TranscodeTemplateId>
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
			      <CompleteTime>2019-02-27T03:34:50Z</CompleteTime>
			      <TranscodeJobStatus>TranscodeSuccess</TranscodeJobStatus>
			      <Filesize>759520</Filesize>
			      <Duration>12</Duration>
			      <TranscodeTemplateId>fa0b39136499c54e9c63680ddcfd</TranscodeTemplateId>
			      <Width>360</Width>
			      <Fps>25</Fps>
			      <Bitrate>499</Bitrate>
			      <Definition>LD</Definition>
		    </TranscodeJobInfoSummaryList>
	  </TranscodeSummaryList>
	  <NonExistVideoIds>ggggggg</NonExistVideoIds>
	  <NonExistVideoIds>ddddddddd</NonExistVideoIds>
</GetTranscodeSummaryResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"NonExistVideoIds":[
		"ggggggg",
		"ddddddddd"
	],
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"TranscodeSummaryList":[
		{
			"CreationTime":"2019-01-23T12:35:12Z",
			"TranscodeTemplateGroupId":"uuuuuuuuuu",
			"VideoId":"hhhhhhhhh",
			"TranscodeJobInfoSummaryList":[
				{
					"Format":"mp4",
					"Encryption":"{}",
					"TranscodeProgress":100,
					"Height":"960",
					"CompleteTime":"2019-02-27T03:34:51Z",
					"CreationTime":"2019-02-27T03:34:46Z",
					"TranscodeJobStatus":"TranscodeSuccess",
					"Filesize":1144259,
					"WatermarkIdList":[
						"64079a0e3ea5c223b48a8c9413"
					],
					"Duration":"12",
					"TranscodeTemplateId":"0ff6d65db780ccc643434f38ff",
					"Width":"544",
					"Fps":"30",
					"Bitrate":"749",
					"Definition":"LD"
				},
				{
					"Format":"m3u8",
					"Encryption":"{\"EncryptType\":\"AliyunVoDEncryption\"}",
					"TranscodeProgress":100,
					"Height":"640",
					"CompleteTime":"2019-02-27T03:34:50Z",
					"CreationTime":"2019-02-27T03:34:46Z",
					"TranscodeJobStatus":"TranscodeSuccess",
					"Filesize":759520,
					"Duration":"12",
					"TranscodeTemplateId":"fa0b39136499c54e9c63680ddcfd",
					"Width":"360",
					"Fps":"25",
					"Bitrate":"499",
					"Definition":"LD"
				}
			],
			"TranscodeStatus":"Processing",
			"CompleteTime":"2019-01-23T12:35:12Z"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

