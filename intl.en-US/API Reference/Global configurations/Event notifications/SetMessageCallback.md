# SetMessageCallback

Sets the callback method, callback URL, and event type of an event notification.

**Note:** For more information, see [Overview](~~55627~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=SetMessageCallback&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetMessageCallback|The operation that you want to perform. Set the value to **SetMessageCallback**. |
|CallbackURL|String|No|http://test.com|The callback URL. This parameter only takes effect when the CallbackType parameter is set to HTTP. |
|CallbackType|String|No|HTTP|The callback method. Valid values:

 -   **HTTP**
-   **MNS** |
|EventTypeList|String|No|FileUploadComplete|The type of the callback event. If you do not set this parameter, notifications for all types of events are disabled. If you set this parameter to ALL, notifications for all types of events are enabled. You can specify the event types for which notifications are enabled. Separate multiple event types with commas \(,\). For more information about the valid values of this parameter, see [Overview](~~55627~~). |
|AuthSwitch|String|No|on|Specifies whether to enable callback authentication. This parameter only takes effect when the CallbackType parameter is set to HTTP. Valid values:

 -   **on**: enables authentication.
-   **off**: disables authentication. |
|AuthKey|String|No|dsf346dvet|The cryptographic key. This parameter only takes effect when the CallbackType parameter is set to HTTP. The key can be up to 32 characters in length and must contain uppercase letters, lowercase letters, and digits. |
|MnsEndpoint|String|No|http://\*\*\*\*.mns.cn-shanghai-internal.aliyuncs.com/|The public endpoint of Message Service \(MNS\). This parameter only takes effect when the CallbackType parameter is set to MNS. |
|MnsQueueName|String|No|quene\_name|The name of the MNS queue. This parameter only takes effect when the CallbackType parameter is set to MNS. |
|AppId|String|No|app-1000000|The ID of the application. If you do not set this parameter, the default value **app-1000000** is used. |

**Note:** To enable notifications for AI-related events, such as AIMediaAuditComplete and AIMediaDNAComplete, set the EventTypeList parameter to **AIComplete**.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=SetMessageCallback
&CallbackURL=http://test.com
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetMessageCallbackResponse>
      <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
</SetMessageCallbackResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

