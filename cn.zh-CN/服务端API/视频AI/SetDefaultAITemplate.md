# SetDefaultAITemplate {#doc_api_vod_SetDefaultAITemplate .reference}

调用SetDefaultAITemplate设置默认AI模板。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SetDefaultAITemplate&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetDefaultAITemplate|系统规定参数，取值：**SetDefaultAITemplate**。

 |
|TemplateId|String|是|33b88e9ceb64fe11d566e423cXXXXXX|模板ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-XXXXXXX|请求ID。

 |
|TemplateId|String|33b88e9ceb64fe11d566e423cXXXXXX|模板ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=SetDefaultAITemplate
&TemplateId=33b88e9ceb64fe11d566e423cXXXXXX
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SetDefaultAITemplateResponse>
  <RequestId>25818875-5F78-4A13-BEF6-XXXXXXX</RequestId>
	  <TemplateId>33b88e9ceb64fe11d566e423cXXXXXX</TemplateId>
</SetDefaultAITemplateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-XXXXXXX",
	"TemplateId":"33b88e9ceb64fe11d566e423cXXXXXX"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

