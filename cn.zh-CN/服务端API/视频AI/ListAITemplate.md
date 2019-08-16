# ListAITemplate {#doc_api_vod_ListAITemplate .reference}

调用ListAITemplate查询AI模板列表。

**说明：** 目前支持的AI模板类型仅为**AIMediaAudit**（智能审核）。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAITemplate&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAITemplate|系统规定参数，取值：**ListAITemplate**。

 |
|TemplateType|String|是|AIMediaAudit|模板类型。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|请求ID。|请求ID。

 |
|TemplateInfoList| | |模板信息列表。

 |
|CreationTime|String|2018-12-12T14:53:14:748Z|创建时间，UTC格式。

 |
|IsDefault|String|Default|是否默认。取值：**Default**\(是\)，**NotDefault**\(否\)。

 |
|ModifyTime|String|2018-12-12T14:53:14:748Z|修改时间，UTC格式。

 |
|Source|String|System|模板来源：

 -   System：系统
-   Custom：自定义

 |
|TemplateConfig|String|\{"AuditRange":\["video","image-cover","text-title"\],"AuditContent":\["screen"\]\}|模板详细配置。

 |
|TemplateId|String|VOD-0003-000001|模板ID。

 |
|TemplateName|String|预置模板|模板名称。

 |
|TemplateType|String|AIMediaAudit|模板类型。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ListAITemplate
&TemplateType=AIMediaAudit
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListAITemplateResponse>
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
</ListAITemplateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TemplateInfoList":[
		{
			"CreationTime":"2018-12-12T14:53:14:748Z",
			"Source":"System",
			"TemplateType":"AIMediaAudit",
			"TemplateName":"预置模板",
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
			"IsDefault":"Default",
			"ModifyTime":"2018-12-12T15:09:38:894Z",
			"TemplateId":"VOD-0003-000001"
		},
		{
			"CreationTime":"2018-12-12T14:53:14:748Z",
			"Source":"System",
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
			"IsDefault":"NotDefault",
			"ModifyTime":"2018-12-12T15:09:38:894Z",
			"TemplateId":"33b88e9ceb64fe11d566e423cXXXXXX"
		}
	],
	"RequestId":"25818875-5F78-4A13-BEF6-XXXXXXX"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

