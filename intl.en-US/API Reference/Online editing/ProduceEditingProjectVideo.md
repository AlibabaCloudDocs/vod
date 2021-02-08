# ProduceEditingProjectVideo

Produces a video from one or more mezzanine files. You can directly submit mezzanine files by specifying the Timeline parameter. Alternatively, you can submit mezzanine files after you create an online editing project.

**Note:**

-   This operation returns only the submission result of a video production task. When the submission result is returned, video production may still be in progress. After a video production task is submitted, the task is queued in the background for asynchronous processing.
    -   The mezzanine files that are referenced in the timeline of an online editing project can be materials from media assets or videos in the media library.
-   Videos are produced based on the ProjectId and Timeline parameters. Take note of the following items when you specify the parameters:
    -   You must specify at least one of the ProjectId and Timeline parameters. Otherwise, video production fails.
    -   If you specify only the Timeline parameter, the system automatically creates an online editing project with the specified timeline. Then, the system obtains the mezzanine files that are referenced in the timeline and produces a video from the mezzanine files.
    -   If you specify only the ProjectId parameter, the system obtains the latest timeline of the specified project and produces a video based on the timeline.
    -   If you specify both the ProjectId and Timeline parameters, the system produces a video based on the specified timeline and updates the timeline and mezzanine files for the specified online editing project. If you specify other parameters, the system also updates related settings for the online editing project.
    -   You can apply effects to the video to be produced. For more information, see [Special effects](~~69082~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=vod&api=ProduceEditingProjectVideo&type=RPC&version=2017-03-21)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ProduceEditingProjectVideo|The operation that you want to perform. Set the value to **ProduceEditingProjectVideo**. |
|ProjectId|String|No|fb2101bf24b\*\*\*\*\*4cb318787dc|The ID of the online editing project. |
|Timeline|String|No|\{"VideoTracks":\[\{"VideoTrackClips":\[\{"MediaId":"cc3308ac5\*\*\*\*\*9615a54328bc3443"\},\{"MediaId":"da87a9cff64\*\*\*\*\*5cd88bc6d8326e4"\}\]\}\]\}|The timeline of the online editing project, in JSON format. For more information about the structure, see [Timeline](~~52839~~). |
|Title|String|No|Test of video production|The title of the online editing project. |
|Description|String|No|Description|The description of the online editing project. |
|CoverURL|String|No|https://\*\*\*\*.com/6AB4D0E1E1C7446888351\*\*\*\*.png|The thumbnail URL of the online editing project. |
|MediaMetadata|String|No|\{"Description": "Description of the produced video", "Title": "User data-based production test"\}|The metadata of the produced video, in JSON format. For more information about the structure, see [MediaMetadata](~~52839~~). |
|ProduceConfig|String|No|\{"TemplateGroupId":"6d11e25ea30a\*\*\*\*\*4c465435c74"\}|The configuration of video production, in JSON format. For more information about the structure, see [ProduceConfig](~~52839~~). |
|UserData|String|No|\{"Extend":\{"width":1280,"id":"028a8e56b\*\*\*\*\*1ebf6bb7afc74","height":720\},"MessageCallback":\{"CallbackURL":"https://xxxxx.com/2016-08-15/proxy/httpcallback/testcallback/","CallbackType":"http"\}\}|The custom configuration, such as the callback configuration. The value is a JSON-formatted string. For more information about the structure, see [UserData](~~86952~~).

 **Note:** To use the MessageCallback parameter, you must set an HTTP callback URL and select a callback event type in the ApsaraVideo VOD console. Otherwise, the callback configuration does not take effect. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MediaId|String|006204a11bb3\*\*\*\*\*86bb25491f95f|The ID of the produced video.

 **Note:**

-   This operation returns the ID of the produced video in synchronous mode.
-   If this operation returns the MediaId parameter, the video production task is being asynchronously processed. |
|ProjectId|String|fb2101bf24b\*\*\*\*\*4cb318787dc|The ID of the online editing project. |
|RequestId|String|25818875-5F78-4A\*\*\*\*\*F6-D7393642CA58|The ID of the request. |

**Note:** ApsaraVideo VOD sends a FileUploadComplete event notification after video production is complete, which is similar to the action that is performed after video upload. After the produced video is transcoded, ApsaraVideo VOD sends the StreamTranscodeComplete and TranscodeComplete event notifications.

## Examples

Sample requests

```
https://vod.aliyuncs.com/?Action=ProduceEditingProjectVideo
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ProduceEditingProjectVideoResponse>
	  <RequestId>25818875-5F78-4A*****F6-D7393642CA58</RequestId>
	  <MediaId>006204a11bb3*****86bb25491f95f</MediaId>
	  <ProjectId>fb2101bf24b*****4cb318787dc</ProjectId>
</ProduceEditingProjectVideoResponse>
```

`JSON` format

```
{
    "RequestId": "25818875-5F78-4A*****F6-D7393642CA58",
    "MediaId": "006204a11bb3*****86bb25491f95f",
    "ProjectId":"fb2101bf24b*****4cb318787dc"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/vod).

## SDK examples

We recommend that you use a [server SDK](~~101789~~) to call this operation. For more information about the sample code that is used to call this operation in various languages, see the following topics:

-   [Java](~~61063~~)
-   [Python](~~61054~~)
-   [PHP](~~61069~~)
-   [.NET](~~84750~~)
-   [Node.js](~~101396~~)
-   [Go](~~101411~~)
-   [C/C++](~~101261~~)

