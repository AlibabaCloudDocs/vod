# UpdateVodTemplate {#doc_api_vod_UpdateVodTemplate .reference}

调用UpdateVodTemplate修改截图模板。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UpdateVodTemplate&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateVodTemplate|系统规定参数，取值：**UpdateVodTemplate**。

 |
|VodTemplateId|String|是|ddddddddddddd|截图模板ID。

 |
|Name|String|否|test|模板名称。长度不超过128个字节，UTF-8编码。

 |
|TemplateConfig|String|否|\{"SnapshotConfig":\{"Count":10,"SpecifiedOffsetTime":0,"Interval":1\}|截图模板配置数据。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |
|VodTemplateId|String|ee014fd5889b67828cae2bbb2b|截图模板ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=UpdateVodTemplate
&VodTemplateId=ddddddddddddd
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateVodTemplateResponse>
      <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <VodTemplateId>ee014fd5889b67828cae2bbb2b</VodTemplateId>
</UpdateVodTemplateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"VodTemplateId":"ee014fd5889b67828cae2bbb2b",
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

