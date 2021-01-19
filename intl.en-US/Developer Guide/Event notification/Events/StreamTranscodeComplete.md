# StreamTranscodeComplete

This topic describes the StreamTranscodeComplete event as well as its notification content and sample callbacks.

## Event type

StreamTranscodeComplete

## Event description

The StreamTranscodeComplete event is generated after a video stream in a single definition and format \(such as an SD stream in the MP4 format\) is transcoded. A video stream in a single resolution can be played immediately after the video stream is transcoded in at least one format.

**Note:** If you have enabled URL signing, you must generate your own auth\_key to access the playback URL of the video. Otherwise, the `HTTP 403` error code is returned for your request. For more information about URL signing, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL signing.md).

## Event notification content

|Field|Type|Required|Description|
|-----|----|--------|-----------|
|EventTime|String|Yes|The time when the event is generated. The time is displayed in the yyyy-MM-ddTHH:mm:ssZ format and in UTC.|
|EventType|String|Yes|The event type. The value is **StreamTranscodeComplete**.|
|VideoId|String|Yes|The ID of the video.|
|Status|String|Yes|Indicates whether the video stream is transcoded. Valid values:-   **success**: The video stream is transcoded.
-   **fail**: The video stream failed to be transcoded. |
|Bitrate|String|No|The bitrate of the video stream. Unit: Kbit/s.|
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
|Format|String|No|The format of the video stream. Valid values:-   **mp4**
-   **m3u8** |
|Fps|String|No|The frame rate of the video stream, in frames per second.|
|Height|Long|No|The height of the video stream. Unit: px.|
|Size|Long|No|The size of the video stream. Unit: bytes.|
|Width|Long|No|The width of the video stream. Unit: px.|
|JobId|String|No|The ID of the transcoding job.|
|Extend|String|No|The user-defined parameter that is returned in the pass-through mode in callbacks. For more information, see [t1235674.md\#section\_6fg\_qll\_v3w](/intl.en-US/API Reference/Appendix/Request parameters.md).|

## Sample callbacks

Description:

-   For an HTTP callback, the following example is the body of the HTTP POST request.
-   For an MNS callback, the following example is the message body.

```
{ 
   "EventTime": "2017-03-20T07:49:17Z",
   "EventType": "StreamTranscodeComplete", 
   "VideoId": "43q9fj74hdf****", 
   "Status": "success",
   "Bitrate": "925",
   "Definition": "LD",
   "Duration": 15.0,
   "Encrypt": false,
   "FileUrl": "http://vod.aliyunsample.com/DBEBDEAJS73J79BE4D1329/52a53151eba5js73ke2da3b55bc5****.mp4",
   "Format": "mp4",
   "Fps": "30",
   "Height": 960,
   "Size": 1815321,
   "Width": 540,
   "JobId":"ddddddddddd",
   "Extend":"test data"
}
```

