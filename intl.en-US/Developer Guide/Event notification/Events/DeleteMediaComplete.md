# DeleteMediaComplete

This topic describes the DeleteMediaComplete event as well as its notification content and sample callbacks.

## Event type

DeleteMediaComplete

## Event description

The DeleteMediaComplete event is generated only for the [DeleteVideo](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteVideo.md) operation.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventType|String|Yes|The event type. The value is **DeleteMediaComplete**.|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|Status|String|Yes|Indicates whether the media resource is deleted. Valid values:-   **success**: The media resource is deleted.
-   **fail**: The media resource failed to be deleted. |
|MediaType|String|Yes|The type of the media resource.-   **video**: audio and video
-   **image**: image
-   **attached**: attached media resource |
|DeleteType|String|Yes|The type of the deleted media resource. Valid values:-   **all**: complete information of the media resource
-   **mezzanine**: information of the mezzanine file
-   **stream**: information of the transcoded stream |
|MediaId|String|Yes|The ID of the media resource.|
|JobIds|String|No|This parameter is available only when the DeleteType parameter is stream.|
|ErrorCode|String|No|The error code. This parameter is available when an error occurs during the delete operation.|
|ErrorMessage|String|No|The error message. This parameter is available when an error occurs during the delete operation.|

## Sample callbacks

Description:

-   For an HTTP callback, the following examples are the bodies of HTTP POST requests.
-   For an MNS callback, the following examples are the message bodies.

Sample success callback message:

```
{ 
    "EventType": "DeleteMediaComplete",
    "EventTime": "2017-03-20T07:49:17Z",
    "Status": "success",
    "MediaType": "video",
    "DeleteType": "all",
    "MediaId": "1234343b689jsi3ka5422dfe1e47****"
}
```

Sample error callback message:

```
{ 
    "EventType": "DeleteMediaComplete",
    "EventTime": "2017-03-20T07:49:17Z",
    "Status": "fail",
    "MediaType": "video",
    "DeleteType": "all",
    "MediaId": "1234343b689jsi3ka5422dfe1e47****",
    "ErrorCode": "InvalidVideo.NotFound",
    "ErrorMessage": "The video does not exist."
}
```

