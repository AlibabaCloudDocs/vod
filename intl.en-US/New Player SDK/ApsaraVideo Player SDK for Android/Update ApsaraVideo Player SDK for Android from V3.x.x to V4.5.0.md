# Update ApsaraVideo Player SDK for Android from V3.x.x to V4.5.0

This topic describes the major changes and updates of ApsaraVideo Player SDK V4.5.0 for Android compared with V3.x.x, in terms of the unified player, dependencies, class names, and methods. This topic also describes how to update ApsaraVideo Player SDK for Android from V3.x.x to V4.5.0.

## Unified player

-   ApsaraVideo Player SDK V3.x.x for Android provides the following two player objects for you to play videos from specified URLs and videos with specified video IDs \(VIDs\):
    -   AlivcMediaPlayer
    -   AliyunVodPlayer
-   In ApsaraVideo Player SDK V4.5.0 for Android, AlivcMediaPlayer and AliyunVodPlayer are integrated. The AliPlayer class is used to play both videos from specified URLs and videos with specified VIDs.

**Note:** You can follow instructions in this topic to update ApsaraVideo Player SDK for Android to V4.5.0 or later. Pay attention to the specific version number.

## Changes in dependencies

-   ApsaraVideo Player SDK V3.x.x for Android contains the following dependency files:
    -   AlivcPlayer-3.x.x.aar
    -   AlivcReporter-1.2.aar
    -   AliyunVodPlayer-3.x.x.aar
    -   The SDK also contains a Gradle package compile 'com.aliyun.dpa:oss-android-sdk:+'.
-   ApsaraVideo Player SDK V4.5.0 for Android contains the following dependency files:
    -   AliyunPlayer-4.5.0-full.aar
    -   implementation 'com.alivc.conan:AlivcConan:0.9.5'

## Changes in class names and methods

In ApsaraVideo Player SDK V4.5.0 for Android, some class names are changed, and new features and callbacks are added. Some methods in ApsaraVideo Player SDK V3.x.x for Android are removed.

## Changes to obfuscation configuration

The following code shows the obfuscation configuration of ApsaraVideo Player SDK V4.5.0 for Android:

```
  -keep class com.alivc.**{*;}
  -keep class com.aliyun.**{*;}
  -keep class com.cicada.**{*;}
  -dontwarn com.alivc.**
  -dontwarn com.aliyun. **
```

## Update practices

The following section describes how to update ApsaraVideo Player SDK for Android from V3.4.10 to V4.5.0.

**Note:** The procedure for updating ApsaraVideo Player SDK for Android from V3.x.x to V4.5.0 is similar.

1.  Replace the dependencies.
    -   ApsaraVideo Player SDK V3.4.10 for Android contains the following dependency files:
        -   AlivcPlayer-3.4.10.aar
        -   AlivcReporter-1.2.aar
        -   AliyunVodPlayer-3.4.10.aar
        -   The SDK also contains a Gradle package compile 'com.aliyun.dpa:oss-android-sdk:+'.
    -   ApsaraVideo Player SDK V4.5.0 for Android contains the following dependency files:
        -   AliyunPlayer-4.5.0-full.aar
        -   implementation 'com.alivc.conan:AlivcConan:0.9.5'
    1.  Local dependencies:

        If you use local dependencies, you must replace local dependencies and the Gradle package.

        1.  Replace local dependencies:

            Replace AlivcPlayer-3.4.10.aar, AlivcReporter-1.2.aar, and AliyunVodPlayer-3.4.10.aar with AliyunPlayer-4.5.0-full.aar.

            ![Replace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3180401161/p209536.png)

            The following figure shows the replacement result.

            ![Result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3180401161/p209537.png)

        2.  Add Alibaba Cloud Maven repository URL:

            Add Alibaba Cloud Maven repository URL to the buildscript block and the allprojects block in the build.gradle file. Example:

            ```
            maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
            ```

            The following figure shows the build.gradle file after you add the URL. The URL in the following figure is for reference only. Use the URL in the preceding code.

            ![Screenshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4180401161/p209539.png)

        3.  Replace the Gradle package:

            Replace the OSS dependency with a Conan dependency. The following figure shows the replacement result.

            ![Modify](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4180401161/p183057.png)

    2.  Gradle dependency:

        If you use Gradle dependency, you must delete local dependencies and replace the Gradle package.

        1.  Replace the Gradle package.

            ![Replace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4180401161/p183060.png)

            Delete the AlivcPlayer-3.4.10.aar, AlivcReporter-1.2.aar, and AliyunVodPlayer-3.4.10.aar packages.

            ![Delete](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4180401161/p183062.png)

        2.  Add Alibaba Cloud Maven repository URL:

            Add Alibaba Cloud Maven repository URL to the buildscript block and the allprojects block in the build.gradle file.

            ```
            maven { url "http://maven.aliyun.com/nexus/content/repositories/releases" }
            ```

            The following figure shows the build.gradle file after you add the URL. The URL in the following figure is for reference only. Use the URL in the preceding code.

            ![Result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4180401161/p183065.png)

        3.  Replace the Gradle package:

            Add the reference to the AAR package to the dependencies part in the build.gradle file. Example:

            ```
            implementation 'com.aliyun.sdk.android:AliyunPlayer:4.5.0-full'
            implementation 'com.alivc.conan:AlivcConan:0.9.5'
            ```

    3.  Integration of the short video SDK

        To integrate a player SDK that supports short video playback, you must use AliyunPlayer-4.5.0-part.aar as the dependency. In addition, you must add the com.aliyun.video.android:AlivcFFmpeg:1.0.0 package, the version of which is compatible for both the player SDK and the short video SDK.

        **Note:** An FFmpeg error may occur if you choose an invalid dependency for SDK integration.

2.  Modify code.

    After you replace the dependencies, an error occurs when you start to compile the project. You must use classes and methods that are provided by ApsaraVideo Player SDK V4.5.0 for Android to resolve the error. Compared with V3.4.10, class names and API operations are changed in V4.5.0. You must pay attention to the following changes:

    1.  Change of the player creation method

        ApsaraVideo Player SDK V4.5.0 for Android provides the `AliPlayer` class for you to define a player object. You can use the `AliPlayerFactory` class to create a player object. Example:

        ```
        // Define a player object.
        AliPlayer mAliyunVodPlayer;
        ...
        // Create a player object.
        mAliyunVodPlayer = AliPlayerFactory.createAliPlayer(getContext().getApplicationContext());
        ```

    2.  Changes of listeners

        In ApsaraVideo Player SDK V3.4.10 for Android, you can find listeners in the `IAliyunVodPlayer` class. In ApsaraVideo Player SDK V4.5.0 for Android, you can find listeners in the `IPlayer` class. Only specific class names are changed. Therefore, you must change these class names to modify listeners. The following figure shows how the `OnPreparedListener` callback is set in ApsaraVideo Player SDK V3.4.10 for Android.

        ![Class name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4180401161/p183071.png)

        The following figure shows the modified class name.

        ![Class name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4180401161/p183074.png)

        -   For most listeners, you only need to replace the class name. However, for listeners that are deleted or newly added, you must modify the related operations. The following table describes changes in listeners.

            |Method|Feature|Change|
            |------|-------|------|
            |OnPreparedListener|The listener for successful preparation.|Not changed|
            |OnSeekCompleteListener|The listener for the completion of seeking.|Not changed|
            |OnCompletionListener|The listener for the completion of playback.|Not changed|
            |OnFirstFrameStartListener|The listener for the appearance of the first frame.|OnRenderingStartListener|
            |OnStoppedListener|The listener for the stop of video playback.|OnStateChangedListener|
            |OnPcmDataListener|The callback for pulse-code modulation \(PCM\) audio data.|Deleted|
            |OnCircleStartListener|The listener for the start of loop playback.|OnInfoListener|
            |OnLoadingListener|The listener for video loading.|OnLoadingStatusListener|
            |OnBufferingUpdateListener|The listener that indicates the progress of video buffering.|OnInfoListener|
            |OnErrorListener|The listener for a playback error.|OnErrorListener|
            |OnInfoListener|The listener for playback information.|OnInfoListener|
            |OnVideoSizeChangedListener|The callback for the change of the video image size.|Not changed|
            |OnChangeQualityListener|The listener for video resolution switching.|OnTrackChangedListener|
            |LockPortraitListener|The listener for the lock of portrait display.|Deleted|
            |OnRePlayListener|The listener for the start of replay.|Deleted|
            |OnAutoPlayListener|The listener for the start of autoplay.|OnInfoListener|
            |OnTimeShiftUpdaterListener|The listener for the change of time shifting during live streaming.|Classified into the AliLiveshiftPlayer class|
            |OnSeekLiveCompletionListener|The listener for the completion of time shifting seeking during live streaming.|Classified into the AliLiveshiftPlayer class|
            |OnTimeExpiredErrorListener|The listener for the expiration of request information.|OnErrorListener|
            |OnUrlTimeExpiredListener|The listener for the event that the video playback URL is about to expire.|Deleted|
            |OnTrackReadyListener|The listener for obtaining the stream.|New|
            |OnSubtitleDisplayListener|The listener for obtaining the time when subtitles are displayed.|New|
            |OnSnapShotListener|The listener for the snapshot result.|New|

        -   Details of changed listeners:

            OnFirstFrameStartListener: the listener for the appearance of the first frame. Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnFirstFrameStartListener` of the OnRenderingStartListener method is replaced by `OnRenderingStartListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnRenderingStartListener {
                 void onRenderingStart();
            }
            public void setOnRenderingStartListener(OnRenderingStartListener l);
            ```

            OnStoppedListener: the listener for the stop of video playback. Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnStoppedListener` is replaced by `OnStateChangedListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnStateChangedListener {
                void onStateChanged(int newState);
            }
            public void setOnStateChangedListener(OnStateChangedListener l);
            ```

            The `newState` parameter of the `OnStateChangedListener` callback indicates the new status of the player. It provides multiple values to indicate various statuses. The value of the status is defined in the IPlayer class. Example:

            ```
            /**
             * Unknown status.
             */
            public static final int unknow = -1;
             /**
             * Indicates that the player is idle when it is created.
             */
            public static final int idle = 0;
            /**
             * Indicates that the player is initialized after you set the playback source.
             */
            public static final int initalized = 1;//
            /**
             * Indicates that playback is prepared.
             */
            public static final int prepared = 2;
            /**
             * Indicates that the player is playing a file.
             */
            public static final int started = 3;
            /**
             * Indicates that the player pauses the playback.
             */
            public static final int paused = 4;
            /**
             * Indicates that the player stops the playback.
             */
            public static final int stopped = 5;
            /**
             * Indicates that the playback is completed.
             */
            public static final int completion = 6;
            /**
             * Indicates that a playback error occurs.
             */
            public static final int error = 7;
            ```

            OnCircleStartListener: the listener for the start of loop playback.

            Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnCircleStartListener` is replaced by `OnInfoListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnInfoListener {
                void onInfo(InfoBean infoBean);
            }
            public void setOnInfoListener(OnInfoListener l);
            ```

            **Note:** The InfoBean.getCode\(\) = InfoCode.LoopingStart callback is fired when the loop playback starts.

            OnLoadingListener: the listener for video loading.

            Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnLoadingListener` is replaced by `OnLoadingStatusListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnLoadingStatusListener {
                void onLoadingBegin();
                void onLoadingProgress(int percent, float netSpeed);  // The unit of the percent parameter is percentage. The unit of the netSpeed parameter is Kbit/s.
                void onLoadingEnd();
            }
            public void setOnLoadingStatusListener(OnLoadingStatusListener l);
            ```

            **Note:** The value of the netSpeed parameter in the onLoadingProgress method is 0.

            OnBufferingUpdateListener: the listener that indicates the progress of video buffering.

            Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnBufferingUpdateListener` is replaced by `OnInfoListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnInfoListener {
                 void onInfo(InfoBean infoBean);
            }
            public void setOnInfoListener(OnInfoListener l);
            ```

            **Note:** The InfoBean.getCode\(\) = InfoCode.BufferedPosition callback is fired when the buffering progress is updated. You can call the `InfoBean.getExtraValue()` method to obtain the buffering progress information. The `InfoBean.getCode() = InfoCode.CurrentPosition` callback is fired when the playback progress is updated. You can call the `InfoBean.getExtraValue()` method to obtain the playback progress information.

            OnErrorListener: the listener for a playback error.

            Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnErrorListener` is replaced by `OnErrorListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnErrorListener {
                void onError(ErrorInfo errorInfo);
            }
            public void setOnErrorListener(OnErrorListener l);
            ```

            **Note:** ErrorInfo is the error information class. You can call the `ErrorInfo.getCode()` method to obtain the error code, and call the `ErrorInfo.getMsg()` method to obtain the error message.

            OnInfoListener: the listener for playback information.

            Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnBufferingUpdateListener` is replaced by `OnInfoListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnInfoListener {
                void onInfo(InfoBean infoBean);
            }
            public void setOnInfoListener(OnInfoListener l);
            ```

            InfoBean is the playback information class. You can call the `InfoBean.getCode()` method to obtain the playback information code, and call the `InfoBean.getExtraMsg()` method to obtain the playback information message. InfoCode contains the following values:

            ```
            /**
             * Unknown.
             */
            Unknown(-1);
            /**
             * Indicates that loop playback starts. No extra value is available.
             */
            LoopingStart(0),
            /**
             * Indicates the buffer position. The extra value indicates the current buffer position. Unit: milliseconds.
             */
            BufferedPosition(1),
            /**
             * Indicates the current playback position. The extra value indicates the current playback position. Unit: milliseconds.
             */
            CurrentPosition(2),
            /**
             * Indicates that autoplay starts. No extra value is available.
             */
            AutoPlayStart(3),
            /**
             * Indicates that hardware decoding is switched to software decoding. The extra value provides detailed description.
             */
            SwitchToSoftwareVideoDecoder(100),
            /**
             * Indicates that the audio decoding format is not supported. The extra value provides detailed description.
             */
            AudioCodecNotSupport(101),
            /**
             * Indicates that the audio decoder failed. The extra value provides detailed description.
             */
            AudioDecoderDeviceError(102),
            /**
             * Indicates that the video decoding format is not supported. The extra value provides detailed description.
             */
            VideoCodecNotSupport(103),
            /**
             * Indicates that the video decoder failed. The extra value provides detailed description.
             */
            VideoDecoderDeviceError(104),
            /**
             * Indicates that a network error occurs. You must try again. No extra value is available.
             */
            NetworkRetry(107),
            /**
             * Indicates that the caching succeeds. No extra value is available.
             */
            CacheSuccess(108),
            /**
             * Indicates that the caching failed. The extra value provides detailed description.
             */
            CacheError(109),
            /**
             * Indicates that no system memory is available for storing media data.
             */
            LowMemory(110),
            ```

            OnChangeQualityListener: the listener for video resolution switching.

            Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnChangeQualityListener` is replaced by `OnTrackChangedListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnTrackChangedListener {
                void onChangedSuccess(TrackInfo trackInfo);
                void onChangedFail(TrackInfo trackInfo, ErrorInfo errorInfo);
            }
            public void setOnTrackChangedListener(OnTrackChangedListener l);
            ```

            **Note:** The OnTrackChangedListener callback is fired after the `selectTrack(index)` method is called.

            OnAutoPlayListener: the listener for the start of autoplay.

            Compared with ApsaraVideo Player SDK V3.4.10 for Android, `OnAutoPlayListener` is replaced by `OnInfoListener` in ApsaraVideo Player SDK V4.5.0 for Android. Example:

            ```
            public interface OnInfoListener {
                void onInfo(InfoBean infoBean);
            }
            public void setOnInfoListener(OnInfoListener l);
            ```

            **Note:** ErrorInfo is the error information class. You can call the `ErrorInfo.getCode()` method to obtain the error code, and call the `ErrorInfo.getMsg()` method to obtain the error message. For more information about expiration error codes, see [Error codes](/intl.en-US/New Player SDK/Error codes.md).

3.  Set the playback source.

    ApsaraVideo Player SDK V3.4.10 for Android calls the `prepareAsync` method to set parameters for the playback source, and then automatically prepares the player. In ApsaraVideo Player SDK V4.5.0 for Android, call the `AliPlayer.setDataSource` method to set parameters for the playback source. Then, call the `AliPlayer.prepare` method to prepare the playback source. Example:

    ```
    /**
     * Set UrlSource.
     */
    public void setDataSource(UrlSource urlSource);
    /**
     * Set VidSts.
     */
    public void setDataSource(VidSts vidSts);
    /**
     * Set VidAuth.
     */
    public void setDataSource(VidAuth vidAuth);
    /**
     * Set VidMps.
     */
    public void setDataSource(VidMps vidMps);
    ```

    To set the time shifting feature for live streaming, call the `AliLiveShiftPlayer.setDataSource` method. Example:

    ```
    /**
     * Set the data source.
     */
    public void setDataSource(LiveShift liveShift);    
    ```

    **Note:** In ApsaraVideo Player SDK V4.5.0 for Android that provides the AliPlayer class to replace the AlivcMediaPlayer class, you can set UrlSource for URL-based playback.

4.  Main API operations

    |Operation in V3.4.10|Operation in V4.5.0|Description|
    |--------------------|-------------------|-----------|
    |surfaceChanged|redraw|Indicates that the surface changes.|
    |getPlayerState|OnStateChangedListener|Indicates the player status.|

    **Note:** For more information about other API operations, see [List of operations by function](/intl.en-US/API Reference/API overview.md).


## Documents of ApsaraVideo Player SDK V3.x.x for Android

-   [ApsaraVideo Player Basic](https://help.aliyun.com/document_detail/61908.html?spm=a2c4g.11186623.2.26.71aa1ee2MiTIMm#topic5330)
-   [ApsaraVideo Player Pro](https://help.aliyun.com/document_detail/61910.html?spm=a2c4g.11186623.2.27.37e21ee2dYuSGL#topic-2304652)
-   [API operations for ApsaraVideo Player Basic](https://help.aliyun.com/document_detail/61917.html?spm=a2c4g.11186623.2.28.37e21ee26WHy6f#topic14474)
-   [API operations for ApsaraVideo Player Pro](https://help.aliyun.com/document_detail/61918.html?spm=a2c4g.11186623.2.29.37e21ee2WXbFky#topic-2304654)

