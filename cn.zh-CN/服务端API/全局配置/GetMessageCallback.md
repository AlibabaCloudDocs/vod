# GetMessageCallback {#doc_api_vod_GetMessageCallback .reference}

调用GetMessageCallback查询事件通知的回调方式、回调地址、事件类型。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=vod&api=GetMessageCallback&type=RPC&version=2017-03-21)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMessageCallback|系统规定参数，取值：**GetMessageCallback**。

 |
|AccessKeyId|String|否|your\_accesskey\_id|您的AccessKey ID。

 |
|AppId|String|否|app-1000000|应用ID，不传时为系统默认应用的ID，即**app-1000000**。

 |
|ResourceRealOwnerId|Long|否|346|资源所有者ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MessageCallback| | |事件通知配置。

 |
|AppId|String|app-xxxxx|应用ID。

 |
|AuthKey|String|12345678abc|回调方式选择HTTP时，鉴权Key。

 |
|AuthSwitch|String|on|回调方式选择HTTP时，回调鉴权开关，取值：**on**（启用）、**off**（不启用）。

 |
|CallbackType|String|HTTP|回调方式，取值：**HTTP | MNS**。

 |
|CallbackURL|String|http://test.com/test|回调方式选择HTTP时，回调地址。

 |
|EventTypeList|String|FileUploadComplete,StreamTranscodeComplete,TranscodeComplete,SnapshotComplete,AIComplete,AddLiveRecordVideoComplete,CreateAuditComplete,UploadByURLComplete,ProduceMediaComplete,LiveRecordVideoComposeStart,ImageUploadComplete,VideoAnalysisComplete|回调事件类型。

 |
|MnsEndpoint|String|http://1234567.mns.cn-shanghai-internal.aliyuncs.com/|回调方式选择MNS时，消息队列公网Endpoint。

 |
|MnsQueueName|String|vodcallback|回调方式选择MNS时，消息队列名称。

 |
|RequestId|String|272A222A-F7F7-4A3E-BF18-F531574F1234|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=GetMessageCallback
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetMessageCallbackResponse>
	  <MessageCallback>
		    <CallbackType>HTTP</CallbackType>
		    <EventTypeList>FileUploadComplete,StreamTranscodeComplete,TranscodeComplete,SnapshotComplete,AIComplete,AddLiveRecordVideoComplete,CreateAuditComplete,UploadByURLComplete,ProduceMediaComplete,LiveRecordVideoComposeStart,ImageUploadComplete,VideoAnalysisComplete</EventTypeList>
		    <AuthKey>12345678abc</AuthKey>
		    <AppId>app-1000000</AppId>
		    <MnsQueueName>vodcallback</MnsQueueName>
		    <CallbackURL>http://test.com/test</CallbackURL>
		    <MnsEndpoint>http://1234567.mns.cn-shanghai-internal.aliyuncs.com/</MnsEndpoint>
		    <AuthSwitch>off</AuthSwitch>
	  </MessageCallback>
	  <RequestId>272A222A-F7F7-4A3E-BF18-F531574F1234</RequestId>
</GetMessageCallbackResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"MessageCallback":{
		"EventTypeList":"FileUploadComplete,StreamTranscodeComplete,TranscodeComplete,SnapshotComplete,AIComplete,AddLiveRecordVideoComplete,CreateAuditComplete,UploadByURLComplete,ProduceMediaComplete,LiveRecordVideoComposeStart,ImageUploadComplete,VideoAnalysisComplete",
		"CallbackType":"HTTP",
		"AuthKey":"12345678abc",
		"AppId":"app-1000000",
		"MnsQueueName":"vodcallback",
		"MnsEndpoint":"http://1234567.mns.cn-shanghai-internal.aliyuncs.com/",
		"CallbackURL":"http://test.com/test",
		"AuthSwitch":"off"
	},
	"RequestId":"272A222A-F7F7-4A3E-BF18-F531574F1234"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/vod)查看更多错误码。

