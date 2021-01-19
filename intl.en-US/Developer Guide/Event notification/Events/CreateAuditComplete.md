# CreateAuditComplete

This topic describes the CreateAuditComplete event as well as its notification content and sample callbacks.

## Event type

CreateAuditComplete

## Event description

The CreateAuditComplete event is generated when the [t1235575.md\#](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md) operation is called.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventType|String|Yes|The event type. The value is **CreateAuditComplete**.|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|Status|String|Yes|Indicates whether the manual review is complete. Valid values:-   **success**: The manual review is complete.
-   **fail**: The manual review failed to be complete. |
|MediaId|String|Yes|The ID of the media resource.|
|SubType|String|Yes|The type of the media resource.**video**: audio and video |
|AuditStatus|String|Yes|The result of the manual review. Valid values:-   **Normal**: The media resource passes manual review.
-   **Blocked**: The media resource failed to pass manual review and is rejected. |
|CreationTime|String|Yes|The time when the manual review is performed. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|Auditor|String|No|The auditor who performs the manual review.|
|Reason|String|No|The reason for the manual review.|

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{ 
    "EventType": "CreateAuditComplete",
    "EventTime": "2017-03-20T07:49:17Z",
    "MediaId": "<Example ID>",
    "Status": "success",
    "CreationTime": "2017-03-20T07:49:17Z",
    "SubType": "video",
    "AuditStatus": "Blocked",
    "Auditor":"author",
    "Reason":"Vulgar content"
}
```

