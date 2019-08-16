# DeleteTranscodeTemplateGroup {#doc_api_vod_DeleteTranscodeTemplateGroup .reference}

调用DeleteTranscodeTemplateGroup删除转码配置信息，可删除转码模板组下的部分转码模板，也可强制删除整个转码模板组。

-   默认的转码模板，不允许删除，可取消其默认后再进行删除。
-   出于安全保护目的，被点播后台锁定的转码模板组不支持自定义操作，请通过工单或售后联系点播后台进行解锁或更改操作。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteTranscodeTemplateGroup&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteTranscodeTemplateGroup|系统规定参数，取值：**DeleteTranscodeTemplateGroup**。

 |
|TranscodeTemplateGroupId|String|是|4c71a339fecec0152b4fa6f4527xxx|转码模板组ID。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|ForceDelGroup|String|否|true|是否强制删除整个转码模板组。取值：

 -   **true**：删除整个模板组及其转码模板列表。
-   **false（默认）**：只删除指定的转码模板。

 |
|TranscodeTemplateIds|String|否|\["dddddd","ffffff"\]|需要删除的转码模板ID列表。ID以英文逗号分隔，最大支持10个模板ID。

 **说明：** **DeleteMode**取值**DeleteTranscodeTemplate**时，该参数必传。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NonExistTranscodeTemplateIds| |\["dddddd","ffffff"\]|根据转码模板ID列表删除转码模板时，不存在的转码模板ID列表。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DeleteTranscodeTemplateGroup
&TranscodeTemplateGroupId=4c71a339fecec0152b4fa6f4527xxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteTranscodeTemplateGroupResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <NonExistTranscodeTemplateIds>dddddd</NonExistTranscodeTemplateIds>
	  <NonExistTranscodeTemplateIds>ffffff</NonExistTranscodeTemplateIds>
</DeleteTranscodeTemplateGroupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"NonExistTranscodeTemplateIds":[
		"dddddd",
		"ffffff"
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

