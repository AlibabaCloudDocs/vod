# ListAIJob {#doc_api_vod_ListAIJob .reference}

调用ListAIJob查询AI作业。在提交AI作业后，会进行异步处理，通过此接口可以实时查询作业信息。

目前支持查询的作业类型：**AIMediaDNA**，**AIVideoTag**。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAIJob&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAIJob|系统规定参数，取值：**ListAIJob**。

 |
|JobIds|String|是|1236ca184c0e47098a5b665e2xxxxxx|作业ID列表。最多一次查10个，多个ID之间用逗号隔开。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AIJobList| | |作业信息列表。

 |
|Code|String|0|作业错误码。当Status为失败时，可关注该字段。

 |
|CompleteTime|String|2017-01-11T12:00:00Z|作业结束时间。

 |
|CreationTime|String|2017-01-11T12:00:00Z|作业开始时间。

 |
|Data|String|XXXXXXXXXXXXXXXXX|作业结果数据，Json数据格式。

 -   当Type值为AIMediaDNA时，关于Data的数据结构参见[AIMediaDNAResult](https://help.aliyun.com/document_detail/89863.html?spm=a2c4g.11186623.2.16.4831f79a1yZqcb#AIMediaDNAResult)。
-   当Type值为AIVideoTagResult时，关于Data的数据结构参见[AIVideoTagResult](https://help.aliyun.com/document_detail/89863.html?spm=a2c4g.11186623.2.17.4831f79a1yZqcb#AIVideoTagResult)。

 |
|JobId|String|1236ca184c0e47098a5b665e2xxxxxx|作业ID。

 |
|MediaId|String|3D3D12340d92c641401fab46a0b847xxxxxx|视频ID。

 |
|Message|String|OK|作业错误信息。当Status为失败时，可关注该字段。

 |
|Status|String|success|作业状态。取值：

 -   success\(成功\)
-   fail\(失败\)
-   init\(初始化\)
-   processing\(处理中\)

 |
|Type|String|AIMediaDNA|作业类型。

 |
|NonExistAIJobIds| |\{"String": \[\]\}|不存在的作业ID列表。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393xxxxxx|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListAIJob
&JobIds=1236ca184c0e47098a5b665e2xxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListAIJobResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393xxxxxx</RequestId>
	  <AIJobList>
		    <AIJob>
			      <JobId>1236ca184c0e47098a5b665e2xxxxxx</JobId>
			      <MediaId>3D3D12340d92c641401fab46a0b847xxxxxx</MediaId>
			      <Type>AIVideoTag</Type>
			      <CreationTime>2018-01-10T12:00:00Z</CreationTime>
			      <CompleteTime>2018-01-10T12:00:30Z</CompleteTime>
			      <Status>success</Status>
			      <Code>0</Code>
			      <Message>OK</Message>
			      <Data>XXXXXXXXXXXXXXXXX</Data>
		    </AIJob>
	  </AIJobList>
	  <NonExistAIJobIds></NonExistAIJobIds>
</ListAIJobResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"NonExistAIJobIds":{
		"String":[]
	},
	"RequestId":"25818875-5F78-4A13-BEF6-D7393xxxxxx",
	"AIJobList":{
		"AIJob":[
			{
				"CreationTime":"2018-01-10T12:00:00Z",
				"Data":"XXXXXXXXXXXXXXXXX",
				"Status":"success",
				"Message":"OK",
				"Type":"AIVideoTag",
				"JobId":"1236ca184c0e47098a5b665e2xxxxxx",
				"MediaId":"3D3D12340d92c641401fab46a0b847xxxxxx",
				"Code":"0",
				"CompleteTime":"2018-01-10T12:00:30Z"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

