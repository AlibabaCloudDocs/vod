# 删除AI模板

调用DeleteAITemplate删除AI模板。

**说明：** 已设置为默认的AI模板不能删除。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteAITemplate&type=RPC&version=2017-03-21)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAITemplate|操作接口名，系统规定参数。取值：**DeleteAITemplate**。 |
|TemplateId|String|是|1706a0063dd733f6a823e\*\*\*\*0a5879e|模板ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-\*\*\*\*|请求ID。 |
|TemplateId|String|1706a0063dd733f6a823e\*\*\*\*0a5879e|模板ID。 |

## 示例

请求示例

```
https://vod.aliyuncs.com/?Action=DeleteAITemplate
&TemplateId=1706a0063dd733f6a823e****0a5879e
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteAITemplateResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-****</RequestId>
	  <TemplateId>1706a0063dd733f6a823e****0a5879e</TemplateId>
</DeleteAITemplateResponse>
```

`JSON` 格式

```
{
    "RequestId": "25818875-5F78-4A13-BEF6-****",
    "TemplateId":"1706a0063dd733f6a823e****0a5879e"
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

