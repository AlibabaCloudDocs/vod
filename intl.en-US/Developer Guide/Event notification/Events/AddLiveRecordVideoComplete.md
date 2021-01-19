# AddLiveRecordVideoComplete

This topic describes the AddLiveRecordVideoComplete event as well as its notification content and sample callbacks.

## Event type

AddLiveRecordVideoComplete

## Event description

The AddLiveRecordVideoComplete event is generated after a live stream has been recorded as an on-demand videos and the recording period or live streaming ends.

**Note:** A live stream is considered to have ended when it has been interrupted for more than 3 minutes.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **AddLiveRecordVideoComplete**.|
|VideoId|String|Yes|The ID of the video.|
|Status|String|Yes|Indicates whether the live stream is recorded as an on-demand video. Valid values:-   **success**: The live stream is recorded as an on-demand video.
-   **fail**: The live stream failed to be recorded as an on-demand video. |
|StreamName|String|No|The name of the live stream.|
|DomainName|String|No|The domain name of the live stream.|
|AppName|String|No|The name of the application.|
|RecordStartTime|String|No|The time when the recording starts. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|RecordEndTime|String|No|The time when the recording ends. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{ 
  "EventTime": "2017-12-08T09:26:17Z",
  "EventType": "AddLiveRecordVideoComplete", 
  "VideoId": "43q9fjdhef****", 
  "Status": "success",
  "StreamName": "xxx",
  "DomainName": "xxx",
  "AppName": "xxx",
  "RecordStartTime":"2017-12-08T07:40:56Z",
  "RecordEndTime":"2017-12-08T09:26:17Z",
}
```

