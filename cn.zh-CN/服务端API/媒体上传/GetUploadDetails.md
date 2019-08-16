# GetUploadDetails {#doc_api_vod_GetUploadDetails .reference}

调用GetUploadDetails通过媒资ID（支持批量）获取媒资上传详情，如上传时间、已上传比例、上传来源等信息。

**说明：** 已上传比例等详细信息，只有使用点播控制台上传视频或指定版本（Java上传SDK1.4.4版本，C++上传SDK1.0.0版本，PHP上传SDK1.0.2版本，Python上传SDK1.3.0版本，Javascript上传SDK1.4.0版本，Android上传SDK1.5.0版本，iOS上传SDK1.5.0版本）及以上版本的上传SDK上传的视频才能获取到。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetUploadDetails&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetUploadDetails|系统规定参数。取值：**GetUploadDetails**。

 |
|MediaIds|String|是|media\_ids|媒资ID。

 目前仅支持视频ID。多个用英文逗号分隔，最多支持20个。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|MediaType|String|否|video|媒体类型。默认为**video**，取值：**video\(音视频\)**。

 |
|ResourceRealOwnerId|Long|否|5432684|资源所有者ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ForbiddenMediaIds| |gfhdttdk\*\*\*\*|禁止访问的媒体ID。

 |
|NonExistMediaIds| |dfsg\*\*\*\*|不存在的媒体ID。

 |
|RequestId|String|9E290613-04F4-4711-9CF4-795D30732077|请求ID。

 |
|UploadDetails| | |上传详情列表。

 |
|CompletionTime|String|2019-04-28T09:42:07Z|完成时间。

 |
|CreationTime|String|2019-04-28T09:42:07Z|创建时间。

 |
|DeviceModel|String|Chrome|设备模型。

 |
|FileSize|Long|46|文件大小。

 |
|MediaId|String|xxxxxxxxxx|上传视频ID。

 |
|ModificationTime|String|2019-04-28T09:43:12Z"|更新时间。

 |
|Status|String|Uploading|状态。

 |
|Title|String|测试文件上传详情|标题。

 |
|UploadIP|String|xx.xx.xx.xx|上传IP。

 |
|UploadRatio|Float|0.038|上传比率。

 |
|UploadSize|Long|346|上传大小。

 |
|UploadSource|String|WebSDK|上传资源。

 |
|UploadStatus|String|UPLOADING|上传状态。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetUploadDetails
&MediaIds=media_ids
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetUploadDetailsResponse>
	  <UploadDetails>
		    <Status>Uploading</Status>
		    <DeviceModel>Chrome...</DeviceModel>
		    <UploadSource>WebSDK</UploadSource>
		    <MediaId>xxxxxxxxxx</MediaId>
		    <UploadStatus>UPLOADING</UploadStatus>
		    <UploadSize>xxxxx</UploadSize>
		    <CreationTime>2019-04-28T09:42:07Z</CreationTime>
		    <Title>测试文件上传详情</Title>
		    <UploadIP>xx.xx.xx.xx</UploadIP>
		    <ModificationTime>2019-04-28T09:43:12Z</ModificationTime>
		    <UploadRatio>0.038</UploadRatio>
		    <FileSize>xxxxx</FileSize>
	  </UploadDetails>
	  <UploadDetails>
		    <DeviceModel>Chrome...</DeviceModel>
		    <Status>Normal</Status>
		    <Title>测试文件上传详情2</Title>
		    <ModificationTime>2019-05-06T09:21:36Z</ModificationTime>
		    <UploadRatio>1</UploadRatio>
		    <UploadSource>WebSDK</UploadSource>
		    <MediaId>xxxxxxxxxx</MediaId>
		    <CompletionTime>2019-05-06T09:21:36Z</CompletionTime>
		    <UploadStatus>UPLOAD_SUCCESS</UploadStatus>
		    <UploadSize>xxxxx</UploadSize>
		    <CreationTime>2019-05-06T09:21:32Z</CreationTime>
		    <UploadIP>xx.xx.xx.xx</UploadIP>
		    <FileSize>xxxxx</FileSize>
	  </UploadDetails>
	  <RequestId>9E290613-04F4-4711-9CF4-795D30732077</RequestId>
</GetUploadDetailsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"UploadDetails":[
		{
			"FileSize":"xxxxx",
			"CreationTime":"2019-04-28T09:42:07Z",
			"Status":"Uploading",
			"UploadRatio":0.038,
			"UploadIP":"xx.xx.xx.xx",
			"ModificationTime":"2019-04-28T09:43:12Z",
			"UploadStatus":"UPLOADING",
			"UploadSource":"WebSDK",
			"MediaId":"xxxxxxxxxx",
			"Title":"测试文件上传详情",
			"UploadSize":"xxxxx",
			"DeviceModel":"Chrome..."
		},
		{
			"UploadIP":"xx.xx.xx.xx",
			"ModificationTime":"2019-05-06T09:21:36Z",
			"CompletionTime":"2019-05-06T09:21:36Z",
			"UploadStatus":"UPLOAD_SUCCESS",
			"UploadSource":"WebSDK",
			"MediaId":"xxxxxxxxxx",
			"Title":"测试文件上传详情2",
			"UploadSize":"xxxxx",
			"DeviceModel":"Chrome...",
			"CreationTime":"2019-05-06T09:21:32Z",
			"FileSize":"xxxxx",
			"Status":"Normal",
			"UploadRatio":1.0
		}
	],
	"RequestId":"9E290613-04F4-4711-9CF4-795D30732077"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

