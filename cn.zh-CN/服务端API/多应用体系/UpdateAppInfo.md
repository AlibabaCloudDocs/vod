# UpdateAppInfo {#doc_api_vod_UpdateAppInfo .reference}

调用UpdateAppInfo更新应用信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=UpdateAppInfo&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateAppInfo|系统规定参数，取值：**UpdateAppInfo**。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AppId|String|否|app-xxxxxx|应用ID。

 |
|AppName|String|否|test|应用名称，最多包含128个字符或汉字，UTF-8编码。格式：`^[a-zA-Z0-9.@-\u4e00-\u9fa5]+$`。

 |
|Description|String|否|my first app.|应用描述，最多支持512个字符或汉字，UTF-8编码。

 |
|ResourceRealOwnerId|Long|否|577|资源所有者ID。

 |
|Status|String|否|Disable|应用状态，可选值：**Normal**\(正常启用\)，**Disable**\(停用\)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=UpdateAppInfo
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateAppInfoResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</UpdateAppInfoResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

