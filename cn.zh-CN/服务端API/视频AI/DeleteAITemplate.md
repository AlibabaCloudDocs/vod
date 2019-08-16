# DeleteAITemplate {#doc_api_vod_DeleteAITemplate .reference}

调用DeleteAITemplate删除AI模板。

已设置为默认的AI模板不能删除。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=DeleteAITemplate&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAITemplate|系统规定参数，取值：**DeleteAITemplate**。

 |
|TemplateId|String|是|XXXXX|模板ID。

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

http(s)://[Endpoint]/?Action=DeleteAITemplate
&TemplateId=XXXXX
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteAITemplateResponse>
	  <RequestId>25818875-5F78-4A13-BEF6-XXXXXXX</RequestId>
	  <TemplateId>XXXXXXX</TemplateId>
</DeleteAITemplateResponse>
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

