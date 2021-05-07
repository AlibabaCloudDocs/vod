# DeleteMessageCallback

Deletes the callback method, callback URL, and event type of an event notification.

**Note:** For more information, see [Overview](~~55627~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=DeleteMessageCallback&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteMessageCallback|The operation that you want to perform. Set the value to **DeleteMessageCallback**. |
|AppId|String|Yes|app-1000000|The ID of the application. If you do not set this parameter, the default value **app-1000000** is used. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|25818875-5F78-4A13-\*\*\*\*-D7393642CA58|The ID of the request. |

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=DeleteMessageCallback
&AppId=app-1000000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteMessageCallbackResponse>
      <RequestId>25818875-5F78-4A13-****-D7393642CA58</RequestId>
</DeleteMessageCallbackResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A13-****-D7393642CA58"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

