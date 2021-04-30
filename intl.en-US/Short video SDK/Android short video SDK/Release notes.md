# Release notes

## V3.19.0

**Feature updates**

-   The noise reduction feature is added to the editing module.
-   The background image and background color can be set during duet recording and video merging.
-   Audio tracks can be merged during duet recording and video merging.
-   Callbacks for audio data can be fired during the preview of the recording file.
-   The issue is fixed where emojis in subtitles fail to be displayed when the font of the subtitles is enlarged to a specific size in the editing module.
-   The issue is fixed where the halo color changes when a transparent halo effect is added to a watermark or an image.
-   The issue is fixed where added static images are not rotated in the expected angle.

SDK changes

The following interfaces are deprecated:

-   com.aliyun.svideosdk.editor.AudioEffectType.EFFECT\_TYPE\_DENOISE
-   com.aliyun.svideosdk.editor.AliyunIEditor.denoise\(int, boolean\)

**Others**

-   **URL of the Maven repository for the short video SDK for Android**

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   **Core libraries**

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.19.0
```


## V3.18.1

**Feature updates**

The issue is fixed where the screen flickers during duet recording in cropping mode.

**Others**

-   **URL of the Maven repository for the short video SDK for Android**

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   **Core libraries**

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.18.1
```


## V3.18.0

**Feature updates**

-   Audio tracks, such as the track of the original audio, recorded audio, or mute audio, can be specified for duet recording.
-   The issue is fixed where black bars flicker when the aspect ratio is switched on Android Q phones.

**Others**

-   **URL of the Maven repository for the short video SDK for Android**

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   **Core libraries**

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.18.0
```


## V3.17.1

**Feature updates**

-   The issue is fixed where Open Graphics Library \(OpenGL\) unexpectedly quits applications on specific phone models after a video is produced.
-   The issue is fixed where custom fonts do not take effect.
-   The issue is fixed where the information about the timestamp and process ID is not written after you call the AlivcSdkCore.setLogPath method.

**Others**

-   **URL of the Maven repository for the short video SDK for Android**

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   **Core libraries**

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.17.1
```


## V3.17.0

Feature updates

-   The voice effect of lolita is optimized and the voice effects of Chinese dialects are added.
-   The issue is fixed where unexpected quits occur during photo taking in extreme scenarios.

SDK changes

-   The package name of the short video SDK for Android is optimized. The new package name is in the unified format of com.aliyun.svideosdk. \*.

    For more information, see the [API Reference](/intl.en-US/Short video SDK/Android short video SDK/Project configuration.md) section in the Project configuration topic. If you need to upgrade the existing API to the latest version, download the [interface\_upgrade](https://alivc-demo-cms.alicdn.com/versionProduct/sourceCode/shortVideo/tool/interface_upgrade.py) tool.

-   The following deprecated interfaces are deleted:
    -   com.error.NativeErrorCode
    -   com.qu.preview.callback.OnNativeReady
    -   com.aliyun.qupai.editor.AliyunIExporter
    -   com.aliyun.qupai.editor.AliyunIPlayer
    -   com.aliyun.qupai.editor.OnPlayCallback
    -   com.aliyun.qupai.editor.OnPreparedListener
    -   com.aliyun.querrorcode.AliyunVideoCoreError

Others

-   URL of the Maven repository for the short video SDK for Android

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   Core libraries

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.17.0
```


## V3.16.2

Feature updates

The Gaussian blur effect on backgrounds is improved.

Others

-   URL of the Maven repository for the short video SDK for Android

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   Core libraries

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.16.2
```


## V3.16.1

Feature updates

-   The issue is fixed where the number of words in each line of the added subtitles is different.
-   The issue is fixed where the subtitles and animated stickers do not move as specified during secondary editing.

Others

-   URL of the Maven repository for the short video SDK for Android

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   Core libraries

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.16.1
```


## V3.16.0

Feature updates

-   The major animation effects are added again.
-   The issue is fixed where intermittent unexpected quits occur when users send feedback online.
-   The issue is fixed where stuttering may occur during the playback of long videos.
-   The issue is fixed where the recording unexpectedly quits due to incompatibility with some phone models.

Others

-   URL of the Maven repository for the short video SDK for Android

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   Core libraries

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.16.0
```


## V3.15.0

Feature updates

-   The issue is fixed where stuttering occurs during the playback of produced videos.
-   The issue is fixed where the speed of multiple clips cannot be changed at the same time.
-   The issue is fixed where the exposure area of the front camera of specific phone models is invalid.
-   Two sets of transitions, filter effect transitions, and filters are added based on the standards of producing custom effects.

SDK changes

-   An interface is added to modify the parameters of custom effects in real time.
-   The features of custom filters and transitions are supported. For more information about the standards of producing custom effects, see the official documentation.

Others

-   URL of the Maven repository for the short video SDK for Android
-   Core libraries

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.3
com.aliyun.video.android:AlivcFFmpeg:2.0.0
com.aliyun.video.android:svideopro:3.15.0
```


## V3.14.0

Feature updates

-   The SDK is adapted to the Android Q system to improve the performance of recording, editing, and producing videos in the Android Q system.
-   The recording implementation is optimized and the issue of intermittent unexpected quits is fixed.
-   The known memory leaks are fixed and the performance of specific modules is optimized.

Fixed issues

-   The issue is fixed where the error code -10000004 is returned after you call specific methods.
-   The issue of intermittent stuck during video cropping is fixed.
-   The issue is fixed where deadlock may occur if you take a photo and adjust the focus at the same time during video recording.
-   The issue is fixed where the color setting of the background does not take effect.
-   The known memory leaks and other known issues are fixed.

Others

-   URL of the Maven repository for the short video SDK for Android

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   Core libraries

```
com.aliyun.video.android:core:1.2.2
com.alivc.conan:AlivcConan:1.0.2
com.aliyun.video.android:AlivcSvideoFFmpeg:1.1.0
com.aliyun.video.android:svideopro:3.14.0
```


## V3.13.0

Feature updates

-   The stability and performance of the recording module are optimized.
-   The Render And Compute Everything \(RACE\) engine-based face filters are added to the recording module.

SDK changes

The method for the music video \(MV\) effect is deprecated and the feature of adding the MV effect is removed.

Others

-   URL of the Maven repository for the short video SDK for Android

    ```
    maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
    ```

-   Core libraries

```
com.aliyun.video.android:core:1.2.2: corresponds to AlivcCore.jar.
com.alivc.conan:AlivcConan:1.0.1
com.aliyun.video.android:AlivcSvideoFFmpeg:1.0.2
com.aliyun.video.android:svideopro:3.13.0
```


## V3.12.0

Feature updates

-   The feature of log analysis is added.

    ```
    AlivcSdkCore#setDebugLoggerLevel(AlivcDebugLoggerLevel level)
    ```

    The following three options are provided:

    -   AlivcDLAll: Analyze all logs. We recommend that you use this option only for troubleshooting. We recommend that you do not use this option in the official release.
    -   AlivcDLNormal: Analyze warning or error logs. We recommend that you use this option to analyze logs.
    -   AlivcDLClose: Disable the feature of log analysis.
    The preceding options apply only to SDK logs.

-   The performance of the editing module is improved.

SDK changes

-   The addRunningDisplayMode method is deleted from the editing module.
-   The removeRunningDisplayMode method is deleted from the editing module.

Others

-   URL of the Maven repository for the short video SDK for Android

    ```
    maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
    ```

-   Core libraries

```
com.aliyun.video.android:core:1.2.2: corresponds to AlivcCore.jar.
com.alivc.conan:AlivcConan:1.0.1
com.aliyun.video.android:AlivcSvideoFFmpeg:1.0.2
com.aliyun.video.android:svideopro:3.12.0
```


## V3.11.0

Feature updates

-   The start and stop speeds of clip recording and the video production speed are improved, which enables smoother clip recording.
-   The granularity and accuracy of the recording progress callback are improved.
-   The transcoding speed in specific scenarios is improved by precisely adjusting the group of pictures \(GOP\) size.

SDK changes

-   All error codes are integrated into AliyunErrorCode.
-   The getErrorCodeMessage\(int errorCode\) method is added so that you can obtain the error description.

Fixed issues

-   The issue is fixed where the FILL mode does not take effect for obtaining the thumbnail frame and frames cannot be obtained from TikTok videos.
-   The issue is fixed where the first frame of the produced video in which the reverse playback effect is applied is a gray frame.
-   The issue is fixed where you cannot delete a doodle added to a paused video during editing.
-   The issue is fixed where the screen flickers during video recording after you delete a clip and crop the frame in the OpenH264 or FFmpeg encoding format.
-   The issue is fixed where the number of frames in a GIF image is not accurately parsed.
-   The issue is fixed where specific videos stutter when the videos are reversely played.
-   The issue is fixed where the audio and image of a multi-clip video are not synchronized.
-   The issue is fixed where the duration of a recorded video is inaccurate.

Others

-   URL of the Maven repository for the short video SDK for Android

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   Core libraries

```
om.aliyun.video.android:core:1.2.1: corresponds to AlivcCore.jar.
com.alivc.conan:AlivcConan:0.9.5.1
com.aliyun.video.android:AlivcSvideoFFmpeg:1.0.1
com.aliyun.video.android:svideopro:3.11.0: corresponds to the .so libraries of armeabi-v7a&arm64-v8a and the AliyunSdk-RCE.aar library, on which the short video SDK Professional Edition for Android depends.
```


## V3.10.5

Feature updates

-   The AliyunIMixRecorder interface is added. This interface can be called to record videos in duet mode.
-   The AliyunIMixComposer interface is added. This interface can be called to achieve effects such as picture-in-picture and left-right split-screen.

## V3.10.0

Feature updates

-   The voice effects of the big devil and Minions are added to the editing module.
-   Videos in the MJPEG format can be edited.
-   The compatibility with specific damaged video files is improved for playback during editing.
-   Hardware decoding is supported for High Efficiency Video Coding \(HEVC\) videos during editing and transcoding.
-   The transcoding speed is improved.
-   The AliyunIRecorder.resizePreviewSize method is added so that you can reset the size of the preview window during video recording.
-   Separate interfaces for producing and uploading videos are added.

Fixed issues

-   The issue is fixed where the duration is incorrectly displayed for a recorded video clip.
-   The issue is fixed where a memory leak may occur because specific handles are not released.

SDK changes

-   All error codes are integrated into AliyunErrorCode.
-   The getErrorCodeMessage\(int errorCode\) method is added so that you can obtain the error description.

Others

-   URL of the Maven repository for the short video SDK for Android

```
 maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   Core libraries

```
com.aliyun.video.android:core:1.1.2: corresponds to AlivcCore.jar.
com.alivc.conan:AlivcConan:0.9.4
com.aliyun.video.android:AlivcSvideoFFmpeg:1.0.0
com.aliyun.video.android:svideopro:3.10.0: corresponds to the .so libraries of armeabi-v7a&arm64-v8a and the AliyunSdk-RCE.aar library, on which the short video SDK Professional Edition for Android depends.
```


## V3.9.0

Feature updates

-   The seeking performance during editing is improved.
-   The voice effect feature is supported. The voice effects include lolita, uncle, reverberation, and echo.
-   The libAliFaceAREngine.so and libFaceAREngine.so libraries are combined to the libAliFaceAREngine.so library.

SDK changes

The thread triggered by OnFrameCallBack is changed to a child thread.

## V3.8.0

Feature updates

-   The playback capability during editing is optimized to ensure smooth playback.
-   The video production speed is improved for the editing module.
-   The preview resolution of recorded videos is optimized.
-   The recording frame rate on low-end devices is improved.
-   Maven dependencies are supported by the short video SDK for Android.

SDK changes

-   The threads used by the following methods of the RecordCallback interface are adjusted:

    -   RecordCallback\#onComplete: The thread used by this method is changed from the main thread to a child thread. If the method needs to be called to perform an operation on the user interface \(UI\), you must post the operation to the main thread.
    -   RecordCallback\#onProgress: The thread used by this method is changed from the main thread to a child thread. If the method needs to be called to perform an operation on the UI, you must post the operation to the main thread.
    -   RecordCallback\#onMaxDuration: The thread used by this method is changed from the main thread to a child thread. If the method needs to be called to perform an operation on the UI, you must post the operation to the main thread.
    -   RecordCallback\#onError: The thread used by this method is changed from the main thread to a child thread. If the method needs to be called to perform an operation on the UI, you must post the operation to the main thread.
    This adjustment ensures that callback data is the same as that in the SDK, which reduces exceptions.

-   The EditorCallback interface has the following changes:
    -   EditorCallback is changed from an interface to an abstract class.
    -   The mNeedRenderCallback parameter is added to enable or disable onCustomRender or onTextureRender. When onCustomRender and onTextureRender are disabled, the editing performance is improved. By default, onCustomRender and onTextureRender are disabled. To enable onCustomRender and onTextureRender, set this parameter in the following ways:

        ```
        mNeedRenderCallback = EditorCallBack.RENDER_CALLBACK_CUSTOM;// Enables onCustomRender.
        mNeedRenderCallback = EditorCallBack.RENDER_CALLBACK_TEXTURE;// Enables onTextureRender.
        mNeedRenderCallback = EditorCallBack.RENDER_CALLBACK_TEXTURE|EditorCallBack.RENDER_CALLBACK_CUSTOM;// Enables onCustomRender and onTextureRender at the same time.
        ```


Others

-   URL of the Maven repository for the short video SDK for Android

```
maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
```

-   Core libraries

```
compile 'com.aliyun.video.android:core:1.1.0': corresponds to AlivcCore.jar.
com.aliyun.video.android:svideopro:3.8.0: corresponds to the AliyunSdk-RCE.aar library, on which the short video SDK Professional Edition for Android depends.
com.aliyun.video.android:svideopro-armv7a:3.8.0: corresponds to all .so libraries of armeabi-v7a, on which the short video SDK Professional Edition for Android depends.
com.aliyun.video.android:svideopro-arm64:3.8.0: corresponds to all .so libraries of arm64-v8a, on which the short video SDK Professional Edition for Android depends.
```


**Note:** The upload SDK is removed from the short video SDK. If the upload feature is required, you must add the external dependency com.aliyun.video.android:upload:1.5.2'9 by using Gradle. To meet the requirement of SDK stability monitoring and data-related requirements in the future, you must add the com.alivc.conan:AlivcConan:0.9.0 dependency and obfuscation to the short video SDK. For more information, see the demo code.

## V3.7.8.1

SDK changes

The postToGl and removeFromGl methods are added to the AliyunIRecorder interface. You can use the two methods to post and remove operations to and from the GL thread. This way, GL dependencies are added or removed.

## V3.7.8

Feature updates

The frame rate for preview and recording is greatly optimized.

SDK changes

-   AliyunIRecorder.setDisplayView\(GLSurfaceView surfaceView\) is changed to AliyunIRecorder.setDisplayView\(SurfaceView surfaceView\). That is, GLSurfaceView is changed to SurfaceView in the setDisplayView method.
-   The OnTextureIdCallBack.onTextureDestroyed\(\) callback is added so that you can destroy GL resources during custom third-party rendering. Originally, you must call the GLSurfaceView.queueEvent method to destroy GL resources.
-   The surface size can be adjusted without the need to restart preview. If you need to reselect the collection resolution, you must restart preview.
-   The RecordCallback.onInitReady method is called only once in the setRecordCallback method when you create an AliyunIRecorder instance. This ensures compatibility with earlier versions. In fact, you can directly perform other operations after you create an AliyunIRecorder instance, without the need to wait for the RecordCallback.onInitReady callback.

## V3.7.7

Feature updates

The AlivcSdkCore class is added for debugging. The AlivcSdkCore\#register method is used to replace dynamic libraries in debugging mode. The AlivcSdkCore\#setLogLevel method is used to customize the log level.

Others

-   An [intelligent chatbot](https://h5.m.taobao.com/alicare/meebot.html?appKey=zjrE3jzzba&type=dingding_channel) that can answer your questions about the short video SDK is provided. To obtain precise answers, we recommend that you enter accurate keyword information, such as SDK documentation or how to add a common animated sticker.
-   The resolution of produced or cropped videos is improved.
-   The overall stability is improved.

## V3.7.5

Feature updates

-   The issue is fixed where unexpected quits may occur when a third-party rendering interface is used in editing.
-   The playback smoothness of videos with time effects is improved.
-   The compatibility with GIF images is improved.
-   Videos with odd resolution can be imported.
-   Audio and video synchronization during multi-clip recording is optimized.
-   The stability is improved.

## V3.7.0

Feature updates

-   The replay method for the preview in the editor is added. To replay a video, call the replay method after you receive the onEnd callback. For more information, see the demo code.
-   The implementation of the mute method AliyunIEditor\#setAudioSilence is modified. The same method in the current version mutes a video only during preview playback. To mute the audio in the produced audio, call the AliyunIEditor\#setVolume\(0\) method to set the output volume to 0.
-   The following methods are added to the editing interface AliyunPasterBaseView:

    ```
    getTextMaxLines // Obtains the maximum number of lines.
    getTextAlign() // Obtains the text alignment mode.
    getTextPaddingX() // Obtains the distance between the x-axis of the text and the left edge, with the upper-left corner as the origin.
    getTextPaddingY() // Obtains the distance between the y-axis of the text and the top edge, with the upper-left corner as the origin.
    getTextFixSize() // Obtains the font size of the text.
    getBackgroundBitmap() // Obtains the background image of the text.
    isTextHasLabel() // Indicates whether the text has a background color.
    getTextBgLabelColor() // Obtains the background color of the text. You must implement these methods by yourself.
                            
    ```

-   The playback logic after media clips are updated is modified. After you call the AliyunIEditor\#applySourceChange method to update media clips, the media clips are not automatically played. You must call the AliyunIEditor\#play method to start the playback.
-   The package name related to the AliyunIThumbnailFetcher interface for fetching a thumbnail or frame is changed. You can precompile the SDK code. When an error is reported during the compilation, delete the original import statement and import the correct package.
-   The data type of the parameter in the AliyunIThumbnailFetcher$OnThumbnailCompletion.onThumbnailReady\(\) method is changed from SharableBitmap to Bitmap. You can directly use this parameter without the need to recycle it.
-   The transition duration parameter is added to the addVideoSource and addImageSource methods of the AliyunIThumbnailFetcher interface. If the imported video or image requires transition duration, set this parameter to the required transition duration. Otherwise, set this parameter to 0.
-   The ScaleMode enumeration is replaced by the VideoDisplayMode enumeration.
-   Multiple instances are supported by the AliyunIReocder and AliyunICrop interfaces. The destroy method is deleted from the AliyunRecorderCreator and AliyunCropCreator classes.
-   The libQuCore-ThirdParty.so library is replaced by the libsvideo\_alivcffmpeg.so library.
-   The location of specific structure classes is changed. If a class is not found in the original package, delete the import statement for the class and import the correct package.
-   The issue is fixed where the SDK unexpectedly quits on specific phone models.
-   The issue is fixed where stuttering occurs during reverse playback.
-   The issue is fixed where animated filters are not properly displayed on specific phone models.
-   The TransitionBase class is added to provide the transition feature. For more information, see API Reference. Transition-related parameters inDuration, outDuration, and overlapDuration are deleted from the addVideo and addImage methods of the AliyunIimport interface. Subclasses of TransitionBase are used to provide more comprehensive transition effects.
-   The AliyunIEditor\#addFrameAnimation method is added so that you can customize animations. For more information, see API Reference.
-   Multiple speed control effects can be added to a multi-clip video. The repetition and reverse playback effects can be configured only for a single-clip video.
-   The AliyunIEditor\#deleteTimeEffect method is added so that you can delete a time effect.
-   The AliyunIEditor\#applyBlurBackground method is added so that you can add the Gaussian blur effect to the specified stream in the specified time period.
-   The AliyunIEditor\#addRunningDisplayMode method is added so that you can set the display mode to padding or cropping for the specified stream in the specified time period.
-   The AliyunIEditor\#applyDub method is added so that you can add dubbing. The dubbing is affected by time effects.

Others

The methods for configuring MVs during recording are deprecated, including the applyMv\(EffectBean effectMv\), pauseMv\(\), resumeMv\(\), and restartMv\(\) methods. The deprecated methods can still be used. They are to be deleted in a later version.

## V3.6.5

Feature updates

-   FFmpeg software coding is no longer supported for production.
-   The issue is fixed where the onEnd callback is triggered first when you add a time effect.
-   The issue is fixed where the volume that is specified during editing does not take effect during production. The volume is larger than that is specified, and the default volume of the SDK is modified.
-   The issue is fixed where specific videos are stuck at 99% during cropping.
-   The issue is fixed where specific videos that are cropped on mobile phones stutter during the preview playback.
-   The issue is fixed where animated filters have dashed lines on specific Huawei mobile phones.
-   The issue is fixed where the SDK unexpectedly quits when you remove music on specific phone models.
-   The issue is fixed where stuttering occurs during reverse playback.
-   The issue is fixed where a color gamut issue occurs when the BT.709 formula is used for YUV-to-RGB conversion.
-   Audio files in the AAC SBR format are supported.
-   The issue is fixed where the audio sample rate is invalid.
-   The issue is fixed where animated filters are not properly displayed.
-   The upload library is updated. Your short video application needs to integrate the new version of the SDK to use the new fields.

SDK changes

The Alivc.jar package is added. You must add the dependency on this package to your project.

## V3.6.0

SDK changes

-   The parameters of the addVideo and addImage methods for multi-video import are modified. The fadeDuration parameter is split into the outDuration, inDuration, and overlapDuration parameters. The outDuration parameter specifies the duration for displaying the transition in the previous video. The inDuration parameter specifies the duration for displaying the transition in the next video. The overlapDuration parameter specifies the overlapping duration between the two videos.
-   The callback parameter of the EditorCallBack type is added to the AliyunEditorFactory.creatAliyunEditor method, which originally has only the uri parameter. The EditorCallback class is a new class that replaces the OnPlayCallback class.

    |Original method|New method|
    |---------------|----------|
    |OnPlayCallback.onPlayCompleted|EditorCallback.onEnd|
    |OnPlayCallback.onError|EditorCallback.onError|
    |OnPlayCallback.onTextureIDCallback|EditorCallback.onCustomRender|
    |OnPlayCallback.onPlayStarted \(This method is deleted.\)|OnPlayCallback.onSeekDone \(This method is deleted.\)|

-   The AliyunIPlayer interface and the createAliyunPlayer\(\) method for creating a player instance are deleted. You can use the methods of AliyunIEditor for playback control, as described in the following table.

    |Original method|New method|
    |---------------|----------|
    |AliyunIPlayer.getCurrentPosition|AliyunIEditor.getCurrentPlayPosition|
    |AliyunIPlayer.getDuration|AliyunIEditor.getDuration|
    |AliyunIPlayer.getRotation|AliyunIEditor.getRotation|
    |AliyunIPlayer.getVideoHeight|AliyunIEditor.getVideoHeight|
    |AliyunIPlayer.getVideoWidth|AliyunIEditor.getVideoWidth|
    |AliyunIPlayer.isAudioSilent|AliyunIEditor.isAudioSilense|
    |AliyunIPlayer.isPlaying|AliyunIEditor.isPlaying|
    |AliyunIPlayer.pause|AliyunIEditor.pause|
    |AliyunIPlayer.resume|AliyunIEditor.resume|
    |AliyunIPlayer.seek|AliyunIEditor.seek|
    |AliyunIPlayer.setAudioSilense|AliyunIEditor.setAudioSilense|
    |AliyunIPlayer.setDisplayMode|AliyunIEditor.setDisplayMode|
    |AliyunIPlayer.setFillBackgroundColor|AliyunIEditor.setFillBackgroundColor|
    |AliyunIPlayer.setOnPlayCallbackListene \(This method is deleted.\)|AliyunIPlayer.setOnPreparedListener \(This method is deleted.\)|
    |AliyunIPlayer.setVolume|AliyunIEditor.setVolume|
    |AliyunIPlayer.start|AliyunIEditor.start|
    |AliyunIPlayer.stop|AliyunIEditor.stop|


**Note:** The OnPreparedListener method is deleted in this version. You can add effects immediately after an AliyunIEditor instance is initialized, without the need to wait for the OnPrepared callback.

Others

-   The id parameter is added to the applyMusicMixWeight method. This version allows you to add multiple dubbing tracks. Therefore, IDs are needed to distinguish the tracks. For more information about this method, see API Reference.
-   The getExporter method is deleted. You can use the production methods in AliyunIEditor to produce videos.

    |Original method|New method|
    |---------------|----------|
    |AliyunIExporter.startCompose|compose|
    |AliyunIExporter.cance|cancelCompose|
    |AliyunIExporter.setTailWatermark \(This method is deleted.\)|AliyunIExporter.clearTailWatermark \(This method is deleted.\)|

-   The OnComposeCallback parameter is changed to the AliyunIComposeCallBack parameter in the AliyunICompose.startCompose method.
-   The AliyunIEditor\#saveEffectToLocal\(\) method must be called before you create a production instance.

**Note:** The release notes do not cover all changes to parameters of methods. If a parameter-related error is reported during compilation, you can modify your code based on the parameter description in the API Reference.

