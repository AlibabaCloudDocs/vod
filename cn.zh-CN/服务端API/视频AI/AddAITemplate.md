# AddAITemplate {#doc_api_vod_AddAITemplate .reference}

调用AddAITemplate添加AI模板。

**说明：** 目前支持的AI模板类型仅为**AIMediaAudit（智能审核）**。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=AddAITemplate&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddAITemplate|系统规定参数，取值：**AddAITemplate**。

 |
|TemplateConfig|String|是|XXXXX|模板详细配置，JSON字符串，具体值详见[AITemplateConfig](https://help.aliyun.com/document_detail/89863.html?spm=a2c4g.11186623.2.15.286a5046RmMdjh#AITemplateConfig)。

 |
|TemplateName|String|是|AI-media-test|模板名称，最大128字节。

 |
|TemplateType|String|是|AIMediaAudit|模板类型，取值范围：**AIMediaAudit\(智能审核\)**。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-XXXXXXX|请求ID。

 |
|TemplateId|String|XXXXXXX|模板ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=AddAITemplate
&TemplateConfig=XXXXX
&TemplateName=AI-media-test
&TemplateType=AIMediaAudit
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddAITemplateResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-XXXXXXX</RequestId>
	  <TemplateId>XXXXXXX</TemplateId>
</AddAITemplateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-XXXXXXX",
	"TemplateId":"XXXXXXX"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

