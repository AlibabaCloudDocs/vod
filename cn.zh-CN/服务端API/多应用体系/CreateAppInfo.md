# CreateAppInfo {#doc_api_vod_CreateAppInfo .reference}

调用CreateAppInfo创建新的应用。

**说明：** 请参考[多应用开发指南](https://help.aliyun.com/document_detail/113600.html?spm=a2c4g.11186623.2.15.477b68a7Ff7FAG)使用，每个账号最多能创建10个应用。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=CreateAppInfo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAppInfo|系统规定参数，取值：**CreateAppInfo**。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AppName|String|否|test|应用名称，不能重复。最多包含128个字符或汉字，UTF-8编码。格式：`^[a-zA-Z0-9.@-\u4e00-\u9fa5]+$`。

 |
|Description|String|否|myfirstapp|应用描述，最多支持512个字符或汉字，UTF-8编码。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AppId|String|app-xxxxxxxx|应用ID。

 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=CreateAppInfo
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateAppInfoResponse>
      <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
	  <AppId>app-xxxxxxxx</AppId>
</CreateAppInfoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
	"AppId":"app-xxxxxxxx"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

