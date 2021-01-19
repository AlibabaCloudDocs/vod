# ImageUploadComplete

This topic describes the ImageUploadComplete event as well as its notification content and sample callbacks.

## Event type

ImageUploadComplete

## Event description

The ImageUploadComplete event is generated after an image is uploaded.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **ImageUploadComplete**.|
|ImageId|String|Yes|The ID of the image.|
|Size|Long|No|The size of the uploaded image. Unit: bytes.|
|FileURL|String|No|The URL of the uploaded image.|
|Status|String|Yes|Indicates whether the image is uploaded. Valid values:-   **success**: The image is uploaded.
-   **fail**: The image failed to be uploaded. |

**Note:** Because resumable upload is supported, the ApsaraVideo VOD server is unable to determine whether an upload has been temporarily suspended or has failed. Therefore, no notification is sent in the event an upload fails.

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{
    "Status": "success",
    "FileURL": "https://outin-bfefbb90a47c16sh280163e1c7426.oss-cn-shanghai.aliyuncs.com/image/default/AF8018C2908A434HD73JA678D08B0E****.jpg",
    "AppId": "app-1000000",
    "EventType": "ImageUploadComplete",
    "EventTime": "2017-03-20T07:49:17Z",
    "Size": 105520,
    "ImageId": "59bdbf10df76a8d8b6137a5ad12****"
}
```

