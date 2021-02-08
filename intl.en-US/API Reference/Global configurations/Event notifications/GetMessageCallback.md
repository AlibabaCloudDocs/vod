# GetMessageCallback

Queries the callback method, callback URL, and event type of an event notification.

**Note:** For more information, see [Overview](~~55627~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=GetMessageCallback&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetMessageCallback|The operation that you want to perform. Set the value to **GetMessageCallback**. |
|AppId|String|No|app-1000000|The ID of the application. If you do not set this parameter, the default value **app-1000000** is used. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MessageCallback|Struct| |The configuration of the event notification. |
|AppId|String|app-1000000|The ID of the application. |
|AuthKey|String|12345678abc|The cryptographic key. This parameter is returned only for HTTP callbacks. |
|AuthSwitch|String|on|Indicates whether callback authentication is enabled. This parameter is returned only for HTTP callbacks. Valid values:

 -   **on**: indicates that authentication is enabled.
-   **off**: indicates that authentication is disabled. |
|CallbackType|String|HTTP|The callback method. Valid values:

 -   **HTTP**
-   **MNS** |
|CallbackURL|String|http://test.com/test|The callback URL. This parameter is returned only for HTTP callbacks. |
|EventTypeList|String|FileUploadComplete,StreamTranscodeComplete,TranscodeComplete,SnapshotComplete,AIComplete,AddLiveRecordVideoComplete,CreateAuditComplete,UploadByURLComplete,ProduceMediaComplete,LiveRecordVideoComposeStart,ImageUploadComplete,VideoAnalysisComplete|The type of the callback event. |
|MnsEndpoint|String|http://1234567.mns.cn-shanghai-internal.aliyuncs.com/|The public endpoint of Message Service \(MNS\). This parameter is returned only for MNS callbacks. |
|MnsQueueName|String|vodcallback|The name of the MNS queue. This parameter is returned only for MNS callbacks. |
|RequestId|String|272A222A-F7F7-4A3E-\*\*\*\*-F531574F1234|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=GetMessageCallback
&<Common request parameters>
```

Sample success responses

`XML` format

```
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
	  <RequestId>272A222A-F7F7-4A3E-****-F531574F1234</RequestId>
</GetMessageCallbackResponse>
```

`JSON` format

```
{
    "MessageCallback":{
        "CallbackType":"HTTP",
        "EventTypeList":"FileUploadComplete,StreamTranscodeComplete,TranscodeComplete,SnapshotComplete,AIComplete,AddLiveRecordVideoComplete,CreateAuditComplete,UploadByURLComplete,ProduceMediaComplete,LiveRecordVideoComposeStart,ImageUploadComplete,VideoAnalysisComplete",
        "AuthKey":"12345678abc",
        "AppId":"app-1000000",
        "MnsQueueName":"vodcallback",
        "CallbackURL":"http://test.com/test",
        "MnsEndpoint":"http://1234567.mns.cn-shanghai-internal.aliyuncs.com/",
        "AuthSwitch":"off"
    },
    "RequestId":"272A222A-F7F7-4A3E-****-F531574F1234"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

