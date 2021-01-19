# Short video SDK for Android

This topic describes the release notes of different versions of the short video SDK for Android.

## Short video SDK Pro for Android

|**Release date**|**Version**|**Description**|
|----------------|-----------|---------------|
|2020-10-30|V3.17.0|-   The package name of the short video SDK for Android is optimized, which reduces the cost of service integration and makes the SDK more user-friendly. The new package name is in the unified format of com.aliyun.svideosdk. \*. For more information about the latest API operations, see [Project configuration](/intl.en-US/Short video SDK/Android short video SDK/Project configuration.md).

If you want to upgrade the existing API to the latest version, download the [upgrade tool](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/shortVideo/tool/interface_upgrade.py).

-   The sound effect of lolita is optimized and the sound effects of Chinese dialects are added.
-   The issue of unexpected quits during photo taking in extreme scenarios is fixed.
-   The following deprecated operations that are no longer needed are deleted:
    -   com.error.NativeErrorCode
    -   com.qu.preview.callback.OnNativeReady
    -   com.aliyun.qupai.editor.AliyunIExporter
    -   com.aliyun.qupai.editor.AliyunIPlayer
    -   com.aliyun.qupai.editor.OnPlayCallback
    -   com.aliyun.qupai.editor.OnPreparedListener
    -   com.aliyun.querrorcode.AliyunVideoCoreError |
|2020-09-21|V3.16.2|The effect of the Gaussian blur background is optimized.|
|2020-06-23|V3.16.1|-   The issue is fixed where the number of words is different in different lines of the added subtitles.
-   The issue is fixed where the subtitles and animated stickers do not correctly move during secondary editing. |
|2020-05-12|V3.16.0|-   The mainstream animation effects are added again.
-   The issue of intermittent unexpected quits that users report online is fixed.
-   The issue is fixed where freezes may occur during the playback of long videos.
-   The issue is fixed where the recording unexpectedly quits due to incompatibility with some phone models. |
|2020-03-20|V3.15.0|-   The issue is fixed where freezes occur during the playback of produced videos.
-   The issue is fixed where the speed of multiple clips cannot be changed at the same time.
-   The issue is fixed where the exposure area of the front camera of some phone models is invalid.
-   Two sets of transitions, filter effect transitions, and filter effects are added based on the specifications for producing custom effects.
-   An operation is added for modifying the parameters of custom effects in real time.
-   The features of custom filters, transition effects, and custom effects are supported. |
|2019-12-27|V3.14.0|-   The SDK is adapted to the Android Q system to improve the performance of recording, editing, and generating videos in the Android Q system.
-   The recording implementation is optimized and the issue of intermittent unexpected quits is fixed.
-   The known memory leaks are fixed and the performance of some modules is optimized. |
|2019-11-21|V3.13.0|-   The stability and performance of the recording module are optimized.
-   The Render And Compute Everything \(RACE\) engine-based face filters are added to the recording module. |
|2019-09-10|V3.12.0|-   The feature of log analysis is supported. The AlivcSdkCore\#setDebugLoggerLevel\(AlivcDebugLoggerLevel level\) operation is added for specifying whether to enable the feature. The following three options are provided:
    -   AlivcDLClose: Disable the feature of log analysis.
    -   AlivcDLNormal: Analyze warning or error logs. We recommend that you use this option to analyze logs.
    -   AlivcDLAll: Analyze all logs. We recommend that you use this option only for troubleshooting. We recommend that you do not use this option in the official release. You can only use this option to analyze logs of the SDK.
-   The performance of the editing module is improved.
-   The addRunningDisplayMode operation is deleted from the editing module.
-   The removeRunningDisplayMode operation is deleted from the editing module. |
|2019-07-30|V3.11.0|-   The start and stop speeds of clip recording and the video production speed are improved, which enables smoother clip recording.
-   The granularity and accuracy of the recording progress callback are improved.
-   The transcoding speed in some scenarios is improved by precisely adjusting the group of pictures \(GOP\) size. |
|2019-06-26|V3.10.5|-   The AliyunIMixRecorder operation is added.
-   The AliyunMixComposer operation is added. This operation can be used to achieve effects such as picture-in-picture and left-right split-screen. |
|2019-06-12|V3.10.0|-   The sound effects of the big devil and Minions are added to the editing module. Videos in the MJPEG format can be edited.
-   The compatibility with some damaged video files is improved for playback during editing.
-   Hardware decoding is supported for HEVC videos during editing and transcoding.
-   The transcoding speed is improved.
-   An operation is added for resetting the size of the preview window during recording.
-   The issue is fixed where the duration is incorrectly displayed for a recorded video clip.
-   Separate operations for producing and uploading videos are added.
-   The issue is fixed where a memory leak may occur because some handles are not released.
-   The draw method is added to forcibly draw a frame during editing. This fixes the issue where the first frame is not drawn during initialization by default. |
|2019-04-24|V3.9.0|-   The sound effect feature is supported with multiple effects, such as lolita, uncle, reverberation, and echo.
-   The seeking performance during editing is improved. |
|2019-03-01|V3.8.0|-   The playback capability during editing is optimized to ensure smooth playback.
-   The video production speed is improved for the editing module.
-   The preview resolution of recorded videos is optimized.
-   The recording frame rate on low-end devices is improved. |
|2018-12-14|V3.7.7|-   The video resolution is improved without changing the video quality.
-   H.265 videos can be uploaded. |
|2018-11-01|V3.7.5|-   The transition feature is supported with mainstream effects, such as fade, polygon, and blinds.
-   The subtitle animation feature is supported with multiple effects, such as rotation, shifting, scaling, and transparency adjustment.
-   Multiple speed ramps can be added for multiple video clips.
-   The compatibility with GIF images is improved. |
|2018-08-21|V3.6.5.1|-   Copyrighted music from Xiami Music is integrated.
-   A third-party AR facial recognition module is integrated and advanced face and skin filters are added.
-   The issue is fixed where multiple video clips cannot be automatically played after they are uploaded for editing.
-   The pixel buffer can be used to access and render YUV data. |
|2018-07-26|V3.6.5|-   The issue is fixed where some videos are stuck at 99% during cropping.
-   The issue is fixed where freezes occur during the preview of some cropped videos.
-   The known bugs in the editing and upload modules are fixed. |
|2018-06-21|V3.6.0|-   The editing module is rebuilt to improve the performance of transcoding and production.
-   The time effects, including the fast-forward motion, slow motion, looping, and reverse motion effects, are added.
-   The video file size is reduced without changing the resolution.
-   The resolution of videos that are rendered with effects is improved.
-   The features of audio mixing, audio cropping, and choosing random audio segments are supported.
-   The tracking effect of face stickers is improved. |
|2018-02-09|V3.5.0|-   The magic music feature is added to the recording module.
-   Filters, such as trance and phantom, are added. |
|2018-01-03|V3.4.0|-   Thirteen filters are added.
-   The performance of face recognition and tracking is improved. Up to three faces can be recognized and tracked at the same time.
-   The music seeking feature is added to the editing module, which allows you to seek to the required point in time.
-   The transition time can be set in the editing module. |
|2017-11-24|V3.3.5|-   The features of producing and uploading videos in the background are added, which improves user experience.
-   The thumbnail can be customized.
-   An operation is added for adding static stickers to the editing UI. |
|2017-10-25|V3.3.4|-   An operation is added for customizing the bitrate.
-   An operation for cropping videos is added to the GPU to improve performance.
-   Internal optimization is completed and the known issues are fixed. |
|2017-09-29|V3.3.3|-   The manual focus feature during video recording is optimized.
-   An operation is added for instantly accessing the editing mode after video cropping.
-   The reporting of unexpected program quits and errors is supported to improve the SDK. |
|2017-08-31|V3.3.2|-   An operation is added for setting the background color of the cropping and editing UIs.
-   Software encoding is supported.
-   The issue of unexpected quits in Android 8.0 is fixed.
-   The bug is fixed where locally uploaded music cannot be played. |
|2017-08-11|V3.3.1|-   The feature of facial recognition is supported.
-   The resolution of recorded videos is optimized.
-   The issue of oversized recording files is fixed.
-   The bug is fixed where a black and unresponsive video screen appears after you switch from the recording UI to the editing UI. |
|2017-07-11|V3.3.0|-   The features of real-time audio mixing and speed ramping are supported.
-   Videos and images can be uploaded at the same time. |
|2017-06-23|V3.2.0|-   The feature of video doodle is supported.
-   The issue is fixed where only rectangular thumbnails can be generated.
-   The issue is fixed where animation effects, such as music video movement, selection, and scaling, are invalid.
-   An operation is added for retrieving non-keyframe thumbnails. |
|2017-06-16|V3.1.3|-   The error code and error message are added for invalid encoding formats.
-   The issue is fixed where the settings of the cropping area are invalid. The bundleId parameter is replaced with the packageName parameter in the download operation.
-   The encoding format error can be returned by underlying libraries. |

## Short video SDK Standard for Android

|**Release date**|**Version**|**Description**|
|----------------|-----------|---------------|
|2020-10-30|V3.17.0|-   The package name of the short video SDK for Android is optimized, which reduces the cost of service integration and makes the SDK more user-friendly. The new package name is in the unified format of com.aliyun.svideosdk. \*. For more information about the latest API operations, see [Project configuration](/intl.en-US/Short video SDK/Android short video SDK/Project configuration.md).

If you need to upgrade the existing API to the latest version, download the [upgrade tool](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/shortVideo/tool/interface_upgrade.py).

-   The sound effect of lolita is optimized and the sound effects of Chinese dialects are added.
-   The issue of unexpected quits during photo taking in extreme scenarios is fixed.
-   The following deprecated operations that are no longer needed are deleted:
    -   com.error.NativeErrorCode
    -   com.qu.preview.callback.OnNativeReady
    -   com.aliyun.qupai.editor.AliyunIExporter
    -   com.aliyun.qupai.editor.AliyunIPlayer
    -   com.aliyun.qupai.editor.OnPlayCallback
    -   com.aliyun.qupai.editor.OnPreparedListener
    -   com.aliyun.querrorcode.AliyunVideoCoreError |
|2020-09-21|V3.16.2|-   The effect of the Gaussian blur background is optimized. |
|2020-06-23|V3.16.1|-   The issue is fixed where the subtitles and animated stickers do not correctly move during secondary editing.
-   The issue is fixed where the number of words is different in different lines of the added subtitles. |
|2020-05-12|V3.16.0|-   The mainstream animation effects are added again.
-   The issue of intermittent unexpected quits that users report online is fixed.
-   The issue is fixed where freezes may occur during the playback of long videos.
-   The issue is fixed where the recording unexpectedly quits due to incompatibility with some phone models. |
|2020-03-20|V3.15.0|-   The issue is fixed where freezes occur during the playback of produced videos.
-   The issue is fixed where the speed of multiple clips cannot be changed at the same time.
-   The issue is fixed where the exposure area of the front camera of some phone models is invalid.
-   Two sets of transitions, filter effect transitions, and filter effects are added based on the specifications for producing custom effects.
-   An operation is added for modifying the parameters of custom effects in real time.
-   The features of custom filters, transition effects, and custom effects are supported. |
|2019-12-27|V3.14.0|-   The SDK is adapted to the Android Q system to improve the performance of recording, editing, and generating videos in the Android Q system.
-   The recording implementation is optimized and the issue of intermittent unexpected quits is fixed.
-   The known memory leaks are fixed and the performance of some modules is optimized. |
|2019-11-21|V3.13.0|-   The RACE engine-based face filters are added to the recording module.
-   The stability and performance of the recording module are optimized. |
|2019-09-10|V3.12.0|-   The feature of log analysis is supported. The AlivcSdkCore\#setDebugLoggerLevel\(AlivcDebugLoggerLevel level\) operation is added for specifying whether to enable the feature. The following three options are provided:
    -   AlivcDLClose: Disable the feature of log analysis.
    -   AlivcDLNormal: Analyze warning or error logs. We recommend that you use this option to analyze logs.
    -   AlivcDLAll: Analyze all logs. We recommend that you use this option only for troubleshooting. We recommend that you do not use this option in the official release. You can only use this option to analyze logs of the SDK.
-   The performance of the editing module is improved.
-   The addRunningDisplayMode operation is deleted from the editing module.
-   The removeRunningDisplayMode operation is deleted from the editing module. |
|2019-07-30|V3.11.0|-   The start and stop speeds of clip recording and the video production speed are improved, which enables smoother clip recording.
-   The granularity and accuracy of the recording progress callback are improved.
-   The transcoding speed in some scenarios is improved by precisely adjusting the GOP size. |
|2019-06-26|V3.10.5|-   The AliyunIMixRecorder operation is added.
-   The AliyunMixComposer operation is added. This operation can be used to achieve effects such as picture-in-picture and left-right split-screen. |
|2019-06-12|V3.10.0|-   The sound effects of the big devil and Minions are added to the editing module. Videos in the MJPEG format can be edited.
-   The compatibility with some damaged video files is improved for playback during editing.
-   Hardware decoding is supported for HEVC videos during editing and transcoding.
-   The transcoding speed is improved.
-   An operation is added for resetting the size of the preview window during recording.
-   The issue is fixed where the duration is incorrectly displayed for a recorded video clip.
-   Separate operations for producing and uploading videos are added.
-   The issue is fixed where a memory leak may occur because some handles are not released.
-   The draw method is added to forcibly draw a frame during editing. This fixes the issue where the first frame is not drawn during initialization by default. |
|2019-04-24|V3.9.0|-   The sound effect feature is supported with multiple effects, such as lolita, uncle, reverberation, and echo.
-   The seeking performance during editing is improved. |
|2019-03-01|V3.8.0|-   The playback capability during editing is optimized to ensure smooth playback.
-   The video production speed is improved for the editing module.
-   The preview resolution of recorded videos is optimized.
-   The recording frame rate on low-end devices is improved. |
|2018-12-21|V3.7.7|-   The video resolution is improved without changing the video quality.
-   H.265 videos can be uploaded. |
|2018-11-01|V3.7.5|-   The transition feature is supported with mainstream effects, such as fade, polygon, and blinds.
-   Multiple speed ramps can be added for multiple video clips.
-   The compatibility with GIF images is improved. |
|2018-08-21|V3.6.5.1|-   Copyrighted music from Xiami Music is integrated.
-   A third-party AR facial recognition module is integrated and advanced face and skin filters are added.
-   The issue is fixed where multiple video clips cannot be automatically played after they are uploaded for editing.
-   The pixel buffer can be used to access and render YUV data. |
|2018-07-26|V3.6.5|-   The issue is fixed where some videos are stuck at 99% during cropping.
-   The issue is fixed where freezes occur during the preview of some cropped videos.
-   The known bugs in the editing and upload modules are fixed. |
|2018-06-21|V3.6.0|-   The editing module is rebuilt to improve the performance of transcoding and production.
-   The time effects, including the fast-forward motion, slow motion, looping, and reverse motion effects, are added.
-   The video file size is reduced without changing the resolution.
-   The resolution of videos that are rendered with effects is improved.
-   The features of audio mixing, audio cropping, and choosing random audio segments are supported. |
|2018-02-09|V3.5.0|-   Multiple videos and images can be uploaded at the same time.
-   The features of filter, music, doodle, and closing credits are added to the editing module.
-   Filters, such as trance and phantom, are added. |
|2018-01-03|V3.4.0|Thirteen filters are added.|
|2017-11-24|V3.3.5|The upload feature is supported.|
|2017-10-25|V3.3.4|-   An operation is added for customizing the bitrate.
-   An operation for cropping videos is added to the GPU to improve performance.
-   The performance of related modules is optimized to improve stability. |
|2017-09-29|V3.3.3|-   The manual focus feature during video recording is optimized.
-   The reporting of unexpected program quits and errors is supported to improve the SDK. |
|2017-08-31|V3.3.2|-   An operation is added for setting the background color of the cropping UI.
-   Software encoding is supported.
-   The issue of unexpected quits in Android 8.0 is fixed. |
|2017-08-11|V3.3.1|The resolution of recorded videos is optimized.|
|2017-07-21|V3.3.0|-   The features of real-time audio mixing and speed ramping are supported.
-   The issue of intermittent unexpected quits during video recording is fixed.
-   The issue is fixed where the aspect ratio of uploaded videos is invalid.
-   The performance of related modules is optimized to improve stability. |
|2017-06-16|V3.1.3|-   The error code and error message are added for invalid encoding formats.
-   The issue is fixed where the settings of the cropping area are invalid. The bundleId parameter is replaced with the packageName parameter in the download operation.
-   The encoding format error can be returned by underlying libraries. |
|2017-05-17|V3.1.1|-   Obfuscation settings are added.
-   The issue is fixed where the player unexpectedly quits when the GOP size is less than 2 seconds.
-   The issue is fixed where the player unexpectedly quits during video recording on Google Nexus mobile phones.
-   The issue is fixed where the player unexpectedly quits during video cropping.
-   The issue is fixed where the face filter icon is invalid due to a filter switching failure that occurs when you access the camera from the album. |
|2017-05-12|V3.1.0|-   The basic features of recording and editing short videos are supported.
-   The features of resumable video recording, ripple deletion, face filters, camera switching, multi-resolution video recording, real-time filter effects, uploading, and cropping are supported. |

## Short video SDK Basic for Android

|**Release date**|**Version**|**Description**|
|----------------|-----------|---------------|
|2020-10-30|V3.17.0|-   The package name of the short video SDK for Android is optimized, which reduces the cost of service integration and makes the SDK more user-friendly. The new package name is in the unified format of com.aliyun.svideosdk. \*. For more information about the latest API operations, see [Project configuration](/intl.en-US/Short video SDK/Android short video SDK/Project configuration.md).

If you need to upgrade the existing API to the latest version, download the [upgrade tool](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/shortVideo/tool/interface_upgrade.py).

-   The sound effect of lolita is optimized and the sound effects of Chinese dialects are added.
-   The issue of unexpected quits during photo taking in extreme scenarios is fixed.
-   The following deprecated operations that are no longer needed are deleted:
    -   com.error.NativeErrorCode
    -   com.qu.preview.callback.OnNativeReady
    -   com.aliyun.qupai.editor.AliyunIExporter
    -   com.aliyun.qupai.editor.AliyunIPlayer
    -   com.aliyun.qupai.editor.OnPlayCallback
    -   com.aliyun.qupai.editor.OnPreparedListener
    -   com.aliyun.querrorcode.AliyunVideoCoreError |
|2020-09-21|V3.16.2|-   The effect of the Gaussian blur background is optimized. |
|2020-06-23|V3.16.1|-   The issue is fixed where the number of words is different in different lines of the added subtitles.
-   The issue is fixed where the subtitles and animated stickers do not correctly move during secondary editing. |
|2020-05-12|V3.16.0|-   The mainstream animation effects are added again.
-   The issue of intermittent unexpected quits that users report online is fixed.
-   The issue is fixed where freezes may occur during the playback of long videos.
-   The issue is fixed where the recording unexpectedly quits due to incompatibility with some phone models. |
|2020-03-20|V3.15.0|-   The issue is fixed where freezes occur during the playback of produced videos.
-   The issue is fixed where the speed of multiple clips cannot be changed at the same time.
-   The issue is fixed where the exposure area of the front camera of some phone models is invalid.
-   Two sets of transitions, filter effect transitions, and filter effects are added based on the specifications for producing custom effects.
-   An operation is added for modifying the parameters of custom effects in real time.
-   The features of custom filters, transition effects, and custom effects are supported. |
|2019-12-27|V3.14.0|-   The SDK is adapted to the Android Q system to improve the performance of recording, editing, and generating videos in the Android Q system.
-   The recording implementation is optimized and the issue of intermittent unexpected quits is fixed.
-   The known memory leaks are fixed and the performance of some modules is optimized. |
|2019-11-21|V3.13.0|-   The stability and performance of the recording module are optimized.
-   The RACE engine-based face filters are added to the recording module.
-   The known issues are fixed to improve stability. |
|2019-09-10|V3.12.0|-   The feature of log analysis is supported. The AlivcSdkCore\#setDebugLoggerLevel\(AlivcDebugLoggerLevel level\) operation is added for specifying whether to enable the feature. The following three options are provided:
    -   AlivcDLClose: Disable the feature of log analysis.
    -   AlivcDLNormal: Analyze warning or error logs. We recommend that you use this option to analyze logs.
    -   AlivcDLAll: Analyze all logs. We recommend that you use this option only for troubleshooting. We recommend that you do not use this option in the official release. You can only use this option to analyze logs of the SDK.
-   The performance of the editing module is improved.
-   The addRunningDisplayMode operation is deleted from the editing module.
-   The removeRunningDisplayMode operation is deleted from the editing module. |
|2019-07-30|V3.11.0|-   The start and stop speeds of clip recording and the video production speed are improved, which enables smoother clip recording.
-   The granularity and accuracy of the recording progress callback are improved.
-   The transcoding speed in some scenarios is improved by precisely adjusting the GOP size. |
|2019-06-26|V3.10.5|The performance of related modules is optimized to improve stability.|
|2019-06-12|V3.10.0|-   The transcoding speed is improved.
-   Separate operations for producing and uploading videos are added.
-   An operation is added for resetting the size of the preview window during recording.
-   The issue is fixed where the duration is incorrectly displayed for a recorded video clip.
-   The issue is fixed where a memory leak may occur because some handles are not released. |
|2019-04-24|V3.9.0|The performance of related modules is optimized to improve stability.|
|2019-03-01|V3.8.0|-   The preview resolution of recorded videos is optimized.
-   The recording frame rate on low-end devices is improved.
-   The performance of related modules is optimized to improve stability. |
|2018-12-21|V3.7.7|-   The video resolution is improved without changing the video quality.
-   H.265 videos can be cropped. |
|2018-11-01|V3.7.5|The player UI is open sourced to support custom UI and interaction design.|
|2018-02-09|V3.5.0|The performance of related modules is optimized to improve stability.|
|2018-01-03|V3.4.0|Thirteen filters are added.|
|2017-11-24|V3.3.5|-   The upload feature is supported.
-   An operation is added for modifying the style of the upload UI.
-   The performance of related modules is optimized to improve stability. |
|2017-10-25|V3.3.4|-   An operation is added for customizing the bitrate.
-   An operation for cropping videos is added to the GPU to improve performance.
-   The performance of related modules is optimized to improve stability. |
|2017-09-29|V3.3.3|-   The manual focus feature during video recording is optimized.
-   The reporting of unexpected program quits and errors is supported to improve the SDK. |
|2017-08-31|V3.3.2|-   An operation is added for setting the background color of the cropping UI.
-   Software encoding is supported.
-   The issue of unexpected quits in Android 8.0 is fixed. |
|2017-08-11|V3.3.1|-   An operation is added for displaying videos and images on the upload UI.
-   The resolution of recorded videos is optimized. |
|2017-07-12|V3.3.0|-   The issue of intermittent unexpected quits during video recording is fixed.
-   The issue is fixed where the aspect ratio of uploaded videos is invalid.
-   The performance of related modules is optimized. |
|2017-06-16|V3.1.3|-   The error code and error message are added for invalid encoding formats.
-   The issue is fixed where the settings of the cropping area are invalid. The bundleId parameter is replaced with the packageName parameter in the download operation.
-   The encoding format error can be returned by underlying libraries. |
|2017-05-17|V3.1.1|-   Obfuscation settings are added.
-   The issue is fixed where the player unexpectedly quits when the GOP size is less than 2 seconds.
-   The issue is fixed where the player unexpectedly quits during video recording on Google Nexus mobile phones.
-   The issue is fixed where the face filter icon is invalid due to a filter switching failure that occurs when you access the camera from the album. |
|2017-05-12|V3.1.0|-   The basic features of recording and editing short videos are supported.
-   The features of resumable video recording, ripple deletion, face filters, camera switching, multi-resolution video recording, real-time filter effects, uploading, and cropping are supported. |
