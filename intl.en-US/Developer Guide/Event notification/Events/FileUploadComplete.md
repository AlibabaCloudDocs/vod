# FileUploadComplete

This topic describes the FileUploadComplete event as well as its notification content and sample callbacks.

## Event type

FileUploadComplete

## Event description

The FileUploadComplete event is generated when the ApsaraVideo VOD server receives uploaded video files.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **FileUploadComplete**.|
|VideoId|String|Yes|The ID of the video.|
|Size|Long|No|The size of the uploaded file. Unit: bytes.|
|FileUrl|String|No|The URL of the uploaded file.|

**Note:** Because resumable upload is supported, the ApsaraVideo VOD server is unable to determine whether an upload has been temporarily suspended or has failed. Therefore, no notification is sent in the event an upload fails.

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{ 
    "EventTime": "2017-03-20T07:49:17Z",
    "EventType": "FileUploadComplete", 
    "VideoId": "43q91jdh7df****", 
    "Size": 1439213,
    "FileUrl":"http://ss****-bucket.oss-cn-shanghai.aliyuncs.com/27ffc438-164h67f57ef-0005-6884-51a-1****.mp4"
}
```

