# VideoAnalysisComplete

This topic describes the VideoAnalysisComplete event as well as its notification content and sample callbacks.

## Event type

VideoAnalysisComplete

## Event description

The VideoAnalysisComplete event is generated after ApsaraVideo VOD analyzes audio and video mezzanine files to be uploaded.

**Note:**

-   By default, ApsaraVideo VOD analyzes all audio and video mezzanine files to be uploaded free of charge.
-   During the analysis, ApsaraVideo VOD extracts the metadata of the mezzanine files. Such metadata includes duration, resolution \(width and height\), bitrate, and frame rate.
-   Metadata obtained from the analysis is stored in the media library. You can call the [t1235518.md\#](/intl.en-US/API Reference/Media management/Audio&Video Management/GetMezzanineInfo.md) operation to obtain the metadata of mezzanine files.

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **VideoAnalysisComplete**.|
|VideoId|String|Yes|The ID of the audio or video file.|
|Status|String|Yes|Indicates whether the mezzanine file is analyzed. Valid values:-   **success**: The mezzanine file is analyzed.
-   **fail**: The mezzanine file failed to be analyzed. |
|Width|Long|No|The width of the mezzanine file. This parameter is unavailable if the mezzanine file is an audio file.|
|Height|Long|No|The height of the mezzanine file. This parameter is unavailable if the mezzanine file is an audio file.|
|Duration|Float|No|The duration of the mezzanine file. Unit: seconds.|
|Bitrate|String|No|The bitrate of the mezzanine file. Unit: Kbps.|
|Fps|String|No|The frame rate of the mezzanine file, in frames per second. This parameter is unavailable if the mezzanine file is an audio file.|
|Size|Long|No|The size of the mezzanine file. Unit: bytes.|
|ErrorCode|String|No|The error code. This parameter is available when an error occurs during the analysis of the mezzanine file.|
|ErrorMessage|String|No|The error message. This parameter is available when an error occurs during the analysis of the mezzanine file.|

**Note:** If the Status value is fail, the mezzanine file fails to be analyzed and no metadata is returned. A typical reason for the failure is because encapsulation of the mezzanine file is abnormal.

## Sample callbacks

Description:

-   For an HTTP callback, the following examples are the bodies of the HTTP POST requests.
-   For an MNS callback, the following examples are the message bodies.

Sample success callback message:

```
{
    "VideoId":"84bd5b0566ddj39549986befd0e80****",
    "Duration":"12",
    "Height":"360",
    "Width":"630",
    "Fps":"30",
    "Bitrate":"499",
    "Size":"1234568",
    "EventTime":"2018-11-28T10:12:48Z",
    "EventType":"VideoAnalysisComplete",
    "Status":"success"
  }
```

Sample error callback message:

```
 {
    "VideoId":"84bd5b0566ddj39549986befd0e80****",
    "EventTime":"2018-11-28T10:12:48Z",
    "EventType":"VideoAnalysisComplete",
    "Status":"fail",
    "ErrorCode":"InvalidParameter.ResourceContentBad",
    "ErrorMessage":"The resource operated InputFile is bad"
  }
```

