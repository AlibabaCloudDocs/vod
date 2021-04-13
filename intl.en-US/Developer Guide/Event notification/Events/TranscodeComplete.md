# TranscodeComplete

This topic describes the TranscodeComplete event as well as its notification content and sample callbacks.

## Event type

TranscodeComplete

## Event description

The TranscodeComplete event is generated after all streams of a video are transcoded.

**Note:** If you have enabled URL signing, you must generate your own auth\_key to access the playback URL of the video. Otherwise, the `HTTP 403` error code is returned for your request. For more information about URL signing, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md).

## Event notification content

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **TranscodeComplete**.|
|VideoId|String|Yes|The ID of the video.|
|Status|String|Yes|Indicates whether the video streams are transcoded. The value is success as long as one video stream is transcoded. Valid values:-   **success**: The video streams are transcoded.
-   **fail**: The video streams failed to be transcoded. |
|Extend|String|No|The user-defined parameter that is returned in the pass-through mode in callbacks. For more information, see [UserData](/intl.en-US/API Reference/Appendix/Request parameters.md).|
|StreamInfos|Array|No|Details about the video streams. For more information, see the following table.|

The value of StreamInfos is an array. The following table describes the fields of this parameter for each stream.

|Field|Type|Required|Description|
|-----|----|--------|-----------|
|Status|String|No|Indicates whether the video stream is transcoded. Valid values:-   **success**: The video stream is transcoded.
-   **fail**: The video stream failed to be transcoded. |
|Bitrate|String|No|The bitrate of the video stream. Unit: Kbps.|
|Definition|String|No|The definition of the video stream. Valid values:-   **FD**: low definition
-   **LD**: standard definition
-   **SD**: high definition
-   **HD**: ultra high definition
-   **OD**: original definition
-   **2K**
-   **4K**
-   **AUTO**: adaptive |
|Duration|Float|No|The length of the video stream. Unit: seconds.|
|Encrypt|Boolean|No|Indicates whether the video stream is encrypted.|
|ErrorCode|String|No|The error code. This parameter is available when an error occurs while the video stream is being transcoded.|
|ErrorMessage|String|No|The error message. This parameter is available when an error occurs while the video stream is being transcoded.|
|FileUrl|String|No|The playback URL of the video stream. The URL does not carry the signing auth\_key. If you have enabled URL signing, you must generate your own auth\_key to access the playback URL of the video stream.|
|Format|String|No|The format of the video stream.-   **mp4**
-   **m3u8** |
|Fps|String|No|The frame rate of the video stream, in frames per second.|
|Height|Long|No|The height of the video stream. Unit: px.|
|Size|Long|No|The size of the video stream. Unit: bytes.|
|Width|Long|No|The width of the video stream. Unit: px.|
|JobId|String|No|The ID of the transcoding job.|

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{ 
  "EventTime": "2017-03-20T07:49:17Z",
  "EventType": "TranscodeComplete", 
  "VideoId": "43q9fjsh73f****", 
  "Status": "success",
  "Extend":"test data",
  "StreamInfos": 
  [
   {
     "Status": "success",
     "Bitrate": "925",
     "Definition": "LD",
     "Duration": 15,
     "Encrypt": false,
     "FileUrl": "http://vod.aliyunsample.com/ABEBDE1JSU79FD4D1329/62cb3151eba52js82j2da3b55bc5****.mp4",
     "Format": "mp4",
     "Fps": "30",
     "Height": 960,
     "Size": 1815321,
     "Width": 540,
     "JobId":"ffffffffff"
   },
   {
     "Status": "success",
     "Bitrate": "1575",
     "Definition": "SD",
     "Duration": 15,
     "Encrypt": false,
     "FileUrl": "http://vod.aliyunsample.com/ABEBDE1JSU79FD4D1329/62cb3151eba52js82j2da3b55bc5****.mp4",
     "Format": "mp4",
     "Fps": "30",
     "Height": 960,
     "Size": 3090951,
     "Width": 540,
     "JobId":"ddddddddddd"
   }
  ]
}
```

