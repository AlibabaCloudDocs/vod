# Release notes of the short video SDK for Android

This topic describes the release notes of different versions of the short video SDK for Android.

## Feature updates

|**Release date**|**Version**|**Description**|
|----------------|-----------|---------------|
|2021-04-28|V3.21.0|-   Rounded borders are supported when the camera is used for duet recording.
-   The tools that are used to import High Efficiency Image Coding \(HEIC\) images can be used.
-   The issue is fixed where the memory piles up and the system stops responding during software encoding on specific phone models.
-   The issue is fixed where the camera matrix that is used to crop the preview image may not be updated at the earliest opportunity during custom rendering.
-   The stability of the SDK is improved. |
|2021-03-24|V3.20.0|-   The audio fade effect is added to the editing module.
-   The combined subtitle feature is added to the editing module.
-   The basic editing capability is added to the editing module.
-   The issue is fixed where the screen flickers on specific phone models when you switch between the preview pages of multiple video clips during editing.
-   The issue is fixed where the frame rate that you set for the exported video during editing does not take effect.
-   The issue is fixed where the camera transformation matrix may be empty during custom rendering in the Android system.
-   The stability of the SDK is improved. |
|2021-02-03|V3.19.0|-   The noise reduction feature is added to the editing module.
-   The background image and background color can be set during duet recording and video merging.
-   Audio tracks can be merged during duet recording and video merging.
-   Callbacks for audio data can be invoked during the preview of recording files.
-   The issue is fixed where emojis in subtitles fail to be displayed when the font of the subtitles is enlarged to a specific size in the editing module.
-   The issue is fixed where the halo color changes when a transparent halo effect is added to a watermark or an image.
-   The issue is fixed where added static images are not rotated in the expected angle. |
|2021-01-13|V3.18.1|The issue is fixed where the screen flickers during duet recording in cropping mode.|
|2020-12-31|V3.18.0|-   Audio tracks can be specified during duet recording. For example, you can use the original or recorded audio. You can also mute the audio.
-   The issue is fixed where black bars flicker when the aspect ratio is switched on Android Q phones. |
|2020-12-1|V3.17.1|-   The issue is fixed where Open Graphics Library \(OpenGL\) unexpectedly quits applications on specific phone models after a video is produced.
-   The issue is fixed where custom fonts do not take effect.
-   The issue is fixed where the information about the timestamp and process ID is not written after you call the AlivcSdkCore.setLogPath method. |
|2020-10-30|V3.17.0|-   The package name of the short video SDK for Android is optimized, which reduces the cost of service integration and makes the SDK more user-friendly. The new package name is in the unified format of com.aliyun.svideosdk.\*. For more information about the latest SDK, see [Project configuration](/intl.en-US/Short video SDK/Android short video SDK/Project configuration.md).

To update the existing SDK to the latest version, download the [update tool](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/shortVideo/tool/interface_upgrade.py).

-   The voice effect of lolita is optimized and the voice effects of Chinese dialects are added.
-   The issue is fixed where unexpected quits occur during photo taking in extreme scenarios.
-   The following deprecated interfaces are deleted:
    -   com.error.NativeErrorCode
    -   com.qu.preview.callback.OnNativeReady
    -   com.aliyun.qupai.editor.AliyunIExporter
    -   com.aliyun.qupai.editor.AliyunIPlayer
    -   com.aliyun.qupai.editor.OnPlayCallback
    -   com.aliyun.qupai.editor.OnPreparedListener
    -   com.aliyun.querrorcode.AliyunVideoCoreError |
|2020-09-21|V3.16.2|The Gaussian blur effect on backgrounds is improved.|
|2020-06-23|V3.16.1|-   The issue is fixed where the number of words in each line of the added subtitles is different.
-   The issue is fixed where the subtitles and animated stickers do not move as specified during secondary editing. |
|2020-05-12|V3.16.0|-   The major animation effects are added again.
-   The issue is fixed where intermittent unexpected quits occur when users send feedback online.
-   The issue is fixed where stuttering may occur during the playback of long videos.
-   The issue is fixed where the recording unexpectedly quits due to the incompatibility with specific phone models. |
|2020-03-20|V3.15.0|-   The issue is fixed where stuttering occurs during the playback of produced videos.
-   The issue is fixed where the speed of multiple clips cannot be changed at the same time.
-   The issue is fixed where the exposure area of the front camera of specific phone models is invalid.
-   Two sets of transitions, filter effect transitions, and filters are added based on the standards of producing custom effects.
-   A method is added to modify the parameters of custom effects in real time.
-   The features of custom filters, transition effects, and custom effects are supported. |
|2019-12-27|V3.14.0|-   The SDK is adapted to the Android Q system to improve the performance of recording, editing, and producing videos in the Android Q system.
-   The recording implementation is optimized and the issue of intermittent unexpected quits is fixed.
-   The known memory leaks are fixed and the performance of specific modules is optimized. |
|2019-11-21|V3.13.0|-   The stability and performance of the recording module are optimized.
-   The Render And Compute Everything \(RACE\) engine-based face filters are added to the recording module. |
|2019-09-10|V3.12.0|-   The feature of log analysis is supported. The AlivcSdkCore\#setDebugLoggerLevel\(AlivcDebugLoggerLevel level\) method is added to specify whether to enable the feature. The following three options are provided:
    -   AlivcDLClose: disables the feature of log analysis.
    -   AlivcDLNormal: analyzes warning or error logs. We recommend that you use this option to analyze logs.
    -   AlivcDLAll: analyzes all logs. We recommend that you use this option only for troubleshooting. However, we recommend that you do not use this option in the official release where this option can be used only to analyze the logs of the SDK.
-   The performance of the editing module is improved.
-   The addRunningDisplayMode method is deleted from the editing module.
-   The removeRunningDisplayMode method is deleted from the editing module. |
|2019-07-30|V3.11.0|-   The start and stop speeds of clip recording and the video production speed are improved, which allows smoother clip recording.
-   The granularity and accuracy of the recording progress callback are improved.
-   The transcoding speed in specific scenarios is improved by precisely adjusting the group of pictures \(GOP\) size. |
|2019-06-26|V3.10.5|-   The AliyunIMixRecorder interface is added.
-   The AliyunIMixComposer interface is added. This interface can be used to achieve effects such as picture-in-picture \(PiP\) and left-right split-screen. |
|2019-06-12|V3.10.0|-   The voice effects of the big devil and Minions are added to the editing module. Videos in the MJPEG format can be edited.
-   The compatibility with specific damaged video files is improved for playback during editing.
-   Hardware decoding is supported for High Efficiency Video Coding \(HEVC\) videos during editing and transcoding.
-   The transcoding speed is improved.
-   A method is added to reset the size of the preview window during recording.
-   The issue is fixed where the duration is not accurately displayed for a recorded video clip.
-   Separate interfaces for producing and uploading videos are added.
-   The issue is fixed where a memory leak may occur because specific handles are not released.
-   The draw method is added to forcibly draw a frame during editing. This fixes the issue where the first frame is not drawn during initialization by default. |
|2019-04-24|V3.9.0|-   The voice effect feature is supported with multiple effects, such as lolita, male, reverberation, and echo.
-   The seeking performance during editing is improved. |
|2019-03-01|V3.8.0|-   The playback capability during editing is optimized to ensure smooth playback.
-   The video production speed is improved for the editing module.
-   The preview resolution of recorded videos is optimized.
-   The recording frame rate on low-end devices is improved. |
|2018-12-14|V3.7.7|-   The video resolution is improved without changing the video quality.
-   H.265 videos can be uploaded. |
|2018-11-01|V3.7.5|-   The transition feature is supported with major effects, such as fade, polygon, and blinds.
-   The subtitle animation feature is supported with multiple effects, such as rotation, shifting, scaling, and transparency adjustment.
-   Multiple speed ramps can be added for multiple video clips.
-   The compatibility with GIF images is improved. |
|2018-08-21|V3.6.5.1|-   Copyrighted music from Xiami Music is integrated.
-   A third-party augmented reality \(AR\) facial recognition module is integrated and advanced face and skin filters are added.
-   The issue is fixed where multiple video clips cannot be automatically played after they are uploaded for editing.
-   The pixel buffer can be used to access and render YUV data. |
|2018-07-26|V3.6.5|-   The issue is fixed where specific videos are stuck at 99% during cropping.
-   The issue is fixed where stuttering occurs during the preview of specific cropped videos.
-   The known issues in the editing and upload modules are fixed. |
|2018-06-21|V3.6.0|-   The editing module is rebuilt to improve the performance of transcoding and production.
-   The time effects, including the fast-forward motion, slow motion, looping, and reverse motion effects, are added.
-   The size of video files is reduced without changing the resolution.
-   The resolution of videos that are rendered with effects is improved.
-   The features of audio mixing, audio cropping, and choosing random audio segments are supported.
-   The accuracy of face-tracking stickers is improved. |
|2018-02-09|V3.5.0|-   The magic music feature is added to the recording module.
-   Filters, such as Out of Body, are added. |
|2018-01-03|V3.4.0|-   Thirteen filters are added.
-   The performance of face recognition and tracking is improved. Up to three faces can be recognized and tracked at the same time.
-   The music seeking feature is added to the editing module. This feature allows you to seek to the required point in time.
-   The transition time can be set in the editing module. |
|2017-11-24|V3.3.5|-   The features of producing and uploading videos in the background are added, which improves user experience.
-   The thumbnail can be customized.
-   A method is added to add static stickers to the editing user interface \(UI\). |
|2017-10-25|V3.3.4|-   A method is added to customize the bitrate.
-   An interface for cropping videos is added to the GPU to improve performance.
-   Internal optimization is complete and the known issues are fixed. |
|2017-09-29|V3.3.3|-   The manual focus feature during video recording is optimized.
-   A method is added to instantly enter the editing mode after video cropping.
-   The reporting of unexpected program quits and errors is supported to improve the SDK. |
|2017-08-31|V3.3.2|-   A method is added to set the background color of the cropping and editing UIs.
-   Software encoding is supported.
-   The issue of unexpected quits in Android 8.0 is fixed.
-   The issue is fixed where the uploaded on-premises music cannot be played. |
|2017-08-11|V3.3.1|-   The feature of facial recognition is supported.
-   The resolution of recorded videos is optimized.
-   The issue is fixed where the recording files are oversized.
-   The issue is fixed where a black and unresponsive video screen appears after you switch from the recording UI to the editing UI. |
|2017-07-11|V3.3.0|-   The features of real-time audio mixing and speed ramping are supported.
-   Videos and images can be uploaded at the same time. |
|2017-06-23|V3.2.0|-   The feature of video doodle is supported.
-   The issue is fixed where only rectangular thumbnails can be generated.
-   The issue is fixed where animation effects, such as music video \(MV\) movement, selection, and scaling, are invalid.
-   A method is added to generate thumbnails from non-keyframes. |
|2017-06-16|V3.1.3|-   The error code and error message are added for invalid encoding formats.
-   The issue is fixed where the settings of the cropping area are invalid. The bundleId parameter is replaced with the packageName parameter in the download interface.
-   The encoding format error can be returned by underlying libraries. |

