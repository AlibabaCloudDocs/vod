# AddTranscodeTemplateGroup {#doc_api_vod_AddTranscodeTemplateGroup .reference}

调用AddTranscodeTemplateGroup添加转码配置信息，可创建新的转码模板组，或者向指定模板组中添加新的转码模板。

-   被点播后台**锁定**的转码模板组不支持自定义操作，请联系点播后台。
-   由于转码涉及到文件的存储地址，因此如果没有存储地址数据，暂不支持添加转码模板组。
-   不转码即分发转码模板组，不允许追加转码模板配置信息。
-   支持最多创建20个转码模板组。
-   单个转码模板组支持最多追加20个转码模板配置。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=AddTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddTranscodeTemplateGroup|系统规定参数，取值：**AddTranscodeTemplateGroup**。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AppId|String|否|app-xxxxx|应用ID。取值如：**app-1000000**。使用说明参考文档[多应用](https://help.aliyun.com/document_detail/113600.html?spm=a2c4g.11186623.2.17.33456d22HYxXg0)。

 |
|Name|String|否|transcodetemplate|转码模板组名称。长度不超过128个字节，UTF-8编码。

 **TranscodeTemplateGroupId**和**Name**必须传递一个。

 |
|TranscodeTemplateGroupId|String|否|4c71a339fecec0152b4fa6f4527xxx|转码模板组ID。

 |
|TranscodeTemplateList|String|否|\[\{"Video":\{"Bitrate":"400","Codec":"H.264","Fps":"30"\},"Audio":\{"Codec":"AAC","Bitrate":"64","Definition":"SD","EncryptType":"Private","Container":\{"Format":"m3u8"\},"PackageType":"HLSPackage"\}\}\]|转码模板配置信息\(JSON字符串\)。

 该参数不传递，则不会构建转码处理流程，视频上传不会触发转码。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|TranscodeTemplateGroupId|String|34e908aa4024a9ae4df7821c31f93a2a|转码模板组ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=AddTranscodeTemplateGroup
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddTranscodeTemplateGroupResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <TranscodeTemplateGroupId>34e908aa4024a9ae4df7821c31f93a2a</TranscodeTemplateGroupId>
</AddTranscodeTemplateGroupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TranscodeTemplateGroupId":"34e908aa4024a9ae4df7821c31f93a2a",
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

