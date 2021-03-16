# Image overlay

This topic describes the parameters of image overlay. This topic also provides examples of overlay in the full-time interval and overlay in the specified time interval. The following examples show how timeline data is organized for image overlay.

## Overview

Video editing and the two methods about how to use the media editing service are introduced in [Overview](/intl.en-US/Developer Guide/Online editing/Overview.md). You can call the [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md) operation to initiate and implement the media editing service. The timeline is the key data processed by the media editing service and the core object in video editing. The internal parameters of the timeline can be organized in multiple ways to meet requirements in different business scenarios.

## Parameters

|Parameter|Description|
|---------|-----------|
|Coordinates of the image overlaid on the output video|-   X: the horizontal distance between the upper-left corner of the image and the upper-left corner of the output video.
-   Y: the vertical distance between the upper-left corner of the image and the upper-left corner of the output video.

You can set the value to a percentage or the number of pixels.-   If the value is within **0～0.9999**, the percentage of the horizontal or vertical offset distance of the image relative to the width or height of the output video. X indicates the percentage of the width, and Y indicates the percentage of the height.
-   If the value is an integer greater than or equal to 8, the value indicates the number of pixels. |
|Size of the image overlaid on the output video|-   Width: the width of the image overlaid on the output video.
-   Height: the height of the image overlaid on the output video.

You can set the value to a percentage or the number of pixels.-   If the value is within **0～0.9999**, the percentage of the width or height of the image relative to that of the output video. Width indicates the percentage of the width, and Height indicates the percentage of the height.
-   If the value is an integer greater than or equal to 8, the value indicates the number of pixels. |
|Time interval when the image is overlaid on the output video|-   TimelineIn: the start time of the image relative to the timeline.
-   TimelineOut: the end time of the image relative to the timeline. |

## Example of overlay in the full-time interval

This action overlays images on a video from the start time to the end time of the entire video. You do not need to set the `TimelineIn` or `TimelineOut` parameter. The position of the image in the output video is specified by `X` and `Y`. The size of the image in the output video is specified by `Width` and `Height`. Example:

-   Overlay on a single video

    ```
    {
      "VideoTracks": [
          {
              "VideoTrackClips": [
                  {
                      "MediaId": "222d9296e8864746a0b6f32dad6e****"
                  }
              ]
          }
      ],
      "ImageTracks": [
          {
              "ImageTrackClips": [
                  {
                      "ImageId": "001d9296e8864746a0b6f32dad6e****",
                      "Width": 0.1345,
                      "Height": 0.1678,
                      "X": 0.1234,
                      "Y": 0.1234
                  },
                  {
                      "ImageId": "002d9296e8864746a0b6f32dad6e****",
                      "Width": 0.1345,
                      "Height": 0.1678,
                      "X": 0.7234,
                      "Y": 0.7234
                  }
              ]
          }
      ]
    }
    ```

-   Overlay on multiple videos

    ```
    {
      "VideoTracks": [
          {
              "VideoTrackClips": [
                  {
                      "MediaId": "222d9296e8864746a0b6f32dad6e****"
                  },
                  {
                      "MediaId": "333d9296e8864746a0b6f32dad6e****"
                  }
              ]
          }
      ],
      "ImageTracks": [
          {
              "ImageTrackClips": [
                  {
                      "ImageId": "001d9296e8864746a0b6f32dad6e****",
                      "Width": 0.1345,
                      "Height": 0.1678,
                      "X": 0.1234,
                      "Y": 0.1234
                  },
                  {
                      "ImageId": "002d9296e8864746a0b6f32dad6e****",
                      "Width": 0.1345,
                      "Height": 0.1678,
                      "X": 0.7234,
                      "Y": 0.7234
                  }
              ]
          }
      ]
    }
    ```


## Example of overlay in the specified time interval

This action overlays an image on a video in the specified time interval of the video. The position of the image in the output video is specified by `X` and `Y`. The size of the image in the output video is specified by `Width` and `Height`. The following code provides an example on how to overlay two images on a video from the 2nd second to the 100th second:

**Note:** The output video refers to the finally produced video.

-   Overlay on a single video

    -   By default, if the `TimelineIn` parameter is not set, the image is overlaid from the start time of the video.
    -   By default, if the `TimelineOut` parameter is not set, the image remains overlaid until the video ends.
    -   If the `TimelineOut` value exceeds the total duration of a single video, the excess time interval is automatically excluded and the image remains overlaid until the end time of the video.
    ```
    {
      "VideoTracks": [
          {
              "VideoTrackClips": [
                  {
                      "MediaId": "222d9296e8864746a0b6f32dad6e****"
                  }
              ]
          }
      ],
      "ImageTracks": [
          {
              "ImageTrackClips": [
                  {
                      "ImageId": "001d9296e8864746a0b6f32dad6e****",
                      "Width": 0.1345,
                      "Height": 0.1678,
                      "X": 0.1234,
                      "Y": 0.1234,
                      "TimelineIn":2,
                      "TimelineOut":100
                  },
                  {
                      "ImageId": "002d9296e8864746a0b6f32dad6e****",
                      "Width": 0.1345,
                      "Height": 0.1678,
                      "X": 0.7234,
                      "Y": 0.7234,
                      "TimelineIn":2,
                      "TimelineOut":100
                  }
              ]
          }
      ]
    }
    ```

-   Overlay on multiple videos

    -   By default, if the `TimelineIn` parameter is not set, the image is overlaid from the start time of the video.
    -   By default, if the `TimelineOut` parameter is not set, the image remains overlaid until the video ends.
    -   If the `TimelineOut` value exceeds the total duration of a single video, the excess time interval is automatically excluded and the image remains overlaid until the end time of the video.
    If a video track consists of multiple video mezzanine files at different resolutions, take note of the following items:

    -   The width of the output video is the maximum width of the video mezzanine files.
    -   The height of the output video is the maximum height of the video mezzanine files.
    -   The video image is processed in padding and scaling mode. First, black borders are added to the video image to ensure that the aspect ratio remains unchanged. Then, the video image is scaled up to the width and height of the output video.
    -   The duration of the output video equals that of the video track.
    ```
    {
      "VideoTracks": [
          {
              "VideoTrackClips": [
                  {
                      "MediaId": "222d9296e8864746a0b6f32dad6e****"
                  },
                  {
                      "MediaId": "333d9296e8864746a0b6f32dad6e****"
                  }
              ]
          }
      ],
      "ImageTracks": [
          {
              "ImageTrackClips": [
                  {
                      "ImageId": "001d9296e8864746a0b6f32dad6e****",
                      "Width": 0.1345,
                      "Height": 0.1678,
                      "X": 0.1234,
                      "Y": 0.1234,
                      "TimelineIn":2,
                      "TimelineOut":100
                  },
                  {
                      "ImageId": "002d9296e8864746a0b6f32dad6e****",
                      "Width": 0.1345,
                      "Height": 0.1678,
                      "X": 0.7234,
                      "Y": 0.7234,
                      "TimelineIn":2,
                      "TimelineOut":100
                  }
              ]
          }
      ]
    }
    ```


