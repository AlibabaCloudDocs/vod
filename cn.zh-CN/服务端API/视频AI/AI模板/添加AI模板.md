# 添加AI模板

添加AI模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=AddAITemplate&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddAITemplate|系统规定参数，取值：**AddAITemplate**。 |
|TemplateConfig|String|是|\{"AuditItem":\["terrorism","porn"\],"AuditRange":\["image-cover","text-title","video"\],"AuditContent":\["screen"\],"AuditAutoBlock":"yes"\}|模板详细配置，JSON字符串，具体值详见[AITemplateConfig](~~89863#title-vd3-499-o36~~)。 |
|TemplateName|String|是|AI-media-test|模板名称，最大128字节。 |
|TemplateType|String|是|AIMediaAudit|模板类型，取值范围：

 -   **AIMediaAudit**（智能审核）
-   **AIImage**（智能封面）

 **说明：** 智能封面模板在控制台暂不可见。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-XXXXXXX|请求ID。 |
|TemplateId|String|XXXXXXX|模板ID。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=AddAITemplate
&TemplateConfig={"AuditItem":["terrorism","porn"],"AuditRange":["image-cover","text-title","video"],"AuditContent":["screen"],"AuditAutoBlock":"yes"}
&TemplateName=AI-media-test
&TemplateType=AIMediaAudit
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<AddAITemplateResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-XXXXXXX</RequestId>
	  <TemplateId>XXXXXXX</TemplateId>
</AddAITemplateResponse>
```

`JSON` 格式

```
{
    "RequestId": "25818875-5F78-4A13-BEF6-XXXXXXX",
    "TemplateId":"XXXXXXX"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

## SDK示例

建议使用 [服务端SDK](~~101789~~) 来调用API，此API各语言调用的示例代码，请参考如下：

-   [Java](~~100692#AddAITemplate~~)
-   [Python](~~101181#AddAITemplate~~)
-   [PHP](~~101159#AddAITemplate~~)
-   [.NET](~~100844#AddAITemplate~~)
-   [Node.js](~~101564#AddAITemplate~~)
-   [Go](~~101575#AddAITemplate~~)
-   [C/C++](~~102987#AddAITemplate~~)

