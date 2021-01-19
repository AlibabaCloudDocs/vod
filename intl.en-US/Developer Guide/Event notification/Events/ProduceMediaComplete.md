# ProduceMediaComplete

This topic describes the ProduceMediaComplete event as well as its notification content and sample callbacks.

## Event type

ProduceMediaComplete

## Event description

This event is generated after media editing is complete.

**Note:**

-   Media editing can be initiated on the [Video Editor](https://vod.console.aliyun.com/#/videoEditor/list) page in the ApsaraVideo VOD console or through calls to the [t1235562.md\#](/intl.en-US/API Reference/Video editing/ProduceEditingProjectVideo.md) operation.
-   Media files produced from media editing are used as the mezzanine files of media resources.

## Event notification content

|Field|Type|Required|Description|
|-----|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **ProduceMediaComplete**.|
|Status|String|Yes|The status of media editing. Valid values:-   **success**: Media editing succeeds.
-   **fail**: Media editing fails.

**Note:** If the value of Status is fail, mezzanine files of produced resources are not generated. |
|MediaId|String|Yes|The ID of the produced media resource.|
|ProjectId|String|Yes|The ID of the online editing project.|
|ErrorCode|String|No|The error code. This parameter is available when an error occurs during media editing.|
|ErrorMessage|String|No|The error message. This parameter is available when an error occurs during media editing.|

## Sample callbacks

Description:

-   For an HTTP callback, the following examples are the bodies of the HTTP POST requests.
-   For an MNS callback, the following examples are the message bodies.

Sample success callback message:

```
{
    "MediaId": "1234343b689*****a5422dfe1e472a41",
    "ProjectId": "987624bab6*****d9fcdeefdd974c7aa",
    "Status": "success",
    "EventType": "ProduceMediaComplete",
    "EventTime": "2018-12-26T14:34:09Z"
}
```

Sample error callback message:

```
{
    "MediaId": "1234343b689*****a5422dfe1e472a41",
    "ProjectId": "987624bab6*****d9fcdeefdd974c7aa",
    "Status": "fail",
    "EventType": "ProduceMediaComplete",
    "EventTime": "2018-12-26T14:34:09Z",
    "ErrorCode": "InvalidParameter.ResourceContentBad",
    "ErrorMessage": "The resource operated InputFile is bad"
}
```

