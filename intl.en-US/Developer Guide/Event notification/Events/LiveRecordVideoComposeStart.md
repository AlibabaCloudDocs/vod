# LiveRecordVideoComposeStart

This topic describes the LiveRecordVideoComposeStart event as well as its notification content and sample callbacks.

## Event type

LiveRecordVideoComposeStart

## Event description

If automatic production is enabled when live streams are being recorded as on-demand videos, ApsaraVideo VOD automatically processes the recorded on-demand videos whenever the live streams end or time out. In this case, the LiveRecordVideoComposeStart events are generated. The event notifications include the IDs of the produced videos.

**Note:**

-   By default, a live stream is considered to have ended when it has been interrupted for more than 3 minutes.
-   The LiveRecordVideoComposeStart event only indicates that live streams have begun to be recorded as on-demand videos. This event does not include the production status. You must record the ID of the produced video to follow up the production status.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **LiveRecordVideoComposeStart**.|
|VideoId|String|Yes|The ID of the produced video.|
|Status|String|Yes|Indicates whether the live stream has begun to be recorded as an on-demand video. Valid values:-   **success**: Recording has started for the live stream.
-   **fail**: Recording failed to start for the live stream. |
|StreamName|String|No|The name of the live stream.|
|DomainName|String|No|The domain name of the live stream.|
|AppName|String|No|The name of the application.|

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{ 
  "EventTime": "2017-12-08T09:26:17Z",
  "EventType": "LiveRecordVideoComposeStart", 
  "VideoId": "43q9fsjnehdf****", 
  "Status": "success",
  "StreamName": "streamname_****",
  "DomainName": "domainname_****",
  "AppName": "appname_****"
}
```

