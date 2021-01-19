# Cutting and merging

This topic describes how to merge multiple videos as a whole, cut a video with the starting part, ending part, or middle part retained, and merge parts of multiple videos. Timeline data is used to cut and merge videos.

## Overview

Video editing and the two methods about how to use the media editing service are introduced in [Overview](/intl.en-US/Developer Guide/Online editing/Overview.md). You can call the [ProduceEditingProjectVideo](/intl.en-US/API Reference/Video editing/ProduceEditingProjectVideo.md) operation to initiate and implement the media editing service. The timeline is the key data processed by the media editing service and the core object in video editing. The internal parameters of the timeline can be organized in multiple ways to meet requirements in different business scenarios.

## Example of merging multiple videos as a whole

This action merges multiple videos as a whole in sequence. You do not need to specify the start or end time when you merge the videos. The following code provides an example on how to merge multiple videos as a whole in sequence:

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "4bcf9b4d7cf14dc7b83b0e801cbe****"
                },
                {
                    "MediaId": "789f9b4d7cf14dc7b83b0e801cbe****"
                }
            ]
        }
    ]
}
```

## Example of cutting a video with the starting part retained

This action does not require you to specify the start time when you cut a video. By default, the video is cut from the start time of the video. You need only to specify the end time when you cut the video. The following code provides an example on how to extract the first 5 seconds of a video:

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "4bcf9b4d7cf14dc7b83b0e801cbe****",
                    "Out": 5
                }
            ]
        }
    ]
}
```

## Example of cutting a video with the ending part retained

This action does not require you to specify the end time when you cut a video. By default, the video is cut to the end time of the video. You need only to specify the start time when you cut the video. The following code provides an example on how to extract the last 10 seconds of a video:

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "4bcf9b4d7cf14dc7b83b0e801cbe****",
                    "In": 10
                }
            ]
        }
    ]
}
```

## Example of cutting a video with the middle part retained

This action requires you to specify the start time \(the In parameter\) and end time \(the Out parameter\) when you cut a video. Only the part between the start time and end time is retained. The following code provides an example on how to cut a video with the middle part retained:

**Note:** If the Out value exceeds the video duration, the end time of the video is used as the Out value.

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "4bcf9b4d7cf14dc7b83b0e801cbe****",
                    "In": 5,
                    "Out": 10
                }
            ]
        }
    ]
}
```

## Example of merging parts of multiple videos

This action extracts multiple parts from multiple videos and merges the extracted parts. The following code provides an example on how to merge two parts of `4bcf9b4d7cf14dc7b83b0e801cbe****` and one part of `789f9b4d7cf14dc7b83b0e801cbe****` based on the order of the array in sequence:

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "4bcf9b4d7cf14dc7b83b0e801cbe****",
                    "In": 12,
                    "Out": 16
                },{
                    "MediaId": "4bcf9b4d7cf14dc7b83b0e801cbe****",
                    "In": 4,
                    "Out": 7
                },{
                    "MediaId": "789f9b4d7cf14dc7b83b0e801cbe****",
                    "In": 12,
                    "Out": 20
                }
            ]
        }
    ]
}
```

