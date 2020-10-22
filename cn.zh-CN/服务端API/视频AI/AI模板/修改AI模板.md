# 修改AI模板

修改AI模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UpdateAITemplate&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateAITemplate|系统规定参数，取值：**UpdateAITemplate** |
|TemplateConfig|String|是|\{"AuditItem":\["terrorism","porn"\],"AuditRange":\["text-title","video"\],"AuditContent":\["screen"\],"AuditAutoBlock":"yes"\}|模板详细配置。JSON字符串，具体值详见[AITemplateConfig](~~89863#title-vd3-499-o36~~) |
|TemplateId|String|是|1706a0063dd733f6a823e\*\*\*\*0a5879e|模板ID。 |
|TemplateName|String|是|DemoAITemplate|模板名称，最大128字节。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-XXXXXXX|请求ID。 |
|TemplateId|String|XXXXXXX|模板ID。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UpdateAITemplate
&TemplateConfig={"AuditItem":["terrorism","porn"],"AuditRange":["text-title","video"],"AuditContent":["screen"],"AuditAutoBlock":"yes"}
&TemplateId=1706a0063dd733f6a823e****0a5879e
&TemplateName=DemoAITemplate
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateAITemplateResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-XXXXXXX</RequestId>
	  <TemplateId>XXXXXXX</TemplateId>
</UpdateAITemplateResponse>
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

-   [Java](~~100692#UpdateAITemplate~~)
-   [Python](~~101181#UpdateAITemplate~~)
-   [PHP](~~101159#UpdateAITemplate~~)
-   [.NET](~~100844#UpdateAITemplate~~)
-   [Node.js](~~101564#UpdateAITemplate~~)
-   [Go](~~101575#UpdateAITemplate~~)
-   [C/C++](~~102987#UpdateAITemplate~~)

