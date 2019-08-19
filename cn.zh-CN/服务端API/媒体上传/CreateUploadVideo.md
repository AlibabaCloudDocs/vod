# CreateUploadVideo {#doc_api_vod_CreateUploadVideo .reference}

调用CreateUploadVideo获取视频上传地址和凭证，并创建视频信息。

此接口同时支持音频，使用说明参考[上传地址和凭证](https://help.aliyun.com/document_detail/55397.html?spm=a2c4g.11186623.2.16.23c4257eovDfWP)。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=CreateUploadVideo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateUploadVideo|系统规定参数，取值：**CreateUploadVideo**。

 |
|FileName|String|是|f26e9ddb-31f5-47cf-8c4f-f5a92b097334|视频源文件名。

 必须带扩展名，且扩展名不区分大小写。支持的扩展名参见[上传概述]()的限制部分。

 |
|Title|String|是|76f98aba-ab84-4f48-833a-07fe9bc2e316|视频标题。

 长度不超过128个字符或汉字，UTF8编码。

 |
|AppId|String|否|app-xxxxxx|应用ID。取值如：**app-1000000**。使用说明参考文档[多应用](https://help.aliyun.com/document_detail/113600.html?spm=a2c4g.11186623.2.22.23c4257eovDfWP)。

 |
|CateId|Long|否|67788823|视频分类ID。

 请在**点播控制台**\>**全局设置**\>**分类管理**中编辑或查看分类的ID。

 |
|CoverURL|String|否|f5c75b76-82a5-4562-aa42-339e0daf833b|自定义视频封面URL地址。

 |
|CustomMediaInfo|String|否|\{"aa":123\}|参数暂不可用。

 |
|Description|String|否|d192107b-4e80-46ae-a6e9-8995c2de7223|视频描述。

 长度不超过1024个字符或汉字，UTF8编码。

 |
|FileSize|Long|否|123|视频文件大小。单位：字节。

 |
|IP|String|否|127.0.0.1|参数暂不可用。

 |
|StorageLocation|String|否|out-xxxx.oss-cn-shanghai.aliyuncs.com|存储地址。

 当不为空时，会使用该指定的存储地址上传视频文件。可在**点播控制台** \> **存储管理**里查看存储地址。

 |
|Tags|String|否|tag1,tag2|视频标签。

 单个标签不超过32个字符或汉字，最多不超过16个标签。多个用逗号分隔，UTF8编码。

 |
|TemplateGroupId|String|否|405477f9e21e498eaa5cd19ea2c7c854|模板组ID。

 当不为空时，视频转码使用当前指定的模板组进行转码。可在控制台转码设置里查看模版组ID。

 |
|TranscodeMode|String|否|NoTranscode|参数暂不可用。

 |
|UserData|String|否|\{"MessageCallback":"\{"CallbackURL":"http://test.test.com"\}", "Extend":"\{"localId":"xxx", "test":"www"\}"\}|自定义设置，为JSON字符串，支持消息回调等设置。

 |
|WorkflowId|String|否|405477f9e21e498eaa5c-d19ea2c7c854|工作流ID。

 如果同时传递了WorkflowId和TemplateGroupId，以WorkflowId为准。使用说明参考文档[工作流](https://help.aliyun.com/document_detail/115347.html?spm=a2c4g.11186623.2.23.23c4257eJ1Qsl1)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|6544e9ea-0297-4d0f-9c4e-62923a2b0d34|请求ID。

 |
|VideoId|String|3841ee66-4b5e-4bdd-8d11-d70b436c0791|视频ID。

 |
|UploadAddress|String|7797a4bb-8fc0-4e4d-ba87-4992d1da546b|上传地址。

 |
|UploadAuth|String|6506ee8b-aff3-4a44-976e-d57de3d228ce|上传凭证。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=CreateUploadVideo
&FileName=f26e9ddb-31f5-47cf-8c4f-f5a92b097334
&Title=76f98aba-ab84-4f48-833a-07fe9bc2e316
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateUploadVideoResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
  <VideoId>93ab850b4f6f44eab54b6e91d24d81d4</VideoId>
  <UploadAddress>eyJTZWN1cml0eVRva2VuIjoiQ0FJU3p3TjF</UploadAddress>
  <UploadAuth>eyJFbmRwb2ludCI6Im</UploadAuth>
</CreateUploadVideoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"UploadAddress":"eyJTZWN1cml0eVRva2VuIjoiQ0FJU3p3TjF",
	"VideoId":"93ab850b4f6f44eab54b6e91d24d81d4",
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"UploadAuth":"eyJFbmRwb2ludCI6Im"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

