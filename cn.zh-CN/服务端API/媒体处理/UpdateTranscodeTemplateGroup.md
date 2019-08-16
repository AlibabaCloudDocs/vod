# UpdateTranscodeTemplateGroup {#doc_api_vod_UpdateTranscodeTemplateGroup .reference}

调用UpdateTranscodeTemplateGroup修改转码配置信息，可修改转码模板组下指定的转码模板配置。

**说明：** 被点播后台**锁定**的转码模板组不支持自定义操作，请联系点播后台。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UpdateTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateTranscodeTemplateGroup|系统规定参数，取值：**UpdateTranscodeTemplateGroup**。

 |
|TranscodeTemplateGroupId|String|是|4c71a339fecec0152b4fa6f4527xxx|转码模板组ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|Locked|String|否|locked|指定的转码模板被锁定。

 |
|Name|String|否|transcodetemplate|转码模板组名称。长度不超过128个字节，UTF-8编码。

 |
|TranscodeTemplateList|String|否|\[\{"Video":\{"Bitrate":"400","Codec":"H.264","Fps":"30"\},"Audio":\{"Codec":"AAC","Bitrate":"64","Definition":"SD","EncryptType":"Private","Container":\{"Format":"m3u8"\},"PackageType":"HLSPackage"\}\}\]|转码模板配置信息\(JSON字符串\)。

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

http(s)://[Endpoint]/?Action=UpdateTranscodeTemplateGroup
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateTranscodeTemplateGroupResponse>
	    <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	    <TranscodeTemplateGroupId>34e908aa4024a9ae4df7821c31f93a2a</TranscodeTemplateGroupId>
</UpdateTranscodeTemplateGroupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TranscodeTemplateGroupId":"34e908aa4024a9ae4df78211f93a2a",
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

