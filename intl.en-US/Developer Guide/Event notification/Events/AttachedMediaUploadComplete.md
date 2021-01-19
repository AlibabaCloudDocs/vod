# AttachedMediaUploadComplete

This topic describes the AttachedMediaUploadComplete event as well as its notification content and sample callbacks.

## Event type

AttachedMediaUploadComplete

## Event description

The AttachedMediaUploadComplete event is generated after attached media resources are uploaded.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **AttachedMediaUploadComplete**.|
|AttachedMediaId|String|Yes|The ID of the attached media resource.|
|Size|Long|Yes|The size of the uploaded attached media resource. Unit: bytes.|
|FileURL|String|Yes|The URL of the uploaded attached media resource.|
|Status|String|Yes|Indicates whether the attached media resource is uploaded. Valid values:-   **success**: The attached media resource is uploaded.
-   **fail**: The attached media resource failed to be uploaded. |

**Note:** Because resumable upload is supported, the ApsaraVideo VOD server is unable to determine whether an upload has been temporarily suspended or has failed. Therefore, no notification is sent in the event an upload fails.

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{ 
    "EventTime": "2019-01-20T07:49:17Z",
    "EventType": "AttachedMediaUploadComplete", 
    "AttachedMediaId": "62cb3151eba52js82j2da3b55bc5****", 
    "Size": 14333,
    "FileURL": "https://vod.aliyunsample.com/ABEBDE1JSU79FD4D1329/ba52js82j2da3b55bc5****.png",
    "Status":"success"
}
```

