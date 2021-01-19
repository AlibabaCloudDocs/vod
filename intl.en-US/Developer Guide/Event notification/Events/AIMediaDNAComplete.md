# AIMediaDNAComplete

This topic describes the AIMediaDNAComplete event as well as its notification content and sample callbacks.

## Event type

AIMediaDNAComplete

## Event description

The AIMediaDNAComplete event is generated after video DNA jobs are complete.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **AIMediaDNAComplete**.|
|JobId|String|Yes|The ID of the video DNA job. The value is the same as the JobId value returned by the SubmitAIJob operation.|
|MediaId|String|Yes|The ID of the video.|
|Status|String|Yes|Indicates whether the video DNA job is completed. Valid values:-   **success**: The video DNA job is completed.
-   **fail**: The video DNA job failed to be completed. |
|Code|String|No|The error code. This parameter is available when the video DNA job fails.|
|Message|String|No|The error message. This parameter is available when the video DNA job fails.|
|Data|String|Yes|The result of the video DNA job. The value is a JSON string. For more information, see the "AIMediaDNAResult" section in [AI processing parameters](/intl.en-US/API Reference/Appendix/Video AI parameters.md).|

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{
    "EventTime": "2017-03-20T07:49:17Z",
    "EventType": "AIMediaDNAComplete",
    "JobId": "88c6ca184c0edj384a5b665e2a12****",
    "MediaId": "3D12340d92cjsw83k1fab46a0b847fd****",
    "Status": "success",
    "Code": "0",
    "Message": "OK",
    "Data": "{\"VideoDNA\":[{\"Similarity\":\"0.99\",\"PrimaryKey\":\"7a1d275cc8da4jw93mkde0e182e80****\",\"Detail\":[{\"Input\":{\"Start\":\"0.0\",\"Duration\":\"14.0\"},\"Duplication\":{\"Start\":\"0.5\",\"Duration\":\"14.4\"}}]}]}"
}
```

