# SetMessageCallback {#doc_api_vod_SetMessageCallback .reference}

调用SetMessageCallback设置事件通知的回调方式、回调地址、事件类型。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=SetMessageCallback&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetMessageCallback|系统规定参数，取值：**SetMessageCallback**。

 |
|CallbackURL|String|是|http://test.com|回调方式选择HTTP时，回调地址。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AppId|String|否|app-1000000|应用ID，不传时为系统默认应用的ID，即**app-1000000**。

 |
|AuthKey|String|否|dsf346dvet|回调方式选择HTTP时，鉴权Key，最长32位，必须同时包含大小写字母和数字。

 |
|AuthSwitch|String|否|on|回调方式选择HTTP时，回调鉴权开关，取值：**on**（启用）、**off**（不启用）。

 |
|CallbackType|String|否|HTTP|回调方式，取值：**HTTP** | **MNS**。

 |
|EventTypeList|String|否|FileUploadComplete|回调事件类型，为空时关闭所有消息通知，为ALL时开启全部消息通知。也可指定开启某些消息通知，多个用逗号分隔。取值：[事件类型](https://help.aliyun.com/document_detail/55627.html?spm=a2c4g.11186623.2.15.45eb7ca2afB9e2#MessageCallbackType)。

 |
|MnsEndpoint|String|否|endpoint|回调方式选择MNS时，消息队列公网Endpoint。

 |
|MnsQueueName|String|否|quene\_name|回调方式选择MNS时，消息队列名称。

 |
|ResourceRealOwnerId|Long|否|324|资源所有者ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=SetMessageCallback
&CallbackURL=http://test.com
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SetMessageCallbackResponse>
  <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
</SetMessageCallbackResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

