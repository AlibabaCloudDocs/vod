# GetMediaDNAResult {#doc_api_vod_GetMediaDNAResult .reference}

调用GetMediaDNAResult获取视频DNA结果。视频DNA作业完成后，可通过此接口实时查询DNA结果。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetMediaDNAResult&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMediaDNAResult|系统规定参数，取值：**GetMediaDNAResult**。

 |
|MediaId|String|是|88c6ca184c0e47098a5b665e2a126797|视频ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DNAResult| | |DNA结果。

 |
|VideoDNA| | |视频DNA识别结果。

 |
|Detail| | |相似视频详情，包括视频的位置、时长等。

 |
|Duplication| | |库中视频的开始时间和时长。

 |
|Duration|String|12.0|视频的时长。

 |
|Start|String|2.0|视频的开始时间。

 |
|Input| | |输入视频的开始时间和时长。

 |
|Duration|String|12.0|视频的时长。

 |
|Start|String|2.0|视频的开始时间。

 |
|PrimaryKey|String|6ad8987da46f4b14b9d6490ce2873745|相似视频ID。

 |
|Similarity|String|0.98|视频相似度。

 |
|RequestId|String|63FC4896-E956-4B27-BF7D-134FF1BC597A|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetMediaDNAResult
&MediaId=88c6ca184c0e47098a5b665e2a126797
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetMediaDNAResultResponse>
	  <RequestId>63FC4896-E956-4B27-BF7D-134FF1BC597A</RequestId>
	  <DNAResult>
		    <VideoDNA>
			      <Similarity>0.98</Similarity>
			      <PrimaryKey>6ad8987da46f4b14b9d6490ce2873745</PrimaryKey>
			      <Detail>
				        <Input>
					          <Start>2.0</Start>
					          <Duration>12.0</Duration>
				        </Input>
				        <Duplication>
					          <Start>2.0</Start>
					          <Duration>12.1</Duration>
				        </Duplication>
			      </Detail>
		    </VideoDNA>
	  </DNAResult>
</GetMediaDNAResultResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DNAResult":{
		"VideoDNA":[
			{
				"Detail":[
					{
						"Input":{
							"Start":"2.0",
							"Duration":"12.0"
						},
						"Duplication":{
							"Start":"2.0",
							"Duration":"12.1"
						}
					}
				],
				"PrimaryKey":"6ad8987da46f4b14b9d6490ce2873745",
				"Similarity":"0.98"
			}
		]
	},
	"RequestId":"63FC4896-E956-4B27-BF7D-134FF1BC597A"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

