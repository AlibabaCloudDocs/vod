# Audio processing

This topic describes how to mute an entire video, mute a specified part of a video, extract audio clips, mute a video and dub the video with a full audio resource, mute a video and dub the video with a specified part of an audio resource, adjust the volume of a video and dub the video with an audio resource whose volume is also adjusted, merge audio clips, mix multiple audio tracks, perform complex audio processing, and organize timeline data for audio processing.

## Overview

Video editing and the two methods about how to use the media editing service are introduced in [Overview](/intl.en-US/Developer Guide/Online editing/Overview.md). You can call the [ProduceEditingProjectVideo](/intl.en-US/API Reference/Video editing/ProduceEditingProjectVideo.md) operation to initiate and implement the media editing service. The timeline is the key data processed by the media editing service and the core object in video editing. The internal parameters of the timeline can be organized in multiple ways to meet requirements in different business scenarios.

## Example of muting an entire video

This action turns off the sound of an entire video. The following example shows how to use the volume effect to mute a video. The `Gain` parameter indicates the volume gain. A value of **0** indicates that the video is muted.

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "3f7e62d41a334dec9ac802b0f165****",
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "0"
                        }
                    ]
                }
            ]
        }
    ]
}
```

## Example of muting a specified part of a video

Compared with the parameters used to mute an entire video, this action adds the In and Out parameters to the volume effect. The following code provides an example on how to mute a video from the 8th second to the 60th second and retain the volume of other parts of the video:

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "3f7e62d41a334dec9ac802b0f165****",
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "0",
                            "In": 8,
                            "Out": "60"
                        }
                    ]
                }
            ]
        }
    ]
}
```

## Example of extracting the audio

In some scenarios, you must extract the audio from a video as a separate audio resource. You can create an audio track by passing in the video as an audio track clip. In the following example, b3f37e05512043f49f697f7425b9\*\*\*\* is the ID of a video with audio.

```
{
    "AudioTracks": [
        {
            "AudioTrackClips": [
                {
                    "MediaId": "b3f37e05512043f49f697f7425b9****"
                }
            ]
        }
    ]
}
```

## Example of muting a video and dubbing the video with a full audio resource

This action mutes a video and dubs the video with a full audio resource to generate a new video. This is a typical dubbing scenario. The following code provides an example on how to mute a video and dub the video with a full audio resource:

-   The clips related to audio processing are added to AudioTracks.
-   The `TimelineIn` parameter is set to 5, which indicates that the output video is dubbed with the audio from the 5th second of the video.
-   By default, if the `TimelineOut` parameter is not specified, the output video is dubbed with the full audio. If the output video ends but the audio does not end, the audio is truncated and the playback stops where the output video track ends.

**Note:** You can add audio-only resources or video resources with audio to AudioTrackClips.

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "3f7e62d41a334dec9ac802b0f165****",
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "0"
                        }
                    ]
                }
            ]
        }
    ],
    "AudioTracks": [
        {
            "AudioTrackClips": [
                {
                    "MediaId": "4a71744998414cbe8ea1976435a7****",
                    "TimelineIn":5
                }
            ]
        }
    ]
}
```

## Example of muting a video and dubbing it with the specified part of an audio resource

After you mute a video, you can dub the video with the specified part of an audio resource by specifying the In and Out parameters for the audio resource. The following code provides an example on how to extract the part from the 10th second to the 20th second \(a 10-second audio track clip\) from an audio resource and dub a video with the audio track clip from the 5th second of the video:

**Note:** You can add audio-only resources or video resources with audio to AudioTrackClips.

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "3f7e62d41a334dec9ac802b0f165****",
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "0"
                        }
                    ]
                }
            ]
        }
    ],
    "AudioTracks": [
        {
            "AudioTrackClips": [
                {
                    "MediaId": "4a71744998414cbe8ea1976435a7****",
                    "In":10,
                    "Out":20,
                    "TimelineIn":5
                }
            ]
        }
    ]
}
```

## Example of adjusting the volume of a video and dubbing the video with an audio resource whose volume is also adjusted

You can use the volume effect to specify the volume. In the volume effect, the `Gain` parameter indicates the volume gain.

Valid values of the Gain parameter:

-   0: The video or audio is muted.
-   1: The original volume is used.
-   A value between 0 and 1: The volume is lower than the original volume. The smaller the value, the lower the volume.
-   A value greater than 1: The volume is higher than the original volume. The larger the value, the higher the volume.

**Note:** You can add audio-only resources or video resources with audio to AudioTrackClips.

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "3f7e62d41a334dec9ac802b0f165****",
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "0.5"
                        }
                    ]
                }
            ]
        }
    ],
    "AudioTracks": [
        {
            "AudioTrackClips": [
                {
                    "MediaId": "4a71744998414cbe8ea1976435a7****",
                    "In":10,
                    "Out":20,
                    "TimelineIn":5,
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "2"
                        }
                    ]
                }
            ]
        }
    ]
}
```

## Example of merging audio clips

The preceding examples involve video tracks. Online editing also allows you to process audio-only tracks. The following code provides an example on how to extract specified parts from two audio resources in the same audio track and merge the extracted parts in sequence to generate a 30-second audio resource:

**Note:** You can add audio-only resources or video resources with audio to AudioTrackClips.

```
{
    "AudioTracks": [
        {
            "AudioTrackClips": [
                {
                    "MediaId": "b3f37e05512043f49f697f7425b9****",
                    "In": 100,
                    "Out": 120
                },
                {
                    "MediaId": "ab654a04ce554e4f806b5f9e5a34****",
                    "In": 50,
                    "Out": 60
                }
            ]
        }
    ]
}
```

## Example of mixing multiple audio tracks

In addition to merging audio in the same audio track, online editing allows you to mix multiple audio tracks. The following code provides an example on how to mix two audio tracks to generate a 20-second audio:

**Note:** You can add audio-only resources or video resources with audio to AudioTrackClips.

```
{
    "AudioTracks": [
        {
            "AudioTrackClips": [
                {
                    "MediaId": "b3f37e05512043f49f697f7425b9****",
                    "In": 100,
                    "Out": 120,
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "2"
                        }
                    ]
                }
            ]
        },
        {
            "AudioTrackClips": [
                {
                    "MediaId": "ab654a04ce554e4f806b5f9e5a34****",
                    "In": 50,
                    "Out": 60,
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "1"
                        }
                    ]
                }
            ]
        }
    ]
}
```

## Example of performing complex audio processing

This action allows you to dub a video with multiple audio tracks that are mixed. In the following example, you mute a specified part of a video, adjust the volume of another specified part of the video, and dub the video with multiple audio tracks that are mixed. Perform the following operations:

1.  Mute the 3f7e62d41a334dec9ac802b0f165\*\*\*\* video from the 50th second to the 75th second. Extract the clip from the 100th second to the 120th second from the b3f37e05512043f49f697f7425b9\*\*\*\* audio. Double the volume of the clip, and add the clip to the video that starts from the 50th second to the 70th second. Extract the clip from the 150th second to the 160th second from the ab654a04ce554e4f806b5f9e5a34\*\*\*\* audio. Then, add the clip to the video that starts from the 65th second to the 75th second.
2.  The volume remains unchanged in video 3f7e62d41a334dec9ac802b0f165\*\*\*\* except for the parts from the 50th second to the 75th second and from the 120th second to the 125th second.

**Note:** You can add audio-only resources or video resources with audio to AudioTrackClips.

The following code provides an example on how to perform complex audio processing:

```
{
    "VideoTracks": [
        {
            "VideoTrackClips": [
                {
                    "MediaId": "3f7e62d41a334dec9ac802b0f165****",
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "0",
                            "In": 50,
                            "Out": "75"
                        },
                        {
                            "Type": "Volume",
                            "Gain": "0.8",
                            "In": 120,
                            "Out": "125"
                        },

                    ]
                }
            ]
        }
    ],
    "AudioTracks": [
        {
            "AudioTrackClips": [
                {
                    "MediaId": "b3f37e05512043f49f697f7425b9****",
                    "In": 100,
                    "Out": 120,
                    "TimelineIn":50
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "2"
                        }
                    ]
                }
            ]
        },
        {
            "AudioTrackClips": [
                {
                    "MediaId": "ab654a04ce554e4f806b5f9e5a34****",
                    "In": 150,
                    "Out": 160,
                    "TimelineIn":65
                    "Effects": [
                        {
                            "Type": "Volume",
                            "Gain": "1"
                        }
                    ]
                }
            ]
        }
    ]
}
```

