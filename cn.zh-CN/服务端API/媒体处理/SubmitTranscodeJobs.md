# SubmitTranscodeJobs {#doc_api_vod_SubmitTranscodeJobs .reference}

调用SubmitTranscodeJobs提交媒体转码作业，开始异步转码处理。

**说明：** 

-   只有状态为**上传完成**、**正常** 和**审核中**的视频才能发起转码。
-   如需要获取转码结果，可接收回调消息：**单个清晰度转码完成、全部转码完成。**
-   该接口**不支持**HLS自适应码流打包、DASH打包。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SubmitTranscodeJobs&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SubmitTranscodeJobs|系统规定参数。取值：**SubmitTranscodeJobs**。

 |
|TemplateGroupId|String|是|56e680e618708fef7cefbf2cae7cc9yu|使用指定的模板组进行转码，可在[控制台转码设置](https://vod.console.aliyun.com/?spm=a2c4g.11186623.2.18.2f1a2267jCybwh#/vod/settings/transcode/vod)里查看模版组ID。

 |
|VideoId|String|是|d3e680e618708fef7cefbf2cae7cc931|视频ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|EncryptConfig|String|否|\{"CipherText":"ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMt", "DecryptKeyUri":"http://decrypt.demo.com?CipherText=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMt"\}|加密配置，为JSON字符串，只有使用HLS标准加密时才需要此参数。

 **说明：** 

-   **EncryptConfig**结构体中**CipherText**参数必须为通过[GenerateDataKey](https://help.aliyun.com/document_detail/28948.html?spm=a2c4g.11186623.2.21.2f1a2267jCybwh)生成的AES\_128密文秘钥，否则标准加密转码失败，标准加密接入流程请参阅[HLS标准加密](https://help.aliyun.com/document_detail/68612.html?spm=a2c4g.11186623.2.22.2f1a2267jCybwh)。
-   无论标准加密、私有加密，**TemplateGroupId**对应的模板数据，必须都勾选HLS加密选项，否则不加密。

 |
|OverrideParams|String|否|\{"Watermarks":\[\{"WatermarkId":"watermark1","FileUrl":"http://test.bucket.aliyuncs.com/image/replace.png"\},\{"WatermarkId":"watermark2","Content":"水印测试"\}\]\}|覆盖参数\(JSON字符串\)，支持对转码模板关联的指定图片水印文件、文字水印内容、字幕文件地址以及字幕文件编码格式的覆盖。

 |
|PipelineId|String|否|d3e680e618708fef7cefbf2cae7cc931|管道ID。

 |
|Priority|String|否|6|当前发起的转码作业在所有排队作业中的优先级。取值范围：`[1-10]`。最高优先级：**10**，默认值：**6**。

 **说明：** Priority参数只影响当前发起的转码作业在所有排队状态作业中的优先级，但不影响已经转码处理中的任务优先级。

 |
|UserData|String|否|\{"type":"vod"\}|用户自定义数据。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|TranscodeJobs| | |媒体作业信息。

 |
|JobId|String|ad90a501b1b94ba6afb72374ad005046|作业ID。

 |
|TranscodeTaskId|String|ad90a501b1b94ba6afb72374ad005046|当前提交的转码任务ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=SubmitTranscodeJobs
&TemplateGroupId=56e680e618708fef7cefbf2cae7cc9yu
&VideoId=d3e680e618708fef7cefbf2cae7cc931
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SubmitTranscodeJobsResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <TranscodeJobs>
		    <JobId>ad90a501b1b94ba6afb72374ad005046</JobId>
	  </TranscodeJobs>
</SubmitTranscodeJobsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"TranscodeJobs":[
		{
			"JobId":"ad90a501b1b94ba6afb72374ad005046"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

