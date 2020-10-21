# 查询AI模板

查询AI模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetAITemplate&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetAITemplate|系统规定参数，取值：**GetAITemplate**。 |
|TemplateId|String|是|1706a0063dd733f6a823e83\*\*\*\*5879e|模板ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|080DA371-8AC0-4CD4-\*\*\*\*-33E64282D81F|请求ID。 |
|TemplateInfo|Struct| |AI模板信息。 |
|CreationTime|String|2020-07-08T06:50:45Z|创建时间，UTC格式。 |
|IsDefault|String|NotDefault|是否默认。取值：**Default**\(是\)，**NotDefault**\(否\)。 |
|ModifyTime|String|2018-12-12T15:09:38:894Z|修改时间，UTC格式。 |
|Source|String|Custom|模板来源：

 -   System：系统
-   Custom：自定义 |
|TemplateConfig|String|\{"AuditRange":\["text-title","video"\],"AuditContent":\["screen"\],"AuditItem":\["terrorism","porn"\],"AuditAutoBlock":"yes"\}|模板详细配置。 |
|TemplateId|String|1706a0063dd733f6a823e83\*\*\*\*5879e|模板ID。 |
|TemplateName|String|DemoAITemplate|模板名称。 |
|TemplateType|String|AIMediaAudit|模板类型。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetAITemplate
&TemplateId=1706a0063dd733f6a823e83****5879e
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetAITemplateResponse>
      <TemplateInfo>
            <IsDefault>NotDefault</IsDefault>
            <ModifyTime>2018-12-12T15:09:38:894Z</ModifyTime>
            <CreationTime>2020-07-08T06:50:45Z</CreationTime>
            <TemplateConfig>{"AuditRange":["text-title","video"],"AuditContent":["screen"],"AuditItem":["terrorism","porn"],"AuditAutoBlock":"yes"}</TemplateConfig>
            <TemplateName>DemoAITemplate</TemplateName>
            <TemplateType>AIMediaAudit</TemplateType>
            <Source>Custom</Source>
            <TemplateId>1706a0063dd733f6a823e83****5879e</TemplateId>
      </TemplateInfo>
      <RequestId>080DA371-8AC0-4CD4-****-33E64282D81F</RequestId>
</GetAITemplateResponse>
```

`JSON` 格式

```
{
	"TemplateInfo": {
		"IsDefault": "NotDefault",
		"ModifyTime": "2018-12-12T15:09:38:894Z",
		"CreationTime": "2020-07-08T06:50:45Z",
		"TemplateConfig": "{\"AuditRange\":[\"text-title\",\"video\"],\"AuditContent\":[\"screen\"],\"AuditItem\":[\"terrorism\",\"porn\"],\"AuditAutoBlock\":\"yes\"}",
		"TemplateName": "DemoAITemplate",
		"TemplateType": "AIMediaAudit",
		"Source": "Custom",
		"TemplateId": "1706a0063dd733f6a823e83****5879e"
	},
	"RequestId": "080DA371-8AC0-4CD4-****-33E64282D81F"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

## SDK示例

建议使用 [服务端SDK](~~101789~~) 来调用API，此API各语言调用的示例代码，请参考如下：

-   [Java](~~100692#GetAITemplate~~)
-   [Python](~~101181#GetAITemplate~~)
-   [PHP](~~101159#GetAITemplate~~)
-   [.NET](~~100844#GetAITemplate~~)
-   [Node.js](~~101564#GetAITemplate~~)
-   [Go](~~101575#GetAITemplate~~)
-   [C/C++](~~102987#GetAITemplate~~)

