# AIVideoTagComplete

This topic describes the AIVideoTagComplete event as well as its notification content and sample callbacks.

## Event type

AIVideoTagComplete

## Event description

The AIVideoTagComplete event is generated when smart tag jobs are complete.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **AIVideoTagComplete**.|
|JobId|String|Yes|The ID of the smart tag job. The value is the same as the JobId value returned by the SubmitSmarttagJob operation.|
|MediaId|String|Yes|The ID of the video.|
|Status|String|Yes|Indicates whether the smart tag job is complete. Valid values:-   **success**: The smart tag job is complete.
-   **fail**: The smart tag job failed to be complete. |
|Code|String|No|The error code. This parameter is available when an error occurs in the smart tag job.|
|Message|String|No|The error message. This parameter is available when an error occurs in the smart tag job.|
|Data|String|Yes|The result of the smart tag job. The value is a JSON string. For more information, see the "AIVideoTagResult" section in [AI processing parameters](/intl.en-US/API Reference/Appendix/Video AI parameters.md).|

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{
    "EventTime": "2017-03-20T07:49:17Z",
    "EventType": "AIVideoTagComplete",
    "JobId": "jd83k4184c0e47098a5b665e2aj3****",
    "MediaId": "sj83k40d92c641401fab46a0b842e9****",
    "Status": "success",
    "Code": "0",
    "Message": "OK",
    "Data": "{\"Keyword\":[{\"Times\":[\"3260\",\"4000\",\"5000\",\"8410\",\"10000\",\"12000\",\"13000\",\"14000\",\"15000\"],\"Tag\":\"Cushion\"},{\"Times\":[\"2000\",\"4000\",\"5000\",\"7000\",\"8000\",\"10000\",\"12000\",\"13000\",\"14000\"],\"Tag\":\"lancome\"},{\"Times\":[\"3260\",\"4000\",\"5000\",\"8410\",\"12000\",\"13000\",\"14000\"],\"Tag\":\"Lancome\"},{\"Times\":[\"4000\",\"5000\",\"12000\",\"13000\",\"14000\",\"15000\"],\"Tag\":\"CC cream\"},{\"Times\":[\"8000\",\"8410\",\"10000\"],\"Tag\":\"Light\"},{\"Times\":[\"3260\",\"8410\"],\"Tag\":\"CC cream\"},{\"Times\":[\"3260\"],\"Tag\":\"Petal\"},{\"Times\":[\"8410\"],\"Tag\":\"Air\"},{\"Times\":[\"900\"],\"Tag\":\"Bright\"},{\"Times\":[\"900\"],\"Tag\":\"Clean\"},{\"Times\":[\"900\"],\"Tag\":\"Skin\"},{\"Times\":[\"8410\"],\"Tag\":\"Lancome\"}],\"Person\":[{\"Times\":[\"10760\"],\"Tag\":\"Sam\",\"FaceUrl\":\"http://test.com/aivideotag/11111B65-1955-4B84-823D-7921A742****/Index_00016.jpg\"}],\"Location\":[{\"Times\":[\"8410\"],\"Tag\":\"Asia\"}]}"
}
```

