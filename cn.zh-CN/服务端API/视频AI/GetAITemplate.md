# GetAITemplate {#doc_api_vod_GetAITemplate .reference}

调用GetAITemplate查询AI模板。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetAITemplate&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetAITemplate|系统规定参数，取值：**GetAITemplate**。

 |
|TemplateId|String|是|XXXXX|模板ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|E9790EC4-DDC4-4EF1-8EB0-XXXXXX|请求ID。

 |
|TemplateInfo| | |AI模板信息。

 |
|CreationTime|String|2018-12-12T15:09:38:894Z|创建时间，UTC格式。

 |
|IsDefault|String|Default|是否默认。取值：**Default**\(是\)，**NotDefault**\(否\)。

 |
|ModifyTime|String|2018-12-12T15:09:38:894Z|修改时间，UTC格式。

 |
|Source|String|System|模板来源：

 -   System：系统
-   Custom：自定义

 |
|TemplateConfig|String|\{"AuditRange":\["video","image-cover","text-title"\],"AuditContent":\["screen"\]\}|模板详细配置。

 |
|TemplateId|String|33b88e9ceb64fe11d566e423cXXXXXX|模板ID。

 |
|TemplateName|String|我的自定义模板|模板名称。

 |
|TemplateType|String|AIMediaAudit|模板类型。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetAITemplate
&TemplateId=XXXXX
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetAITemplateResponse>
  <RequestId>E9790EC4-DDC4-4EF1-8EB0-XXXXXX</RequestId>
	  <TemplateInfo>
		    <TemplateId>33b88e9ceb64fe11d566e423cXXXXXX</TemplateId>
		    <TemplateType>AIMediaAudit</TemplateType>
		    <Source>Custom</Source>
		    <ModifyTime>2018-12-12T15:09:38:894Z</ModifyTime>
		    <CreationTime>2018-12-12T14:53:14:748Z</CreationTime>
		    <TemplateName>我的自定义模板</TemplateName>
		    <TemplateConfig>
			      <AuditRange>video</AuditRange>
			      <AuditRange>image-cover</AuditRange>
			      <AuditRange>text-title</AuditRange>
			      <AuditContent>screen</AuditContent>
			      <AuditItem>terrorism</AuditItem>
			      <AuditItem>porn</AuditItem>
			      <AuditAutoBlock>no</AuditAutoBlock>
		    </TemplateConfig>
	  </TemplateInfo>
</GetAITemplateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TemplateInfo":{
		"CreationTime":"2018-12-12T14:53:14:748Z",
		"Source":"Custom",
		"TemplateType":"AIMediaAudit",
		"TemplateName":"我的自定义模板",
		"TemplateConfig":{
			"AuditContent":[
				"screen"
			],
			"AuditRange":[
				"video",
				"image-cover",
				"text-title"
			],
			"AuditItem":[
				"terrorism",
				"porn"
			],
			"AuditAutoBlock":"no"
		},
		"ModifyTime":"2018-12-12T15:09:38:894Z",
		"TemplateId":"33b88e9ceb64fe11d566e423cXXXXXX"
	},
	"RequestId":"E9790EC4-DDC4-4EF1-8EB0-XXXXXX"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

