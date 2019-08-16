# ListTranscodeTemplateGroup {#doc_api_vod_ListTranscodeTemplateGroup .reference}

调用ListTranscodeTemplateGroup查询转码模板配置列表。

**说明：** 该接口不会返回每个转码模板组下的转码模板配置信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTranscodeTemplateGroup|系统规定参数，取值：**ListTranscodeTemplateGroup**。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AppId|String|否|app-xxxxx|应用ID。取值如：**app-1000000**。

 |
|PageNo|Integer|否|1|当前页码。

 |
|PageSize|Integer|否|10|列表大小。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|TranscodeTemplateGroupList| | |转码模板组数据列表。

 |
|AppId|String|app-xxxxx|应用ID。

 |
|CreationTime|String|2018-12-05T10:20:09Z|模板组的创建时间。

 |
|IsDefault|String|Default|是否是默认模板组，取值：

 -   **Default**：默认模板组
-   **NotDefault**：非默认模板组

 |
|Locked|String|locked|转码模板被锁定。

 |
|ModifyTime|String|2018-12-05T10:20:09Z|模板组的修改时间。

 |
|Name|String|test|模板组的名称。

 |
|TranscodeMode|String|FastTranscode|转码模式。取值：

 -   **FastTranscode**：默认模式，上传完成即开始转码，且转码完成才能播放。
-   **NoTranscode**：不转码即分发。
-   **AsyncTranscode**：上传即分发并转码。

 |
|TranscodeTemplateGroupId|String|17a9889fc6685261a81d791c886700932|转码模板组ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListTranscodeTemplateGroup
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListTranscodeTemplateGroupResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <TranscodeTemplateGroupList>
		    <Name>test</Name>
		    <IsDefault>NotDefault</IsDefault>
		    <CreationTime>2018-12-05T10:20:09Z</CreationTime>
		    <ModifyTime>2018-12-05T10:20:09Z</ModifyTime>
		    <TranscodeTemplateGroupId>17a9889fc6685261a81d791c886700932</TranscodeTemplateGroupId>
	  </TranscodeTemplateGroupList>
	  <TranscodeTemplateGroupList>
		    <Name>transcode</Name>
		    <IsDefault>NotDefault</IsDefault>
		    <CreationTime>2018-12-05T10:20:09Z</CreationTime>
		    <ModifyTime>2018-12-05T10:20:09Z</ModifyTime>
		    <TranscodeTemplateGroupId>86e5a2a3c28a9299b8cbab7fe0882b1c9</TranscodeTemplateGroupId>
	  </TranscodeTemplateGroupList>
</ListTranscodeTemplateGroupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TranscodeTemplateGroupList":[
		{
			"CreationTime":"2018-12-05T10:20:09Z",
			"Name":"test",
			"TranscodeTemplateGroupId":"17a9889fc6685261a81d791c886700932",
			"IsDefault":"NotDefault",
			"ModifyTime":"2018-12-05T10:20:09Z"
		},
		{
			"CreationTime":"2018-12-05T10:20:09Z",
			"Name":"transcode",
			"TranscodeTemplateGroupId":"86e5a2a3c28a9299b8cbab7fe0882b1c9",
			"IsDefault":"NotDefault",
			"ModifyTime":"2018-12-05T10:20:09Z"
		}
	],
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

