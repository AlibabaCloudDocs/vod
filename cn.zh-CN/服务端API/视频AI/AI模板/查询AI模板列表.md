# 查询AI模板列表

调用ListAITemplate查询AI模板列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=ListAITemplate&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAITemplate|操作接口名，系统规定参数。取值：**ListAITemplate**。 |
|TemplateType|String|是|AIMediaAudit|模板类型。取值：

 -   **AIMediaAudit**：智能审核。
-   **AIImage**：智能封面。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|75B7BC67-FB8C-4653-\*\*\*\*-F4B01ED2DA95|请求ID。 |
|TemplateInfoList|Array of TemplateInfoList| |模板信息列表。 |
|CreationTime|String|2020-07-08T06:50:45Z|创建时间。日期格式按照ISO8601表示法，并使用UTC时间，格式为：*yyyy-MM-dd*T*HH:mm:ss*Z。 |
|IsDefault|String|NoDefault|是否默认。取值：

 -   **Default**：是。
-   **NotDefault**：否。 |
|ModifyTime|String|2020-07-08T07:05:49Z|修改时间。日期格式按照ISO8601表示法，并使用UTC时间，格式为：*yyyy-MM-dd*T*HH:mm:ss*Z。 |
|Source|String|Custom|模板来源。取值：

 -   **System**：系统。
-   **Custom**：自定义。 |
|TemplateConfig|String|\{"AuditRange":\["text-title","video"\],"AuditContent":\["screen"\],"AuditItem":\["terrorism","porn"\],"AuditAutoBlock":"yes"\}|模板详细配置，JSON字符串。

 具体值，请参见[AITemplateConfig](https://help.aliyun.com/document_detail/89863.html#title-vd3-499-o36)。 |
|TemplateId|String|1706a0063dd733f6a823e83\*\*\*\*5879e|模板ID。 |
|TemplateName|String|DemoAITemplate|模板名称。 |
|TemplateType|String|AIMediaAudit|模板类型。取值：

 -   **AIMediaAudit**：智能审核。
-   **AIImage**：智能封面。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=ListAITemplate
&TemplateType=AIMediaAudit
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListAITemplateResponse>
      <RequestId>75B7BC67-FB8C-4653-****-F4B01ED2DA95</RequestId>
      <TemplateInfoList>
            <IsDefault>NoDefault</IsDefault>
            <ModifyTime>2020-07-08T07:05:49Z</ModifyTime>
            <CreationTime>2020-07-08T06:50:45Z</CreationTime>
            <TemplateConfig>{"AuditRange":["text-title","video"],"AuditContent":["screen"],"AuditItem":["terrorism","porn"],"AuditAutoBlock":"yes"}</TemplateConfig>
            <TemplateName>DemoAITemplate</TemplateName>
            <TemplateType>AIMediaAudit</TemplateType>
            <Source>Custom</Source>
            <TemplateId>1706a0063dd733f6a823e83****5879e</TemplateId>
      </TemplateInfoList>
</ListAITemplateResponse>
```

`JSON` 格式

```
{
	"RequestId": "75B7BC67-FB8C-4653-****-F4B01ED2DA95",
	"TemplateInfoList": [{
		"IsDefault": "NoDefault",
		"ModifyTime": "2020-07-08T07:05:49Z",
		"CreationTime": "2020-07-08T06:50:45Z",
		"TemplateConfig": "{\"AuditRange\":[\"text-title\",\"video\"],\"AuditContent\":[\"screen\"],\"AuditItem\":[\"terrorism\",\"porn\"],\"AuditAutoBlock\":\"yes\"}",
		"TemplateName": "DemoAITemplate",
		"TemplateType": "AIMediaAudit",
		"Source": "Custom",
		"TemplateId": "1706a0063dd733f6a823e83****5879e"
	}]
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

## SDK示例

建议使用[服务端SDK](~~101789~~)来调用API，此API各语言调用的示例代码，请参见：

-   [Java](~~100692~~)
-   [Python](~~101181~~)
-   [PHP](~~101159~~)
-   [.NET](~~100844~~)
-   [Node.js](~~101564~~)
-   [Go](~~101575~~)
-   [C/C++](~~102987~~)

