# UploadByURLComplete

This topic describes the UploadByURLComplete event as well as its notification content and sample callbacks.

## Event type

UploadByURLComplete

## Event description

The UploadByURLComplete event is generated after a video is uploaded through a call to the [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md) operation.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **UploadByURLComplete**.|
|VideoId|String|Yes|The ID of the video. This parameter is available when the video is uploaded.|
|JobId|String|Yes|The ID of the upload job.|
|SourceURL|String|No|The URL of the mezzanine file.|
|Status|String|No|Indicates whether the video is uploaded. Valid values:-   **success**: The video is uploaded.
-   **fail**: The video failed to be uploaded. |
|ErrorCode|String|No|The error code. This parameter is available when an error occurs while the video is being uploaded.|
|ErrorMessage|String|No|The error message. This parameter is available when an error occurs while the video is being uploaded.|

## Sample callbacks

Description:

-   For an HTTP callback, the following examples are the bodies of the HTTP POST requests.
-   For an MNS callback, the following examples are the message bodies.

-   Sample success callback message:

    ```
    { 
      "Status": "success",
      "EventTime": "2017-03-20T07:49:17Z",
      "EventType": "UploadByURLComplete", 
      "VideoId": "43q9fjdun3f****", 
      "JobId": "4c815bjs83j1****", 
      "SourceURL ": "http://sample-bucket.oss-cn-shanghai.aliyuncs.com/27ffc438-164d55217ef-0005-6884-51a-1****.mp4",
      "Size":"123456"
    }
    ```

-   Sample error callback message:

    ```
    { 
      "Status": "fail",
      "EventTime": "2017-03-20T07:49:17Z",
      "EventType": "UploadByURLComplete", 
      "ErrorCode ": "URLInvalidError ", 
      "ErrorMessage ": "download video failed by the url, please check it", 
      "JobId": "4c815bjsued19c8e" ,
      "SourceURL ": "http://sample-bucket.oss-cn-shanghai.aliyuncs.com/27ffc438-164d55217ef-0005-6884-51a-1****.mp4"
    }
    ```


