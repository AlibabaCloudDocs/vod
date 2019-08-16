# ListTranscodeTask {#doc_api_vod_ListTranscodeTask .reference}

调用ListTranscodeTask根据视频ID查询视频历史转码任务信息，该接口不返回具体的作业信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListTranscodeTask&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTranscodeTask|系统规定参数，取值：**ListTranscodeTask**。

 |
|VideoId|String|是|ddddddddd|视频ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|EndTime|String|否|2019-01-23T12:35:12Z|结束时间，UTC时间：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|PageNo|Integer|否|1|查询数据的当前页码，默认值为**1**。

 |
|PageSize|Integer|否|10|查询页数据大小，最大值为**50**，默认值为**10**。

 |
|StartTime|String|否|2019-01-23T12:35:12Z|开始时间，UTC时间：**yyyy-MM-ddTHH:mm:ssZ**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|TranscodeTaskList| | |转码处理信息列表。

 |
|CompleteTime|String|2019-01-23T12:35:12Z|转码任务完成时间，UTC时间：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|CreationTime|String|2019-01-23T12:35:12Z|转码任务创建时间，UTC时间：**yyyy-MM-ddTHH:mm:ssZ**。

 |
|TaskStatus|String|Processing|转码任务状态。

 -   **Processing**：处理中。
-   **Partial**：部分转码完成。
-   **CompleteAllSucc**：全部处理完成，且全部转码成功。
-   **CompleteAllFail**：全部处理完成，且全部转码失败，如果源片有问题，则不会发起任何转码作业，整个转码任务失败。
-   **CompletePartialSucc**：全部转码完成，但仅部分转码成功。

 |
|TranscodeTaskId|String|ddddddddddd|转码任务ID。

 |
|TranscodeTemplateGroupId|String|fffffff|转码使用的模板组ID。

 |
|Trigger|String|Auto|触发类型。取值：

 -   **Auto**：上传视频，自动触发。
-   **Manual**：SubmitTranscodeJobs接口触发。

 |
|VideoId|String|hhhhhhh|视频ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListTranscodeTask
&VideoId=ddddddddd
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListTranscodeTaskResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <TranscodeTaskList>
		    <TranscodeTaskId>ddddddddddd</TranscodeTaskId>
		    <VideoId>hhhhhhh</VideoId>
		    <TaskStatus>Processing</TaskStatus>
		    <TranscodeTemplateGroupId>fffffff</TranscodeTemplateGroupId>
		    <CreationTime>2019-01-23T12:35:12Z</CreationTime>
		    <CompleteTime>2019-01-23T12:35:12Z</CompleteTime>
	  </TranscodeTaskList>
	  <TranscodeTaskList>
		    <TranscodeTaskId>iiiiiiii</TranscodeTaskId>
		    <VideoId>tttttt</VideoId>
		    <TaskStatus>CompeleteAllSucc</TaskStatus>
		    <TranscodeTemplateGroupId>jjjjjjj</TranscodeTemplateGroupId>
		    <CreationTime>2019-01-23T12:35:12Z</CreationTime>
		    <CompleteTime>2019-01-23T12:35:12Z</CompleteTime>
	  </TranscodeTaskList>
</ListTranscodeTaskResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"TranscodeTaskList":[
		{
			"CreationTime":"2019-01-23T12:35:12Z",
			"TranscodeTemplateGroupId":"fffffff",
			"TranscodeTaskId":"ddddddddddd",
			"VideoId":"hhhhhhh",
			"TaskStatus":"Processing",
			"CompleteTime":"2019-01-23T12:35:12Z"
		},
		{
			"CreationTime":"2019-01-23T12:35:12Z",
			"TranscodeTemplateGroupId":"jjjjjjj",
			"TranscodeTaskId":"iiiiiiii",
			"VideoId":"tttttt",
			"TaskStatus":"CompeleteAllSucc",
			"CompleteTime":"2019-01-23T12:35:12Z"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

