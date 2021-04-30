# Implementation

This topic describes how to implement various features of ApsaraVideo Player SDK for Windows. This topic also provides sample code so that you can implement the features with ease.

## Playback

This section describes how to use ApsaraVideo Player SDK for Windows to play videos.

1.  Create a player. Sample code:

    ```
    using namespace alivc_player;
    AliPlayer* mPlayerPtr = AliPlayer::CreatePlayer();
    ```

    Assume that you use the secure download mode to download videos that are encrypted and transcoded by Alibaba Cloud. You must configure a security file encryptedApp.dat for encryption verification. For more information, see [How can I obtain a security file?](/intl.en-US/FAQ/Player/How can I obtain a security file?.md).

    ```
    mPlayerPtr->setListener(new AVPListenerImpl);
    ```

2.  Set player listeners.

    ApsaraVideo Player SDK provides multiple callbacks, such as onPlayerEvent and onError. To use these callbacks, create a class to inherit IAVPListener and implement the pure virtual functions of the class.

    ```
    mPlayerPtr->setListener(new AVPListenerImpl);
    ```

3.  Set the playback source and prepare the player.

    ApsaraVideo Player SDK supports four types of playback sources.

    -   AVPVidStsSource
    -   AVPVidAuthSource
    -   AVPVidMpsSource
    -   AVPUrlSource
    You can use AVPUrlSource for URL-based playback, and use AVPVidStsSource, AVPVidAuthSource, and AVPVidMpsSource for video ID-based playback. We recommend that you use AVPVidAuthSource for ApsaraVideo VOD. AVPVidMpsSource can be used only for ApsaraVideo for Media Processing. In this example, AVPVidStsSource is used.

    ```
    AVPVidStsSource vidSource;
    vidSource.initWithVid(Video ID,
                            "accessKeyId",
                            "accessKeySecret",
                            "Security token",
                            "Access region",
                            nullptr);
    mPlayerPtr->setSource(vidSource);
    mPlayerPtr->prepare();
    ```

    -   For more information about playback in ApsaraVideo for Media Processing, see [Play videos](https://help.aliyun.com/document_detail/53522.html?spm=a2c4g.11186623.2.39.16b44869I36VGN).
    -   For more information about playback based on a playback credential, see [Use playback credentials to play videos](/intl.en-US/Developer Guide/Video play/Use playback credentials to play videos.md).
    -   For more information about access regions, see [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md).
4.  Set the UI view. Sample code:

    ```
    mPlayerPtr->setView((void *) The window handle (HWND) of the UI view);
    ```

5.  Set playback control.

    When the player is prepared, the onPlayerEvent callback is fired and a notification of the AVPEventPrepareDone event is returned. Then, you can start the playback and set playback control. You can create playback control buttons and associate click events with playback control methods to implement playback control. The basic control features include play, stop, pause, and seek. The seek feature applies only to ApsaraVideo VOD. If you pause a live stream, the playback stops at the current position. If you resume the live stream, the playback starts from the current position. Sample code:

    ```
    // Start the playback.
    mPlayerPtr->start();
    // Pause the playback.
    mPlayerPtr->pause();
    // Stop the playback.
    mPlayerPtr->stop();
    // Seek to a position at a specific point in time. The seek feature supports both precise and imprecise modes. Imprecise seek navigates you to the nearest next keyframe of the video. Precise seek navigates you to the video image at the specified point in time, but is slower than imprecise seek.
    mPlayerPtr->seekToTime(int64_t time_in_ms, mode);
    // Reset the player.
    mPlayerPtr->reset();
    // Destroy the player.
    mPlayerPtr->destroy();
    ```

6.  Switch the bitrate.

    ApsaraVideo Player SDK allows you to play videos in different bitrates by using the HTTP Live Streaming \(HLS\) protocol. After the player is prepared, you can call the getMediaInfo method to obtain the value of the TrackInfo parameter. The TrackInfo parameter indicates the bitrate information. Sample code:

    ```
    AVPMediaInfo mediaInfo = mPlayerPtr->getMediaInfo();
    for (int i = 0; i < mediaInfo.trackCount; i++) {
        AVPTrackInfo *trackInfo = mediaInfo.tracks[i];
    }
    ```

    During the playback, you can call the selectTrack method to switch the bitrate. You can view the bitrate switching result after the onTrackChanged callback in IAVPListener is fired. Sample code:

    ```
    int trackIndex = trackInfo->trackIndex;
    mPlayerPtr->selectTrack(trackIndex);
    ```

7.  Set autoplay.

    ApsaraVideo Player SDK supports video autoplay. Set autoplay before you call the prepare method.

    ```
    mPlayerPtr->setAutoPlay(true);
    ```

    After you set autoplay, the player automatically starts the playback when it is prepared. Sample code:

    ```
    void onPlayerEvent(AliPlayer *player, AVPEventType eventType)
    {
        if (eventType == AVPEventPrepareDone) {
            // The player is prepared.
        }
        else if (eventType == AVPEventAutoPlayStart) {
            // The player automatically starts the playback.
        }
    }
    ```

    **Note:** When the onPlayerEvent callback in IAVPListener is fired during autoplay, a notification of the AVPEventAutoPlayStart event instead of the AVPEventPrepareDone event is returned.

8.  Set loop playback.

    ApsaraVideo Player SDK supports loop playback. Call the setLoop method to enable the loop playback feature. The player automatically plays a video all over again each time the playback is complete. A notification of the AVPEventLoopingStart event is returned to start the loop playback. Sample code:

    ```
    mPlayerPtr->setLoop(true);
    ```

9.  Set video image rotation, scaling, and mirroring.

    ApsaraVideo Player SDK provides multiple operations for you to precisely control the video images. You can set the rotation angle, scaling mode, and mirroring mode for video images. Sample code:

    ```
    // Set the mirroring mode: horizontal mirroring, vertical mirroring, and no mirroring.
    mPlayerPtr->setMirrorMode(AVP_MIRRORMODE_HORIZONTAL);
    // Set the rotation angel: 0°, 90°, 180°, and 270°.
    mPlayerPtr->setRotateMode(AVP_ROTATE_0);
    // Set the scaling mode: aspect ratio-based padding, aspect ratio-based fitting, and stretching.
    mPlayerPtr->setScalingMode(AVP_SCALINGMODE_SCALEASPECTFILL);
    ```

    The following table describes the values of the rotateMode parameter.

    |Value|Description|
    |-----|-----------|
    |AVP\_ROTATE\_0|Indicates that the rotation angle is 0°, in the clockwise direction.|
    |AVP\_ROTATE\_90|Indicates that the rotation angle is 90°, in the clockwise direction.|
    |AVP\_ROTATE\_180|Indicates that the rotation angle is 180°, in the clockwise direction.|
    |AVP\_ROTATE\_270|Indicates that the rotation angle is 270°, in the clockwise direction.|

    The following table describes the values of the scalingMode parameter.

    |Value|Description|
    |-----|-----------|
    |AVP\_SCALINGMODE\_SCALEASPECTFIT|Indicates that the video image is scaled down into the UI view without changing the aspect ratio. This prevents image distortion.|
    |AVP\_SCALINGMODE\_SCALEASPECTFILL|Indicates that the video image is scaled up to fill the UI view without changing the aspect ratio. This prevents image distortion.|
    |AVP\_SCALINGMODE\_SCALETOFILL|Indicates that the video image is stretched to fill the UI view. This may cause image distortion if the video image and the UI view do not match in the aspect ratio.|

    The following table describes the values of the mirrorMode parameter.

    |Value|Description|
    |-----|-----------|
    |AVP\_MIRRORMODE\_NONE|Indicates that mirroring is disabled.|
    |AVP\_MIRRORMODE\_HORIZONTAL|Indicates horizontal mirroring.|
    |AVP\_MIRRORMODE\_VERTICAL|Indicates vertical mirroring.|

10. Set the mute mode and volume control.

    ApsaraVideo Player SDK supports volume control for videos. You can call the setMute method to set the mute mode for the player. You can call the setVolume method to set the player volume. Valid values: **0 to 2.0**. Sample code:

    ```
    mPlayerPtr->setMute(true);
    mPlayerPtr->setVolume(1.0f);
    ```

11. Set the playback speed.

    ApsaraVideo Player SDK allows you to set the playback speed. You can call the setRate method to change the playback speed from 0.5x to 2x. The audio pitch remains unchanged at different speeds. Sample code:

    ```
    mPlayerPtr->setRate(1.5);
    ```

12. Enable or disable hardware decoding.

    ApsaraVideo Player SDK supports H.264 and H.265 hardware decoding. You can call the enableHardwareDecoder method to enable or disable hardware decoding. By default, the hardware decoding feature is enabled. If hardware decoding fails to be initialized, it is switched to software decoding to ensure normal playback. Sample code:

    ```
    mPlayerPtr->enableHardwareDecoder(true);
    ```

13. Set the referer.

    ApsaraVideo Player SDK provides the AVPConfig class for you to set the request referer. You can set a referer blacklist or whitelist in the ApsaraVideo VOD console to implement access control. Sample code:

    ```
    // Obtain the configuration information.
    AVPConfig *pConfig = mPlayerPtr->getConfig();
    // Set the referer.
    pConfig->referer = referer;
    ....// Set other parameters.
    // Configure the settings for the player.
    mPlayerPtr->setConfig(pConfig);
    ```

14. Specify the user agent.

    ApsaraVideo Player SDK provides the AVPConfig class for you to specify the request user agent. After you specify the user agent, the player contains the user agent information in its requests. Sample code:

    ```
    // Obtain the configuration information.
    AVPConfig *pConfig = mPlayerPtr->getConfig();
    // Specify the user agent.
    pConfig->userAgent = userAgent;
    ....// Set other parameters.
    // Configure the settings for the player.
    mPlayerPtr->setConfig(pConfig);
    ```

15. Specify the network timeout period and retries.

    You can use the AVPConfig class to specify the network timeout period and the number of retries. Sample code:

    ```
    // Obtain the configuration information.
    AVPConfig *pConfig = mPlayerPtr->getConfig();
    // Specify the network timeout period, in milliseconds.
    pConfig->networkTimeout = 5000;
    // Specify the number of retries upon a network timeout. The retry interval equals the value of the networkTimeout parameter. The networkRetryCount parameter specifies the number of retries. A value of 0 indicates zero retry. The application determines the number of retries. Default value: 2.
    pConfig->networkRetryCount = 2;
    ....// Set other parameters.
    // Configure the settings for the player.
    mPlayerPtr->setConfig(pConfig);
    ```

    **Note:**

    -   If you set the networkRetryCount parameter to a value other than 0, the player retries playback when the player starts to load data due to a network error. The number of retries equals the value of the networkRetryCount parameter. The retry interval equals the value of the networkTimeout parameter.
    -   If the player is still loading data after the maximum number of retries, the onError callback is fired. In this case, the ERROR\_LOADING\_TIMEOUT error is returned in the code parameter of the AVPErrorModel class.
    -   If you set the networkRetryCount parameter to 0, the onPlayerEvent callback is fired when the network connection times out. The value of the eventWithString parameter is EVENT\_PLAYER\_NETWORK\_RETRY. To resolve this issue, call the reload method to reload data or perform other operations as required.
16. Control the buffer and latency.

    Buffer control is important for a player. You can significantly shorten the startup loading time and smooth the playback based on proper configuration. ApsaraVideo Player SDK provides the AVPConfig class for you to control the buffer and latency. Sample code:

    ```
    // Obtain the configuration information.
    AVPConfig *pConfig = mPlayerPtr->getConfig();
    // Set the maximum latency. Note: This parameter is valid only for live streaming. If the latency exceeds the maximum limit, ApsaraVideo Player SDK synchronizes frames to ensure that the latency is within the limit.
    pConfig->maxDelayTime = 5000;
    // Set the maximum buffer duration, in milliseconds. This parameter specifies the maximum buffer duration for the player to load data at a time.
    pConfig->maxBufferDuration = 50000;
    // Set the peak buffer duration, in milliseconds. The player starts to load data when the network condition is poor. This parameter specifies the buffer duration beyond which the player stops loading data in this case.
    pConfig->highBufferDuration = 3000;
    // Set the startup loading duration, in milliseconds. A smaller value indicates a shorter startup loading time. In this case, the player starts to load data sooner after the start of playback.
    pConfig->startBufferDuration = 500;
    // Set other parameters.
    // Configure the settings for the player.
    mPlayerPtr->setConfig(pConfig);
    ```

    **Note:** Make sure that the value of the startBufferDuration parameter is not greater than the value of the highBufferDuration parameter. Make sure that the value of the highBufferDuration parameter is not greater than the value of the maxBufferDuration parameter.

17. Configure HTTP headers.

    ApsaraVideo Player SDK provides the AVPConfig class for you to configure HTTP headers for the player. Sample code:

    ```
    // Obtain the configuration information.
    AVPConfig *pConfig = mPlayerPtr->getConfig();
    // Configure the headers.
    pConfig->headerCount = 1;
    pConfig->httpHeaders = new char *[pConfig->headerCount];
    // Configure a host when you use Alibaba Cloud HTTPDNS.
    pConfig->httpHeaders[0] = strdup("Host:xxx.com");
    ....// Set other parameters.
    // Configure the settings for the player.
    mPlayerPtr->setConfig(pConfig);
    ```

18. Set snapshot capture.

    ApsaraVideo Player SDK supports snapshot capture for the current video image. The player saves the captured image in the ARGB32 format. You can obtain the information about the captured image after the onSnapshotImageBuffer callback is fired. Sample code:

    ```
    // Take a snapshot of the current video image.
    mPlayerPtr->snapshot();
    // Fire a callback for snapshot capture.
    void AlivcLivePlayerMainDlg::onSnapshotImageBuffer(AliPlayer *player, int width, int height, unsigned char *pARGBBuffer)
    {
        QString savePath = "save path";
        QImage snapshot(pARGBBuffer, width, height, QImage::Format_ARGB32);
        snapshot.save(savePath);
    }
    ```

    **Note:** The snapshot is a video image that does not contain the UI.

19. Configure the play-and-cache feature.

    ApsaraVideo Player SDK allows you to cache videos during playback. This saves your traffic during loop playback. To enable this feature, use the AVPCacheConfig class before the prepare method is called. To play an encrypted video, configure a security file for encryption verification. For more information, see "1. Create a player" in this section.Create a player. Sample code:

    ```
    AVPCacheConfig mCacheConfig;
    // Enable the play-and-cache feature.
    mCacheConfig.enable = true;
    // Specify the maximum length of a single cached file. Files whose length exceeds the maximum limit are not cached.
    mCacheConfig.maxDuration = 100;
    // Specify the maximum size of the cache directory. When the total size of cached files in the cache directory exceeds the maximum limit, the earliest cached files are overwritten.
    mCacheConfig.maxSizeMB = 200;
    // Specify the cache directory. Specify it as required by your application.
    mCacheConfig.path = strdup("please use your cache path here");
    // Configure the cache settings for the player.
    mPlayerPtr->setCacheConfig(&mCacheConfig);
    ```

    You must call the setCacheConfig method to use cached files. Cached files are used in the following scenarios:

    -   If you enable the loop playback feature, the player automatically plays a video all over again by using the cached video file each time the playback is complete.
    -   After you cache a video and create a player to play the video, the new player plays the video by using the cached video file.

        **Note:** The player uses information such as the video ID from online requests to find cached files for video ID-based playback.

    The player does not cache videos during playback in the following scenarios:

    -   When the player plays AVPUrlSource streams by using the HLS protocol based on the URL in an M3U8 playlist, the player does not cache the video during the playback. For other supported formats, the player caches videos during playback as configured.
    -   When the player plays a video based on the video ID, the player caches the video during the playback as configured.
    -   A video is cached when the player reads all video data. Caching may fail if the stop method is called or the onError callback is fired before all the data is read.
    -   Seeking to a position inside the cached video does not affect the caching result. Seeking to a position outside the cached video may cause a caching failure.
    -   If the security file does not match the application information, the video caching may fail.
    -   You can check whether the caching result is EVENT\_PLAYER\_CACHE\_SUCCESS or EVENT\_PLAYER\_CACHE\_ERROR after the onPlayerEvent callback is fired.
20. Set preview.

    After you specify the preview duration, ApsaraVideo Player SDK allows you to preview a video for the specified duration instead of the whole video. You can use ApsaraVideo VOD to enable the preview feature. This feature supports VidSts and VidAuth sources. For more information about how to configure and use the preview feature, see [Configure the preview feature for VOD resources](/intl.en-US/Best Practice/Configure the preview feature for VOD resources.md). After you enable the preview feature, you can call the setPreviewTime method in the VidPlayerConfigGenerator class to specify the preview duration. In this example, AVPVidStsSource is used. Sample code:

    ```
    VidPlayerConfigGenerator playConfigGen;
    playConfigGen.setPreviewTime(10);
    AVPVidStsSource vidSource;
    vidSource.initWithVid(Video ID,
                            "accessKeyId",
                            "accessKeySecret",
                            "Security token",
                            "Access region",
                            playConfigGen.generatePlayerConfig());
    mPlayerPtr->setSource(vidSource);
    ```


## Video download

ApsaraVideo Player SDK allows you to download videos from ApsaraVideo VOD. You can download videos of VidSts and VidAuth sources from ApsaraVideo VOD. ApsaraVideo VOD supports two download modes: secure download and normal download. You can set the download mode in the console.

-   When you select the normal download mode, downloaded videos are not encrypted by Alibaba Cloud, even though the videos have been encrypted by ApsaraVideo VOD. In this case, you can use third-party players to play the downloaded videos.
-   When you select the secure download mode, downloaded videos are encrypted by Alibaba Cloud, even though the videos have not been encrypted by ApsaraVideo VOD. In this case, you cannot use third-party players to play the downloaded videos. You must use ApsaraVideo Player to play the downloaded videos.

To use ApsaraVideo Player SDK for Windows to download a video, perform the following steps:

1.  Create a download object. Sample code:

    ```
    mMediaDownloader = AliMediaDownloader::CreateMediaDownloader();
    mMediaDownloader->setListener(new AVDListenerImpl);
    mMediaDownloader->setSaveDirectory("saveDir");
    ```

    ApsaraVideo Player SDK allows you to download videos that are encrypted by proprietary cryptography. To ensure security, configure a security file encryptedApp.dat for encryption verification. Sample code:

    ```
    InitPrivateService(fileContentBuffer, fileLength);
    ```

2.  Prepare the download source.

    Call the prepare method to prepare the download source. The following two download sources are supported:

    -   AVPVidStsSource
    -   AVPVidAuthSource
    In this example, AVPVidStsSource is used. Sample code:

    ```
    AVPVidStsSource vidSource;
    vidSource.initWithVid(Video ID,
                            "accessKeyId",
                            "accessKeySecret",
                            "Security token",
                            "Access region",
                            nullptr);
    mMediaDownloader->prepareWithVid(&vidSource);
    ```

3.  Select a track for download after the preparation.

    After the preparation, the onPrepared callback is fired. Select a track for download. Sample code:

    ```
    void YourClass::onPrepared(AliMediaDownloader *downloader, AVPMediaInfo *mediaInfo) {
        AVPTrackInfo *track = mediaInfo->tracks[0];
        mMediaDownloader->selectTrack(track->trackIndex);
    }
    ```

4.  Update the download source and start the download.

    After the preceding steps, start the download. We recommend that you update the download source information to ensure that the VidSts or VidAuth source is valid. Sample code:

    ```
    mMediaDownloader->updateWithVid(&vidSource);
    mMediaDownloader->start();
    ```

5.  Release the download object after the download succeeds or fails.

    After the download succeeds, release the download object. Sample code:

    ```
    delete mMediaDownloader;
    mMediaDownloader = nullptr;
    ```


