# Text overlay

This topic describes the parameters of text overlay. This topic also provides examples of overlay in the full-time interval and overlay in the specified time interval. The following examples show how timeline data is organized for text overlay.

## Overview

Video editing and the two methods about how to use the media editing service are introduced in [Overview](/intl.en-US/Developer Guide/Online editing/Overview.md). You can call the [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md) operation to initiate and implement the media editing service. The timeline is the key data processed by the media editing service and the core object in video editing. The internal parameters of the timeline can be organized in multiple ways to meet requirements in different business scenarios.

## Parameters

|Parameter|Description|
|---------|-----------|
|Coordinates of the text overlaid on the output video|-   X : the horizontal distance between the upper-left corner of the text and the upper-left corner of the output video.
-   Y: the vertical distance between the upper-left corner of the text and the upper-left corner of the output video.

You can set the value to a percentage or the number of pixels.-   If the value is within **0～0.9999**, the percentage of the horizontal or vertical offset distance of the text relative to the width or height of the output video. X indicates the percentage of the width, and Y indicates the percentage of the height.
-   If the value is an integer greater than or equal to 8, the value indicates the number of pixels. |
|Text attributes|-   Content: the text content.
-   Font: the font used by the text. Default value: SimSun.

Valid values:

    -   SimSun
    -   WenQuanYi Zen Hei
    -   WenQuanYi Zen Hei Mono
    -   WenQuanYi Zen Hei Sharp
    -   Yuanti SC Bold
    -   Yuanti SC Light
    -   Yuanti SC Regular
-   FontSize: the font size. Unit: px. Default value: 20.
-   FontColor: the color of the font, which is a hexadecimal color value. The value starts with a number sign \(\#\). Example: \#FFFFFF. Default value: \#FFFFFFFont.
-   FontColorOpacity: the transparency of the font color. Valid values: 0 to 1. A value of 1 indicates that the color is fully opaque. A value of 0 indicates that the color is fully transparent. Default value: 1.
-   FontFace: the style of the font and contains the following parameters:
    -   Bold: specifies whether the font is bold. Default value: false.
    -   Italic: specifies whether the font is italic. Default value: false.
    -   Underline: specifies whether the font is underlined. Default value: false. |
|Time interval when the text is overlaid on the output video|-   TimelineIn: the start time of the text relative to the timeline.
-   TimelineOut: the end time of the text relative to the timeline. |

## Example of overlay in the full-time interval

This action overlays text on a video from the start time to the end time of the entire video. You do not need to set the `TimelineIn` or `TimelineOut` parameter. The position of the text in the output video is specified by `X` and `Y`. Example:

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "ea9a6f9bdb68419abfd36a7113cf****",
                    "Effects": [
                        {
                            "Type": "Text",
                            "X": 31,
                            "Y": 93,
                            "Font": "WenQuanYi Zen Hei Mono",
                            "Content": "Test Text Test Text",
                            "FontSize": 26,
                            "FontColorOpacity": 0.2,
                            "FontColor": "#000000",
                            "FontFace": {
                                "Bold": true,
                                "Italic": false,
                                "Underline": false
                            }
                        },
                        {
                            "Type": "Text",
                            "X": 30,
                            "Y": 92,
                            "Font": "WenQuanYi Zen Hei Mono",
                            "Content": "Test Text Test Text",
                            "FontSize": 26,
                            "FontColorOpacity": 1,
                            "FontColor": "#FFFFFF"
                        },
                        {
                            "Type": "Text",
                            "X": 0.8123,
                            "Y": 0.7896,
                            "Font": "WenQuanYi Zen Hei Mono",
                            "Content": "Test Text Test Text",
                            "FontSize": 26,
                            "FontColorOpacity": 0.2,
                            "FontColor": "#000000"
                        },
                        {
                            "Type": "Text",
                            "X": 0.8223,
                            "Y": 0.7796,
                            "Font": "WenQuanYi Zen Hei Mono",
                            "Content": "Test Text Test Text",
                            "FontSize": 26,
                            "FontColorOpacity": 1,
                            "FontColor": "#FFFFFF"
                        }
                    ]
                }
            ]
        }
    ]
}
```

## Overlay in the specified time interval

This action overlays text on a video in the specified time interval of the video. The position of the text in the output video is specified by `X` and `Y`. The following code provides an example on how to overlay text on a video from the 0th second to the 5th second and from the 5th second to the 10th second:

-   By default, if the `TimelineIn` parameter is not set, the text is overlaid from the start time of the video.
-   By default, if the `TimelineOut` parameter is not set, the text remains overlaid until the video ends.
-   If the `TimelineOut` value exceeds the total duration of a single video, the excess time interval is automatically excluded and the text remains overlaid until the end time of the video.

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "ea9a6f9bdb68419abfd36a7113cf****",
                    "Effects": [
                        {
                            "Type": "Text",
                            "X": 31,
                            "Y": 93,
                            "TimelineIn": 0,
                            "TimelineOut": 5,
                            "Font": "WenQuanYi Zen Hei Mono",
                            "Content": "Test Text Test Text",
                            "FontSize": 26,
                            "FontColorOpacity": 0.2,
                            "FontColor": "#000000",
                            "FontFace": {
                                "Bold": true,
                                "Italic": false,
                                "Underline": false
                            }
                        },
                        {
                            "Type": "Text",
                            "X": 30,
                            "Y": 92,
                            "TimelineIn": 0,
                            "TimelineOut": 5,
                            "Font": "WenQuanYi Zen Hei Mono",
                            "Content": "Test Text Test Text",
                            "FontSize": 26,
                            "FontColorOpacity": 1,
                            "FontColor": "#FFFFFF"
                        },
                        {
                            "Type": "Text",
                            "X": 1124,
                            "Y": 516,
                            "TimelineIn": 5,
                            "TimelineOut": 10,
                            "Font": "WenQuanYi Zen Hei Mono",
                            "Content": "Test Text Test Text",
                            "FontSize": 26,
                            "FontColorOpacity": 0.2,
                            "FontColor": "#000000"
                        },
                        {
                            "Type": "Text",
                            "X": 1123,
                            "Y": 515,
                            "TimelineIn": 5,
                            "TimelineOut": 10,
                            "Font": "WenQuanYi Zen Hei Mono",
                            "Content": "Test Text Test Text",
                            "FontSize": 26,
                            "FontColorOpacity": 1,
                            "FontColor": "#FFFFFF"
                        }
                    ]
                }
            ]
        }
    ]
}
```

