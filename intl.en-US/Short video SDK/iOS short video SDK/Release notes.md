# Release notes

## V3.20.0

**Feature updates**

-   The audio fade effect is added to the editing module.
-   The combined subtitle feature is added to the editing module.
-   The basic editing capability is added to the editing module.
-   The capability of obtaining the thumbnails of specified video timestamps is added.
-   The issue is fixed where the frame rate that you set for the exported video during editing does not take effect.
-   The stability of the SDK is improved.

## V3.19.0

**Feature updates**

-   The noise reduction feature is added to the editing module.
-   The background image and background color can be set during duet recording and video merging.
-   Audio tracks can be merged during duet recording and video merging.
-   Echoes can be removed for duet recording.
-   The issue is fixed where the halo color changes when a transparent halo effect is added to a watermark or an image.
-   The issue is fixed where added static images are not rotated in the expected angle.

**SDK changes**

Deprecated classes:

AliyunCamera & AliyunIRecorder,@property\(nonatomic, assign\) BOOL useAudioSessionModeVideoRecording;

## V3.18.1

**Feature updates**

The issue is fixed where a memory leak occurs when hardware encoding is used on specific iOS phone models.

## V3.18.0

**Feature updates**

Audio tracks can be specified during duet recording. For example, you can use the original or recorded audio. You can also mute the audio.

## V3.17.1

**Feature updates**

-   The scaling mode is supported for front cameras.
-   The issue is fixed where Open Graphics Library \(OpenGL\) unexpectedly quits applications on specific phone models after a video is produced.

## V3.17.0

**Feature updates**

-   The voice effect of lolita is optimized and the voice effects of Chinese dialects are added.
-   The issue is fixed where the screen becomes green when a video that is shot on iPhone 12 is imported to the cropping or editing module.

## V3.16.2

**Feature updates**

The Gaussian blur effect on backgrounds is improved.

## V3.16.1

**Feature updates**

The issue is fixed where a recorded video cannot be merged with an existing video whose length is shorter than that of the recorded video.

## V3.16.0

**Feature updates**

-   The major animation effects are added again.
-   The issue is fixed where intermittent unexpected quits occur when users send feedback online.
-   The issue is fixed where stuttering may occur during the playback of long videos.
-   The issue is fixed where the watermark is not displayed in the expected direction when a video is recorded in landscape mode.

## V3.15.0

**Feature updates**

-   The issue is fixed where stuttering occurs during the playback of produced videos.
-   The issue is fixed where the speed of multiple clips cannot be changed at the same time.
-   Two sets of transitions, filter effect transitions, and filters are added based on the standards of producing custom effects.

**SDK changes**

-   A method is added to modify the parameters of custom effects in real time.
-   The features of custom filters and transitions are supported. For more information about the standards of producing custom effects, see the official documentation.

## V3.14.0

**Feature updates**

-   The cropping module is optimized to prevent chromatic distortion when a video is cropped multiple times.
-   The stability of the recording module is optimized to deal with exceptions, such as background execution and hardware resource occupation.
-   The known memory leaks are fixed and the performance of specific modules is optimized.

**Fixed issues**

-   The issue is fixed where intermittent unexpected quits occurs when the application is switched to the background during recording.
-   The issue is fixed where exceptions occur when audio resources are occupied during recording.
-   The issue is fixed where the color setting of the background does not take effect.
-   The issue is fixed where a part of the playback image is enlarged after the view of the editing module is changed on iOS devices.
-   The known issues, such as specific known memory leaks, are fixed.

**SDK changes**

The AliyunVideoSDKPro.framework dynamic framework is split into AliyunVideoSDKPro.framework static framework and AliyunVideoCore.framework dynamic framework. If you want to manually integrate the short video SDK, see [Project configuration](/intl.en-US/Short video SDK/iOS short video SDK/Project configuration.md).

## V3.13.0

**Feature updates**

-   The stability and performance of the recording module are optimized.
-   The Render And Compute Everything \(RACE\) engine-based face filters are added to the recording module.
-   The fluency of H.265 videos is improved in the editing module.

**SDK changes**

The method for the music video \(MV\) effect is deprecated and the feature of adding the MV effect is removed.

## V3.12.0

**Feature updates**

-   The feature of log analysis is supported. The AliyunVideoSDKInfo setDebugLogLevel method is added to specify whether to enable the feature. The following three options are provided:

    ```
    AlivcDebugLogClose: Disable the feature of log analysis.
    AlivcDebugLogNormal: Analyze warning or error logs. We recommend that you use this option to analyze logs.
    AlivcDebugLogAll: Analyze all logs. We recommend that you use this option only for troubleshooting. However, we recommend that you do not use this option in the official release where this option can be used only to analyze logs of the SDK.
                            
    ```

-   The performance of the editing module is improved.

**Fixed issues**

The issue is fixed where the recording process is stopped but the corresponding thread is still running.

**SDK changes**

The applyRunningDisplayMode method is deleted from the editing module.

## V3.11.0

**Feature updates**

-   The start and stop speeds of clip recording and the video production speed are improved, which allows smoother clip recording.
-   The granularity and accuracy of the recording progress callback are improved.
-   The transcoding speed in specific scenarios is improved by precisely adjusting the group of pictures \(GOP\) size.
-   The time that is required to switch between cameras is reduced.

**Fixed issues**

-   The issue is fixed where the number of frames in a GIF image is not accurately parsed.
-   The issue is fixed where specific videos stutter when the videos are reversely played.
-   The issue is fixed where the duration of a recorded video is inaccurate.
-   The issue is fixed where the audio and image of a multi-clip video are not synchronized.

**SDK changes**

-   All error codes are integrated into AliyunVideoCoreError.
-   The NSString\* AlivcErrorMessage\(int code\) method is added.

## V3.10.5

**Feature updates**

-   The AliyunMixRecorder interface is added. This interface can be used to record videos in duet mode.
-   The AliyunIMixComposer interface is added. This interface can be used to achieve effects such as picture-in-picture \(PiP\) and left-right split-screen.

## V3.10.0

**Feature updates**

-   The voice effects of the big devil and Minions are added to the editing module.
-   Videos in the MJPEG format can be edited.
-   The compatibility with specific damaged video files is improved for playback during editing.
-   The draw method is added to forcibly draw a frame during editing.

**Fixed issues**

-   The issue is fixed where the duration is not accurately displayed for a recorded video clip.
-   The issue is fixed where the watermark that is added during recording disappears when the application is switched to the background.
-   The issue is fixed where stuttering occurs when you switch between the front and rear cameras during recording.
-   The issue is fixed where an unexpected quit may occur when the application is switched to the background during production.

## V3.9.0

**Feature updates**

-   The voice effect feature is supported. The voice effects include lolita, male, reverberation, and echo.
-   The seeking performance during editing is improved.
-   The stability of the SDK is improved.

## V3.8.0

**Feature updates**

-   The recording stability is improved.
-   The accuracy of time selection during cropping is improved.
-   The playback capability during editing is optimized to ensure smooth playback.
-   The video production speed is improved for the editing module.
-   Specific issues are fixed.
-   The production can be resumed after the application is switched to the foreground from the background.
-   To meet the requirement of SDK stability monitoring and data-related requirements in the future, the AlivcConan.framework is changed as a required dependency. In manual integration, you must add AlivcConan.framework. In CocoaPods integration, you must add pod 'AlivcConan', '0.9.0' to Podfile. For more information, see the demo code.

## V3.7.7

**Feature updates**

-   The stability of the SDK is improved.
-   The resolution of cropped and produced videos is improved.

## V3.7.5

**Feature updates**

-   The issue is fixed where a display exception occurs during the reverse playback of High Efficiency Video Coding \(HEVC\) videos that are generated by iOS 12.
-   The issue is fixed where unexpected quits may occur when a third-party rendering interface is used in editing.
-   The playback smoothness of videos with time effects is improved.
-   The compatibility with GIF images is improved.
-   Videos with odd resolution can be imported.
-   Audio and video synchronization during multi-clip recording is optimized.
-   The stability is improved.

## V3.7.0

**Feature updates**

-   The transition feature is supported with major effects, such as fade, polygon, and blinds.
-   The animation feature is supported with basic animations, such as rotation, translation, scaling, and alpha, and custom animations, such as linear erasure.
-   The Gaussian blur effect can be added to the specified stream in the specified time period.
-   The display mode, including padding and cropping, can be set for the specified stream in the specified time period.
-   The dubbing feature is supported with multi-track dubbing and speed adjustment.
-   Multiple speed control effects can be added to a multi-clip video. The repetition and reverse playback effects can be configured only for a single-clip video.

**SDK changes**

-   The method to be called after preview playback ends is changed from play to replay.
-   The prepare method is added for preloading data, which is called after the startEdit method is called.
-   The reference coordinates of the watermark position and size are changed to the output resolution coordinates.
-   The logic for adding a transition is modified. You must call the stopEdit method before you add a transition. After the transition is added, you can call the startEdit method.
-   The delegate attribute is deleted from the AliyunPasterController class.
-   The destroyAllEffect method is deleted from the AliyunEditor class.
-   The name of QuCore-ThirdParty.framework is changed to alivcffmpeg.framework.

## V3.6.5.5

**Feature updates**

The SDK is compatible with Xcode 10.

## V3.6.5.3

**Feature updates**

-   The issue is fixed where an unexpected quit may occur if the screen is locked when you add an MV during recording.
-   The issue is fixed where an animated filter is not displayed in the specified time period during the reverse playback.
-   The issue is fixed where specific videos are not displayed in the correct color.
-   Audio files in the AAC SBR format are supported.

## V3.6.5

**Feature updates**

-   The issue is fixed where an unexpected quit may occur when a video is exported.
-   The smoothness of reverse playback is improved.

## V3.6.0

**Feature updates**

Framework file size and basic issues

|Name|Size \(Unit: MB\)|
|----|-----------------|
|AliyunVideoSDKPro.framework3.5.0 release|4.9M|
|AliyunVideoSDKPro.framework3.5.0 debug|10.1M|
|AliyunVideoSDKPro.framework3.6.0 release|7.6M|
|AliyunVideoSDKPro.framework3.6.0 debug|15.7M|
|QuCore-ThirdParty.framework3.5.0 release|9.3M|
|QuCore-ThirdParty.framework3.5.0 debug|23.1M|
|QuCore-ThirdParty.framework3.6.0 release|10.2M|
|QuCore-ThirdParty.framework3.6.0 debug|23.2M|

**Note:** AliyunVideoSDKPro.framework and QuCore-ThirdParty.framework must be replaced at the same time. Otherwise, exceptions such as an unexpected quit during production may occur.

**SDK changes**

-   Method changes for watermarks

    The setWaterMark:frame method is deprecated and the setWaterMark method is added. The following code provides an example on how to set a watermark:

    ```
    NSString watermarkPath = [[NSBundle mainBundle] pathForResource:@"watermark" ofType:@"png"]; 
    AliyunEffectImage effectImage = [[AliyunEffectImage alloc] init];
    effectImage.frame = CGRectMake(10, 10, 28, 20);
    effectImage.path = watermarkPath;
    [self.editor setWaterMark:effectImag];
    ```

-   Method changes for end watermarks

    The end watermark can be viewed during preview. The following code provides an example on how to set an end watermark by calling the setTailWaterMark method:

    ```
    NSString tailWatermarkPath = [[NSBundle mainBundle] pathForResource:@"tail" ofType:@"png"]; 
    AliyunEffectImage tailWatermark = [[AliyunEffectImage alloc] initWithFile:tailWatermarkPath];
    tailWatermark.frame = CGRectMake(CGRectGetMidX(self.movieView.bounds) - 84 / 2, CGRectGetMidY(self.movieView.bounds) - 60 / 2, 84, 60);
    tailWatermark.endTime = 2;
    [self.editor setTailWaterMark:tailWatermark];
    ```

-   Method for adding music
    -   Multiple audio streams can be mixed. To add only one audio stream, you must call the removeMusics method. The following code provides an example on how to add one audio stream:

        ```
        AliyunEffectMusic *music = [[AliyunEffectMusic alloc] initWithFile:path];
        [self.editor removeMusics];// If you want to add only one audio stream, call the removeMusics method.
        [self.editor applyMusic:music];
        ```

    -   To add music, call the removeMVMusic method, for example, AliyunEffectMusic \*music = \[\[AliyunEffectMusic alloc\] initWithFile:path\].

        ```
        [self.editor removeMVMusic];
        [self.editor removeMusics];
        [self.editor applyMusic:music];
        ```

    -   The playback of a specified part of a music stream is supported. The following code provides an example on how to specify a time range:

        ```
        AliyunEffectMusic music = [[AliyunEffectMusic alloc] initWithFile:path];
        music.startTime = startTime; // Set the start time of the part to be played in the music stream.
        music.duration = duration; // Set the duration of the part to be played in the music stream.
        music.streamStartTime = streamStart [_player getStreamDuration]; // Set the time when the music stream starts to be played in the playback timeline.
        music.streamDuration = streamDuration * [_player getStreamDuration]; // Set the playback duration of the music stream in the playback timeline.
        ```

-   New method for displaying time effects
    -   The addTimelineTimeFilterItem method is added. For more information about the code, see the demo code.
    -   Time effects affect animated filters.

        If you add an animated filter when the playback speed is adjusted in the entire video or the entire video is reversely played, make sure that the animated filter is displayed in the desired time period. In V3.6.0, the code is in the following methods:

        ```
        (void)didBeganLongPressEffectFilter:(AliyunEffectFilterInfo *)animtinoFilterInfo;
        (void)didTouchingProgress;
        (void)didEndLongPress;
        ```

        You can reference the following code for the three methods:

        ```
        AliyunEffectFilter *animationFilter = [[AliyunEffectFilter alloc] initWithFile:[animtinoFilterInfo localFilterResourcePath]];
        float currentSec = [self.player getCurrentTime];
        float currentStreamSec = [self.player getCurrentStreamTime];
        animationFilter.startTime = currentSec;
        animationFilter.endTime = [self.player getDuration];
        animationFilter.streamStartTime = currentStreamSec; // The streamStartTime parameter is added. You must set the parameter when a time effect is applied.
        animationFilter.streamEndTime = [self.player getStreamDuration];// The streamEndTime parameter is added. You must set the parameter when a time effect is applied.
        [self.editor applyAnimationFilter:animationFilter];
        ```

        For compatibility with earlier versions, you can still set the startTime and endTime parameters when no time effect is applied. In this case, streamStartTime and streamEndTime parameters are not required.

-   New time effect method

    The new methods can also be used in V3.5.0. For more information about the code, see the demo code of V3.6.0.

    ```
    AliyunEffectTimeFilter *timeFilter = [[AliyunEffectTimeFilter alloc] init];
    timeFilter.startTime = [_player getCurrentStreamTime];
    timeFilter.endTime = timeFilter.startTime + 1;
    timeFilter.type = TimeFilterTypeSpeed;
    timeFilter.param = 0.5;
    [self.editor applyTimeFilter:timeFilter];
    ```

-   The adjustment of playback status and methods, such as the methods for switching between the foreground and background and screen switching

    Compared with V3.5.0, the events of switching between the foreground and background and screen switching are internally handled in V3.6.0.

    -   The setActive method is deprecated.
    -   Handling of viewWillAppear and viewWillDisappear: When the viewWillDisappear callback is received, you do not need to call the stopEdit method to release the entire AliyunEdit instance. Instead, you need only to call the stop method to stop the playback. Similarly, when the viewWillAppear callback is received, you need only to call the play method to restart the playback.
    -   Handling when the application is switched to the background or foreground:

        When the application is switched to the background, the SDK stops the playback or production. When the application is switched to the foreground, the SDK starts or pauses the playback by default.

        Error handling:

        In V3.6.0, when an error occurs during the playback or production, the playback or production is stopped, and the error is returned in the playError or exportError callback. You can handle the error as needed.

-   The following three methods of the AliyunImporter class are deprecated. For compatibility with earlier versions, these methods can still be used in V3.6.0.

    -   \(void\)addVideoWithPath:\(NSString \*\)videoPath animDuration:\(CGFloat\)animDuration
    -   \(void\)addVideoWithPath:\(NSString \*\)videoPath startTime:\(CGFloat\)startTime duration:\(CGFloat\)duration animDuration:\(CGFloat\)animDuration
    -   \(NSString \)addImage:\(UIImage \)image duration:\(CGFloat\)duration animDuration:\(CGFloat\)animDuration
    In V3.6.0, you can construct an AliyunClip object and call the addMediaClip:\(AliyunClip\*\)clip method to add a video clip. The following code provides an example:

    ```
    AliyunImporter *importor = [[AliyunImporter alloc] initWithPath:root outputSize:_compositionConfig.outputSize];
    AliyunClip *clip = [[AliyunClip alloc] initWithVideoPath:info.sourcePath startTime:info.startTime duration:info.duration animDuration:i == 0 ? 0 : 1];
    [importor addMediaClip:clip];
    ```


**Note:** You must know the basic concepts about the player when you use time effects.

-   /\* Obtain the total playback duration, in seconds. @return The total duration. /

    \(double\)getDuration

-   /\* Obtain the current playback position, in seconds. /

    \(double\)getCurrentTime

-   /\* Obtain the duration of the original video stream, in seconds. @return The total duration. /

    \(double\)getStreamDuration

-   /\* Obtain the playback position in the original video stream, in seconds. /

    \(double\)getCurrentStreamTime


**Examples**

-   If the duration of a video is 15s and the entire video is played at twice the speed, getDuration returns 7.5s and getStreamDuration returns 15s. In this case, when getCurrentTime returns 3.5s, getCurrentStreamTime returns 7s.
-   If the duration of a video is 15s and the entire video is played at half the speed, getDuration returns 30s and getStreamDuration returns 15s. In this case, when getCurrentTime returns 10s, getCurrentStreamTime returns 5s.
-   If the duration of a video is 15s and the entire video is reversely played, getDuration and getStreamDuration both return 15s. In this case, when getCurrentTime returns 6s, getCurrentStreamTime returns 9s.

In the preceding examples, the time effect is applied to the entire video. If the time effect is applied only to a part of the video, the playback duration, stream duration, and playback positions are calculated based on the same rules.

## Others

**ReleaseNote**

-   New time effect methods
    -   \(int\)applyTimeFilter:\(AliyunEffectTimeFilter \*\)filter
    -   \(int\)removeTimeFilter
-   The following methods of the AliyunImporter class are deprecated:
    -   \(void\)addVideoWithPath:\(NSString \*\)videoPath animDuration:\(CGFloat\)animDuration
    -   \(void\)addVideoWithPath:\(NSString \*\)videoPath startTime:\(CGFloat\)startTime duration:\(CGFloat\)duration animDuration:\(CGFloat\)animDuration
    -   \(NSString \)addImage:\(UIImage \)image duration:\(CGFloat\)duration animDuration:\(CGFloat\)animDuration

        In V3.6.0, you can construct an AliyunClip object and call the addMediaClip:\(AliyunClip\*\)clip method to add a video clip. The following code provides an example:

        ```
        AliyunImporter importor = [[AliyunImporter alloc] initWithPath:root outputSize:_compositionConfig.outputSize];
        AliyunClip *clip = [[AliyunClip alloc] initWithVideoPath:info.sourcePath startTime:info.startTime duration:info.duration animDuration:i == 0 ? 0 : 1];
        [importor addMediaClip:clip];
        ```

-   The playback status and methods are adjusted. Compared with V3.5.0, the events of switching between the foreground and background and screen switching are internally handled in V3.6.0.

    The setActive method is deprecated.

    Handling of viewWillAppear and viewWillDisappear: When the viewWillDisappear callback is received, you do not need to call the stopEdit method to release the entire AliyunEdit instance. Instead, you need only to call the stop method to stop the playback. Similarly, when the viewWillAppear callback is received, you need only to call the play method to restart the playback.

    Handling when the application is switched to the background or foreground: When the application is switched to the background, the SDK stops the playback or production. When the application is switched to the foreground, the SDK starts or pauses the playback by default.

    Error handling: In V3.6.0, when an error occurs during the playback or production, the playback or production is stopped, and the error is returned in the playError or exportError callback. You can handle the error as needed.

-   New methods for the player
    -   \(double\)getStreamDuration; // Obtain the duration of the original video stream, in seconds.
    -   \(double\)getCurrentStreamTime; // Obtain the playback position in the original video stream., in seconds.
-   Method changes for watermarks
    -   The setWaterMark: frame method is deprecated.
    -   The setWaterMark:\(AliyunEffect\*\)waterMark method is added.
    -   The setTailWaterMark: method can be called to set an end watermark, which can be previewed.
-   Method for adding music
    -   Multiple audio streams can be mixed. The specified part of a music stream can be played. To add only one audio stream, you must call the removeMusics method. The following code provides an example:

        ```
        AliyunEffectMusic *music = [[AliyunEffectMusic alloc] initWithFile:path];
        [self.editor removeMusics];// If you want to add only one audio stream, call the removeMusics method. 
        [self.editor applyMusic:music];
        ```

    -   The specified part of a music stream can be played. The following code provides an example:

        ```
        AliyunEffectMusic music = [[AliyunEffectMusic alloc] initWithFile:path];
        music.startTime = startTime; // Set the start time of the part to be played in the music stream. 
        music.duration = duration; // Set the duration of the part to be played in the music stream.
        music.streamStartTime = streamStart [_player getStreamDuration]; // Set the time when the music stream starts to be played in the playback timeline.
        music.streamDuration = streamDuration * [_player getStreamDuration]; // Set the playback duration of the music stream in the playback timeline.
        ```


