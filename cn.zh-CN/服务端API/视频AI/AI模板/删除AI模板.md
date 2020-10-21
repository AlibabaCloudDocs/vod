# 删除AI模板

删除AI模板。

**说明：** 已设置为默认的AI模板不能删除。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteAITemplate&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAITemplate|系统规定参数，取值：**DeleteAITemplate**。 |
|TemplateId|String|是|XXXXX|模板ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-XXXXXXX|请求ID。 |
|TemplateId|String|XXXXXXX|模板ID。 |

**说明：** 下述请求示例中的“公共请求参数”详情，参见[公共参数说明文档](~~44432~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeleteAITemplate
&TemplateId=XXXXX
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteAITemplateResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-XXXXXXX</RequestId>
	  <TemplateId>XXXXXXX</TemplateId>
</DeleteAITemplateResponse>
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

-   [Java](~~100692#DeleteAITemplate~~)
-   [Python](~~101181#DeleteAITemplate~~)
-   [PHP](~~101159#DeleteAITemplate~~)
-   [.NET](~~100844#DeleteAITemplate~~)
-   [Node.js](~~101564#DeleteAITemplate~~)
-   [Go](~~101575#DeleteAITemplate~~)
-   [C/C++](~~102987#DeleteAITemplate~~)

