# 设置默认AI模板

设置默认AI模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SetDefaultAITemplate&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetDefaultAITemplate|系统规定参数，取值：**SetDefaultAITemplate**。 |
|TemplateId|String|是|1706a0063dd733f6a823e83\*\*\*\*5879e|模板ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|8E70E3F8-E2EE-47BC-\*\*\*\*-379D6F28514F|请求ID。 |
|TemplateId|String|1706a0063dd733f6a823e83\*\*\*\*5879e|模板ID。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SetDefaultAITemplate
&TemplateId=1706a0063dd733f6a823e83****5879e
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetDefaultAITemplateResponse>
      <RequestId>8E70E3F8-E2EE-47BC-****-379D6F28514F</RequestId>
      <TemplateId>1706a0063dd733f6a823e83****5879e</TemplateId>
</SetDefaultAITemplateResponse>
```

`JSON` 格式

```
{
	"RequestId": "8E70E3F8-E2EE-47BC-****-379D6F28514F",
	"TemplateId": "1706a0063dd733f6a823e83****5879e"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

## SDK示例

建议使用 [服务端SDK](~~101789~~) 来调用API，此API各语言调用的示例代码，请参考如下：

-   [Java](~~100692#SetDefaultAITemplate~~)
-   [Python](~~101181#SetDefaultAITemplate~~)
-   [PHP](~~101159#SetDefaultAITemplate~~)
-   [.NET](~~100844#SetDefaultAITemplate~~)
-   [Node.js](~~101564#SetDefaultAITemplate~~)
-   [Go](~~101575#SetDefaultAITemplate~~)
-   [C/C++](~~102987#SetDefaultAITemplate~~)

