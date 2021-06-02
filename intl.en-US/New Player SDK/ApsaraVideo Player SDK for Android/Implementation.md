# Implementation

This topic shows you how to implement various features of ApsaraVideo Player SDK for Android. This topic also provides sample code so that you can implement the features with ease.

## Playback

1.  Create a player.

    You can create the following player objects by calling the AliPlayerFactory class:

    -   AliPlayer
    -   AliListPlayer
    To play a single video, create an AliPlayer object. Sample code:

    ```
    AliPlayer aliyunVodPlayer;
    .....
    aliyunVodPlayer = AliPlayerFactory.createAliPlayer(getApplicationContext());
    ```

    To play an on-premises video that is downloaded by using the secure download feature of ApsaraVideo Player SDK for Android, you must configure a security file for encryption verification. We recommend that you configure the security file in your application, once for all. Example:

    ```
    PrivateService.initService(getApplicationContext(), "The path of the encryptedApp.dat file");
    ```

    For more information about how to create a security file for encryption verification, see [How can I obtain a security file?](/intl.en-US/FAQ/Player/How can I obtain a security file?.md).

    **Note:** If you do not configure a correct security file for encryption verification, the ERROR\_DEMUXER\_OPENSTREAM error message appears when you play a video that is downloaded in secure download mode.

2.  Set player listeners.

    ApsaraVideo Player SDK for Android provides a variety of listeners, such as onPrepared and onCompletion. Sample code:

    ```
    aliyunVodPlayer.setOnCompletionListener(new IPlayer.OnCompletionListener() {
        @Override
        public void onCompletion() {
            // The listener for the completion of playback.
        }
    });
    aliyunVodPlayer.setOnErrorListener(new IPlayer.OnErrorListener() {
        @Override
        public void onError(ErrorInfo errorInfo) {
            // The listener for the occurrence of errors.
        }
    });
    aliyunVodPlayer.setOnPreparedListener(new IPlayer.OnPreparedListener() {
        @Override
        public void onPrepared() {
            // The listener for successful preparation.
        }
    });
    aliyunVodPlayer.setOnVideoSizeChangedListener(new IPlayer.OnVideoSizeChangedListener() {
        @Override
        public void onVideoSizeChanged(int width, int height) {
            // The listener for the change of the video resolution.
        }
    });
    aliyunVodPlayer.setOnRenderingStartListener(new IPlayer.OnRenderingStartListener() {
        @Override
        public void onRenderingStart() {
            // The listener for the appearance of the first frame.
        }
    });
    aliyunVodPlayer.setOnInfoListener(new IPlayer.OnInfoListener() {
        @Override
        public void onInfo(int type, long extra) {
            // The listener for other events. The type parameter contains multiple values, indicating various events, such as the start of loop playback, buffer position, current playback position, and the start of autoplay.
        }
    });
    aliyunVodPlayer.setOnLoadingStatusListener(new IPlayer.OnLoadingStatusListener() {
        @Override
        public void onLoadingBegin() {
            // The listener for the start of buffering.
        }
        @Override
        public void onLoadingProgress(int percent, float kbps) {
            // The listener for the buffering progress.
        }
        @Override
        public void onLoadingEnd() {
            // The listener for the completion of buffering.
        }
    });
    aliyunVodPlayer.setOnSeekCompleteListener(new IPlayer.OnSeekCompleteListener() {
        @Override
        public void onSeekComplete() {
            // The listener for the completion of seeking.
        }
    });
    aliyunVodPlayer.setOnSubtitleDisplayListener(new IPlayer.OnSubtitleDisplayListener() {
        @Override
        public void onSubtitleShow(long id, String data) {
            // The listener for the display of subtitles.
        }
        @Override
        public void onSubtitleHide(long id) {
            // The listener for the hiding of subtitles.
        }
    });
    aliyunVodPlayer.setOnTrackChangedListener(new IPlayer.OnTrackChangedListener() {
        @Override
        public void onChangedSuccess(TrackInfo trackInfo) {
            // The listener for the success in switching between audio and video streams or between resolutions.
        }
        @Override
        public void onChangedFail(TrackInfo trackInfo, ErrorInfo errorInfo) {
            // The listener for the failure of switching between audio and video streams or between resolutions.
        }
    });
    aliyunVodPlayer.setOnStateChangedListener(new IPlayer.OnStateChangedListener() {
        @Override
        public void onStateChanged(int newState) {
            // The listener for the change of the player status.
        }
    });
    aliyunVodPlayer.setOnSnapShotListener(new IPlayer.OnSnapShotListener() {
        @Override
        public void onSnapShot(Bitmap bm, int with, int height) {
            // The listener for the capture of snapshots.
        }
    });
    ```

    **Note:** For more information about callback parameters, see [API operations](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Android/API operations.md).

3.  Set a playback source and prepare for playback.

    ApsaraVideo Player SDK for Android supports the following playback sources:

    -   VidSts
    -   VidAuth
    -   VidMps
    -   UrlSource
    **Note:** You can use UrlSource for URL-based playback, and use the other three playback sources for video ID \(VID\)-based playback. VidSts and VidAuth are available for ApsaraVideo VOD users. VidMps is available for ApsaraVideo for Media Processing users only.

    In the following example, VidSts is used.

    ```
    // Create the VidSts download source.
     VidSts aliyunVidSts = new VidSts();
     aliyunVidSts.setVid(Video ID);
     aliyunVidSts.setAccessKeyId(Temporary AccessKey ID);
     aliyunVidSts.setAccessKeySecret(Temporary AccessKey secret);
     aliyunVidSts.setSecurityToken(Security token);
     aliyunVidSts.setRegion(Access region);
     // Set the playback source.
     aliyunVodPlayer.setDataSource(aliyunVidSts);
     ......
     // Prepare for playback.
     aliyunVodPlayer.prepare();
    ```

    **Note:** For more information about the video playback process and concepts in ApsaraVideo for Media Processing, see [Video playback]().

    For more information about the process of using the playback credential for playback, see [Use playback credentials](/intl.en-US/Developer Guide/Video play/Use playback credentials to play videos.md).

    For more information about region settings, see [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md).

4.  Set the user interface \(UI\) view.

    If the playback source contains video images, you must set the UI view to display the video images in the player. You can use SurfaceView or TextureView to set the UI view. In the following example, SurfaceView is used.

    ```
    surfaceView = (SurfaceView) findViewById(R.id.playview);
    surfaceView.getHolder().addCallback(new SurfaceHolder.Callback() {
        @Override
        public void surfaceCreated(SurfaceHolder holder) {
            aliyunVodPlayer.setDisplay(holder);
        }
        @Override
        public void surfaceChanged(SurfaceHolder holder, int format, int width, int height) {
            aliyunVodPlayer.redraw();
        }
        @Override
        public void surfaceDestroyed(SurfaceHolder holder) {
            aliyunVodPlayer.setDisplay(null);
        }
    });
    ```

    The `redraw` method is called inside the `surfaceChanged` method to refresh video images. If the size of the UI view changes, you can call the redraw method to refresh the size of video images. This ensures that video images are adaptive to the view size change.

5.  Set playback control.

    You can create playback control buttons and associate click events with playback control methods to implement playback control. The basic control features include play, stop, pause, and seek. The seek feature is valid only for ApsaraVideo VOD. If you pause a live stream, the live stream stops at the current position. After you resume the playback of the live stream, the live stream starts from the paused position. Sample code:

    ```
    // Start the playback.
    aliyunVodPlayer.start();
    // Pause the playback.
    aliyunVodPlayer.pause();
    // Stop the playback.
    aliyunVodPlayer.stop();
    // Seek. This operation may not direct the video to the precise point in time.
    aliyunVodPlayer.seekTo(long position);
    // Reset the player.
    aliyunVodPlayer.reset();
    // Release the player. The player cannot be used after it is released.
    aliyunVodPlayer.release();
    ```

6.  Set multi-bitrate switching.

    ApsaraVideo Player SDK for Android allows you to play an HTTP Live Streaming \(HLS\) stream in different bitrates. After the player is prepared by calling the `prepare` method, you can call the `getMediaInfo` method to obtain the bitrate information, which is indicated by values of the `TrackInfo` parameter. Sample code:

    ```
    List<TrackInfo> trackInfos  = aliyunVodPlayer.getMediaInfo().getTrackInfos();
    ```

    During the playback, you can call the selectTrack method to switch the bitrate. Sample code:

    ```
    int index = trackInfo.getIndex();
    aliyunVodPlayer.selectTrack(index);
    ```

    You can call the `OnTrackChangedListener` callback to view the switching result. You must call the OnTrackChangedListener method before you call the `selectTrack` method. Sample code:

    ```
    aliyunVodPlayer.setOnTrackChangedListener(new IPlayer.OnTrackChangedListener() {
        @Override
        public void onChangedSuccess(TrackInfo trackInfo) {
            // The bitrate switching is successful.
        }
        @Override
        public void onChangedFail(TrackInfo trackInfo, ErrorInfo errorInfo) {
            // The bitrate switching fails. You can call the errorInfo.getMsg() method to find the cause of the failure.
        }
    });
    ```

7.  Set the autoplay feature.

    ApsaraVideo Player SDK for Android supports the autoplay feature. To set the autoplay feature, call the `setAutoPlay` method before you call the `prepare` method. Sample code:

    ```
    aliyunVodPlayer.setAutoPlay(true);
    ```

    After you set the autoplay feature and prepare the player, videos are automatically played. Sample code:

    ```
    -(void)onPlayerEvent:(AliPlayer*)player eventType:(AVPEventType)eventType {
        switch (eventType) {
            case AVPEventPrepareDone: {
                break;
            case AVPEventAutoPlayStart:
                break;
        }
    }
    ```

    **Note:** When autoplay starts, the `onInfo` callback instead of the `onPrepared` callback is fired.

8.  Set the loop playback feature.

    ApsaraVideo Player SDK for Android supports the loop playback feature. To set the loop playback feature, call the `setLoop` method. The loop playback feature allows the player to play a video again when the player plays the video to the end position. Sample code:

    ```
    aliyunVodPlayer.setLoop(true);
    ```

    The callback for the start of loop playback is fired by the `onInfo` callback. Sample code:

    ```
    aliyunVodPlayer.setOnInfoListener(new IPlayer.OnInfoListener() {
        @Override
        public void onInfo(InfoBean infoBean) {
            if (infoBean.getCode() == InfoCode.LoopingStart){
                // The listener for the start of loop playback.
            }
        }
    });
    ```

9.  Set video image rotation, scaling, and mirroring.

    ApsaraVideo Player SDK for Android provides multiple methods for you to precisely control video images. You can set the rotation angle, scaling mode, and mirroring mode for video images. Sample code:

    ```
    // Set the mirroring mode for video images to horizontal mirroring, vertical mirroring, or no mirroring.
    aliyunVodPlayer.setMirrorMode(MirrorMode.MIRROR_MODE_NONE);
    // Set the rotation angle for video images to 0°, 90°, 180°, or 270°.
    aliyunVodPlayer.setRotateMode(RotateMode.ROTATE_0);
    // Set the scaling mode for video images to padding by keeping the original aspect ratio, fitting by keeping the original aspect ratio, or stretching.
    aliyunVodPlayer.setScaleMode(ScaleMode.SCALE_ASPECT_FIT);
    ```

    The following table describes the supported rotation angles for video images.

    |Value|Description|
    |-----|-----------|
    |ROTATE\_0|Indicates that the rotation angle is 0°, in the clockwise direction.|
    |ROTATE\_90|Indicates that the rotation angle is 90°, in the clockwise direction.|
    |ROTATE\_180|Indicates that the rotation angle is 180°, in the clockwise direction.|
    |ROTATE\_270|Indicates that the rotation angle is 270°, in the clockwise direction.|

    The following table describes the supported scaling modes for video images.

    |Value|Description|
    |-----|-----------|
    |SCALE\_ASPECT\_FIT|Indicates that the video image is scaled down into the UI view without changing the aspect ratio. This prevents image distortion.|
    |SCALE\_ASPECT\_FILL|Indicates that the video image is scaled up to fill the UI view without changing the aspect ratio. This prevents image distortion.|
    |SCALE\_TO\_FILL|Indicates that the video image is stretched to fill the UI view. This may cause image distortion if the video image and the UI view do not match in the aspect ratio.|

    The following table describes the supported mirroring modes for video images.

    |Value|Description|
    |-----|-----------|
    |MIRROR\_MODE\_NONE|Indicates no mirroring.|
    |MIRROR\_MODE\_HORIZONTAL|Indicates horizontal mirroring.|
    |MIRROR\_MODE\_VERTICAL|Indicates vertical mirroring.|

10. Set the mute mode and volume control.

    ApsaraVideo Player SDK for Android allows you to control video volumes. You can call the `setMute` method to set the mute mode for the player. In addition, you can call the `setVolume` method to set the player volume in the range of \[0, 1\].**** Sample code:

    ```
    // Mute the player.
    aliyunVodPlayer.setMute(true);
    // Set the player volume. Value range: 0 to 1.
    aliyunVodPlayer.setVolume(1f);
    ```

11. Set the playback speed.

    ApsaraVideo Player SDK for Android allows you to set the playback speed. You can call the `setSpeed` method to change the playback speed from 0.5x to 2x. The audio pitch remains unchanged at different speeds. Sample code:

    ```
    // Set the playback speed. You can change the playback speed from 0.5x to 2x.
    aliyunVodPlayer.setSpeed(1.0f);
    ```

12. Set the snapshot feature.

    ApsaraVideo Player SDK for Android provides the snapshot feature, which can be used to capture video snapshots.`` When you capture a snapshot, the player saves the source data of the video image to be captured and converts the source data to a bitmap.`` Then, you can call the `OnSnapShotListener` method to obtain the bitmap. Sample code:

    ```
    // Set the callback for snapshot capture.
    aliyunVodPlayer.setOnSnapShotListener(new OnSnapShotListener(){
        @Override
        public void onSnapShot(Bitmap bm, int with, int height){
            // Obtain the bitmap and the width and height of the video image.
        }
    });
    // Capture a snapshot of the current video image.
    aliyunVodPlayer.snapshot();
    ```

13. Set the play-and-cache feature.

    ApsaraVideo Player SDK for Android supports the play-and-cache feature. This feature saves your data traffic during loop playback. To set the play-and-cache feature, call the `CacheConfig` method before you call the `prepare` method. Sample code:

    ```
    CacheConfig cacheConfig = new CacheConfig();
    // Enable the play-and-cache feature.
    cacheConfig.mEnable = true;
     // Specify the maximum length of a single cached file. If a file exceeds the maximum length, it is not cached.
    cacheConfig.mMaxDurationS =100;
    // Specify the cache directory.
    cacheConfig.mDir = "The directory of the cached file";
     // Specify the maximum size of the cache directory. If the size of the cache directory exceeds the maximum value, the earliest cached file is deleted.
    cacheConfig.mMaxSizeMB = 200;
    // Specify the cache settings for the player.
    mAliyunVodPlayer.setCacheConfig(cacheConfig);
    ```

    You can use cached files only after you call the `setCacheConfig` method. After a video is cached, the cached files are used in the following scenarios:

    -   If the loop playback feature is enabled by calling the `setLoop(true)` method, the cached files are used when the player replays the video.
    -   The cached files are used when you create another player to play the same video.

        **Note:** For VID-based playback, information such as the VID is required to locate cached files. An online request must be sent to obtain the required information that determines which cached files are needed for VID-based playback.

    The following table describes the methods that can be used to query the path of a cached file.

    |Method|Description|Parameter|Return value|
    |------|-----------|---------|------------|
    |public String getCacheFilePath\(String URL\)|Queries the path of a cached file based on the video URL. To obtain the path, make sure that you have called the setCacheConfig method.|URL|The absolute path of the cached file.|
    |public String getCacheFilePath\(String vid, String format, String definition, int previewTime\)|Queries the path of a cached file based on the VID. To obtain the path, make sure that you have called the setCacheConfig method.|    -   vid: the video ID.
    -   format: the video format.
    -   definition: the video resolution.
    -   previewTime: the preview duration.
|The absolute path of the cached file.|

    The play-and-cache feature does not mean that all videos are cached during playback. In some scenarios, videos are not cached. Sample code:

    -   When the UrlSource playback source is used for URL-based playback,`` the video is not cached if the player uses the HLS protocol to play the video based on the video URL in the .m3u8 file. For other supported formats of URL-based playback, the player caches a video during playback as configured.
    -   When the player plays a video based on the VID, the player caches the video during playback as configured.
    -   A video is cached when the player reads all video data. Caching fails if the `stop` or `onError` method is called before the player reads all video data.
    -   Seeking inside the cached part of a video does not affect the caching result. Seeking outside the cached part causes a caching failure.
    -   An encrypted video cannot be cached if the verification information in the security file for encryption verification does not match the application information.
    -   The `onInfo` callback returns the caching result.
    ```
    -(void)onPlayerEvent:(AliPlayer*)player eventWithString:(AVPEventWithString)eventWithString description:(NSString *)description {
        if (eventWithString == EVENT_PLAYER_CACHE_SUCCESS) {
            // Indicate that the caching succeeds.
        }else if (eventWithString == EVENT_PLAYER_CACHE_ERROR) {
            // Indicate that the caching fails.
        }
    }
    ```

14. Set the preview feature.

    After you set the preview duration, the server returns the preview video instead of the whole video when you use ApsaraVideo Player SDK for Android to play the video.

    You can use the preview feature by using ApsaraVideo Player SDK for Android with ApsaraVideo VOD. The playback sources that support the preview feature are VidSts and VidAuth. For more information about how to set and use the preview feature, see [Configure the preview feature for VOD resources](/intl.en-US/Best Practice/Configure the preview feature for VOD resources.md). After you enable the preview feature, you can call the `setPreviewTime()` method in VidPlayerConfigGen to set the preview duration. In the following example, VidSts is used.

    ```
    VidSts vidSts = new VidSts;
    ....
    VidPlayerConfigGen configGen = new VidPlayerConfigGen();
    configGen.setPreviewTime(20); // Set the preview duration to 20s.
    vidSts.setPlayConfig(configGen); // Specify the settings for the player.
    ...
    ```

    **Note:**

    -   You can call the VidPlayerConfigGen method to set the request parameters that are supported by the server. For more information, see [t1235674.md\#](/intl.en-US/API Reference/Appendix/Request parameters.md).
    -   The preview feature is not supported for Flash Video \(FLV\) and MP3 files.
15. Enable or disable hardware decoding.

    ApsaraVideo Player SDK for Android supports hardware decoding based on the H.264 and H.265 standards. You can call the `enableHardwareDecoder` method to enable or disable the hardware decoding feature. By default, the hardware decoding feature is enabled. If hardware decoding fails to be initialized, the player switches to software decoding to ensure normal video playback. Sample code:

    ```
    // Enable hardware decoding. By default, hardware decoding is enabled.
    mAliyunVodPlayer.enableHardwareDecoder(true);
    ```

    When hardware decoding is switched to software decoding, a callback is fired by the `onInfo` method. Sample code:

    ```
    mApsaraPlayerActivity.setOnInfoListener(new IPlayer.OnInfoListener() {
        @Override
        public void onInfo(InfoBean infoBean) {
            if (infoBean.getCode() == InfoCode.SwitchToSoftwareVideoDecoder) {
                // Switch to software decoding.
            }
        }
    });
    ```

16. Set a blacklist.

    ApsaraVideo Player SDK for Android allows you to set a blacklist for hardware decoding. If hardware decoding is not allowed for a device, you can use software decoding to avoid decoding failures. Sample code:

    ```
    DeviceInfo deviceInfo = new DeviceInfo();
    deviceInfo.model="Lenovo K320t";
    AliPlayerFactory.addBlackDevice(BlackType.HW_Decode_H264 ,deviceInfo );
    ```

    The blacklist becomes invalid after the application exits.

17. Set the referer.

    ApsaraVideo Player SDK for Android provides the `PlayerConfig` class for you to set the request referer. You can implement access control by setting referers in the blacklist or whitelist in the ApsaraVideo VOD console. Sample code:

    ```
    // Query the configuration.
    PlayerConfig config = mAliyunVodPlayer.getConfig();
    // Set the referer.
    config.mReferrer = referrer;
    ....// Set other parameters.
      // Specify the settings for the player.
    mAliyunVodPlayer.setConfig(config);
    ```

18. Set the UserAgent.

    ApsaraVideo Player SDK for Android provides the `PlayerConfig` class for you to set the request UserAgent. After you set the UserAgent, the UserAgent information is contained in the requests from the player. Sample code:

    ```
    // Query the configuration.
    PlayerConfig config = mAliyunVodPlayer.getConfig();
    // Set the UserAgent.
    config.mUserAgent = "Required UserAgent";
    ....// Set other parameters.
      // Specify the settings for the player.
    mAliyunVodPlayer.setConfig(config);
    ```

19. Set the network timeout period and the number of retries.

    You can use the `PlayerConfig` class to set the network timeout period and the number of retries for the player. Sample code:

    ```
    // Query the configuration.
    PlayerConfig config = mAliyunVodPlayer.getConfig();
    // Specify the network timeout period, in milliseconds.
    config.mNetworkTimeout = 5000;
    // Set the number of retries when a timeout occurs. The networkTimeout parameter indicates the retry interval. By default, the networkRetryCount parameter is set to 2. If the networkRetryCount parameter is set to 0, retry is prohibited. The application determines the retry policy.
    config.mNetworkRetryCount=2;
    ....// Set other parameters.
      // Specify the settings for the player.
    mAliyunVodPlayer.setConfig(config);
    ```

    **Note:**

    -   If you set the networkRetryCount parameter to a value other than 0, the player retries the playback when it enters the loading status due to network errors. The number of retries is the value of the networkRetryCount parameter and the retry interval is the value of the mNetworkTimeout parameter.
    -   If the loading status persists after the maximum number of retries is reached, the `onError` callback is fired. In this case, the ErrorInfo.getCode\(\) method returns ErrorCode.ERROR\_LOADING\_TIMEOUT.
    -   If the networkRetryCount parameter is set to 0, the `onInfo` callback is fired when a network timeout occurs. In this case, the InfoBean.getCode\(\) method returns InfoCode.NetworkRetry.**** To resolve the issue, you can call the `reload` method of ApsaraVideo Player SDK for Android to reload network packets or perform other operations as required. The application can process the relevant logic.
20. Configure buffer and delay settings.

    ApsaraVideo Player SDK for Android provides the `PlayerConfig` class for you to configure buffer and delay settings. Sample code:

    ```
    // Query the configuration.
    PlayerConfig config = mAliyunVodPlayer.getConfig();
    // Set the maximum buffer delay. Note: This parameter is valid only for live streaming. If the delay time exceeds the maximum limit, ApsaraVideo Player SDK for Android synchronizes frames to keep the delay under the maximum delay time.
    config.mMaxDelayTime = 5000;
    // Set the maximum buffer duration. Unit: milliseconds. This parameter indicates the maximum video length that can be loaded by the player.
    config.mMaxBufferDuration = 50000;
    // Set the peak buffer duration. Unit: milliseconds. The player starts loading data when the network connection is poor. This parameter indicates the buffer duration beyond which the player stops loading.
    config.mHighBufferDuration = 3000;
    // Set the startup loading time. Unit: milliseconds. The shorter the startup loading time, the sooner the playback starts. A short startup loading time may cause the player to buffer soon after the playback starts.
    config.mStartBufferDuration = 500;
    ....// Set other parameters.
    // Specify the settings for the player.
    mAliyunVodPlayer.setConfig(config);
    ```

    **Note:** Make sure that the value of the mStartBufferDuration parameter is not greater than that of the mHighBufferDuration parameter, and that the value of the mHighBufferDuration parameter is not greater than that of the mMaxBufferDuration parameter.

21. Set HTTP headers.

    ApsaraVideo Player SDK for Android provides the `PlayerConfig` class for you to add HTTP headers to requests. Sample code:

    ```
    // Query the configuration.
    PlayerConfig config = mAliyunVodPlayer.getConfig();
    // Define a header.
    String[] headers = new String[1];
    headers[0]="Hos t:xxx.com";// For example, add the host information to the header.
    // Set the header.
    config.setCustomHeaders(headers);
    ....// Set other parameters.
      // Specify the settings for the player.
    mAliyunVodPlayer.setConfig(config);
    ```


## List playback

Nowadays, list playback for short video content is prevalent. ApsaraVideo Player SDK for Android provides the complete list playback feature with the built-in preloading mechanism. The list playback feature significantly reduces the startup loading time.

1.  Create a player.

    Use the AliPlayerFactory class to create a player. You can create the following player objects:

    -   AliPlayer
    -   AliListPlayer
    AliListPlayer and AliPlayer provide the same features, except that AliListPlayer provides the list playback feature.```` To use the list playback feature, create an AliListPlayer object.`` Sample code:

    ```
    AliListPlayer aliyunListPlayer;
    .....
    aliyunListPlayer = AliPlayerFactory.createAliListPlayer(getApplicationContext());
    ```

2.  Set the count of videos to be preloaded.

    You can significantly reduce the startup loading time by appropriately setting the count of videos to be preloaded. Sample code:

    ```
    // Set the count of videos to be preloaded. The total number of loaded videos equals 1 plus twice the count.
    aliyunListPlayer.setPreloadCount(int count);
    ```

3.  Add or remove multiple playback sources.

    List playback supports the VidSts and UrlSource playback sources. You can use UrlSource for URL-based playback, and use VidSts for VID-based playback. Sample code:

    ```
    // Add a VidSts playback source.
    aliyunListPlayer.addVid(String videoId, String uid);
    // Add a UrlSource playback source.
    aliyunListPlayer.addUrl(String url, String uid);
    // Remove a playback source.
    aliyunListPlayer.removeSource(String uid);
    ```

    **Note:**

    -   VidAuth and VidMps are not supported for list playback.
    -   The uid parameter indicates the unique ID of a video. It is used to differentiate videos. Videos with the same unique ID are considered the same. If the player plays a video that is not the one you specified, check whether you specify a unique ID for multiple videos. You can set the uid parameter to a string.
4.  Play a playback source.

    After you add one or more playback sources, call the `moveTo` method to play the content from the specified playback source. Sample code:

    ```
    // Call the following method for URL-based playback.
    aliyunVodPlayer.moveTo(String uid);
    // Call the following method for VID-based playback. You must specify the Security Token Service (STS) token for the stsInfo parameter. Make sure that the STS token is valid.
    aliyunVodPlayer.moveTo(String uid, StsInfo info);
    ```

5.  Play the previous or next video in the list.

    You can call the `moveToPrev` method to play the previous video or call the `moveToNext` method to play the next video. Sample code:

    ```
    // Play the next video. Note: This method is valid only for URL-based playback. The method is invalid for VID-based playback.
    aliyunVodPlayer.moveToNext();
    // Play the previous video. Note: This method is valid only for URL-based playback. The method is invalid for VID-based playback.
    aliyunVodPlayer.moveToPrev();
    // Play the next video. Note: This method is valid only for VID-based playback.
    aliyunVodPlayer.moveToNext(StsInfo info);
    // Play the previous video. Note: This method is valid only for VID-based playback.
    aliyunVodPlayer.moveToPrev(StsInfo info);
    ```


## Video download

ApsaraVideo Player SDK for Android allows you to download videos from ApsaraVideo VOD by using VidSts and VidAuth. ApsaraVideo VOD supports the secure download mode and the normal download mode. You can set a download mode in the ApsaraVideo VOD console.

-   Normal download

    Videos that are downloaded in normal download mode are not encrypted by Alibaba Cloud and can be played by third-party players.

-   Secure download

    Videos that are downloaded in secure download mode are encrypted by Alibaba Cloud. You cannot use third-party players to play the downloaded videos. You can use only ApsaraVideo Player to play them.


1.  Create and set a downloader.

    You can use the `AliDownloaderFactory` class to create a downloader. Sample code:

    ```
    AliMediaDownloader mAliDownloader = null;
    ......
    // Create a downloader.
    mAliDownloader = AliDownloaderFactory.create(getApplicationContext());
    // Specify a path to save downloaded files.
    mAliDownloader.setSaveDir("The path of the folder for storing downloaded files");
    ```

    ApsaraVideo Player SDK for Android allows you to download videos that are encrypted by using Alibaba Cloud proprietary cryptography. For security reasons, you must configure a security file for encryption verification in the SDK.We recommend that you configure the security file in your application, once for all. Sample code:

    ```
    PrivateService.initService(getApplicationContext(), "The path of the encryptedApp.dat file");
    ```

    **Note:** If you download a video in secure download mode and the information in the security file for encryption verification does not match the application information, the video download fails.

2.  Set listeners.

    The downloader provides multiple listeners. Sample code:

    ```
    mAliDownloader.setOnPreparedListener(new AliMediaDownloader.OnPreparedListener() {
       @Override
       public void onPrepared(MediaInfo mediaInfo) {
           // Indicate that the content to be downloaded is prepared.
       }
    });
    mAliDownloader.setOnProgressListener(new AliMediaDownloader.OnProgressListener() {
       @Override
       public void onDownloadingProgress(int percent) {
           // Indicate the percentage of the download progress.
       }
       @Override
       public void onProcessingProgress(int percent) {
           // Indicate the percentage of the processing progress.
       }
    });
    mAliDownloader.setOnErrorListener(new AliMediaDownloader.OnErrorListener() {
       @Override
       public void onError(ErrorInfo errorInfo) {
           // Indicate that a download error occurs.
       }
    });
    mAliDownloader.setOnCompletionListener(new AliMediaDownloader.OnCompletionListener() {
       @Override
       public void onCompletion() {
           // Indicate that the download succeeds.
       }
    });
    ```

3.  Prepare a download source.

    You can call the `prepare` method to prepare a download source. VidSts and VidAuth are supported as download sources. In the following example, VidSts is used.

    ```
    // Create the VidSts download source.
    VidSts aliyunVidSts = new VidSts();
    aliyunVidSts.setVid(Video ID);
    aliyunVidSts.setAccessKeyId(Temporary AccessKey ID);
    aliyunVidSts.setAccessKeySecret(Temporary AccessKey secret);
    aliyunVidSts.setSecurityToken(Security token);
    aliyunVidSts.setRegion(Access region);
    // Prepare the download source.
    mAliDownloader.prepare(aliyunVidSts)
    ```

4.  Select the content to be downloaded from the prepared download source.

    After the download source is prepared, the `OnPreparedListener` callback is fired. Select a track to be downloaded. Sample code:

    ```
    public void onPrepared(MediaInfo mediaInfo) {
        // Indicate that the content to be downloaded is prepared.
        List<TrackInfo> trackInfos = mediaInfo.getTrackInfos();
        // In this example, download the content of the first track.
        mAliDownloader.selectItem(trackInfos.get(0).getIndex());
    }
    ```

5.  Update the download source and start the download.

    VidSts or VidAuth may expire before the download. Therefore, we recommend that you update the download source before you start the download. Sample code:

    ```
    // Update the download source.
    mAliDownloader.updateSource(mVidSts);
    // Start the download.
    mAliDownloader.start();
    ```

6.  Release the download object after the download succeeds or fails.

    After the download succeeds, call the `release` method to release the downloader. You can release the downloader when the `onCompletion` or `onError` callback is fired. Sample code:

    ```
    mAliDownloader.stop();
    mAliDownloader.release();
    ```

7.  Delete a downloaded file.

    You can delete a downloaded file during the download or after the download is complete. Sample code:

    ```
    // Delete the file by using the downloader.
    mAliDownloader.deleteFile();
    // Delete the file by using the static method.
    AliDownloaderFactory.deleteFile("The directory of the downloaded file",vid, format,index);
    ```


## Playback of encrypted live streams

ApsaraVideo Player SDK for Android supports the playback of encrypted live streams. For more information about how to create and use a player, see the [Playback](#section_t2w_s5v_3xp) section of this topic.

1.  Set a playback source.

    You must specify AVPLiveStsSource as the playback source. Sample code:

    ```
    // Create the AVPLiveStsSource playback source.
     LiveSts liveSts = new LiveSts();
     liveSts.setUrl("The URL of the encrypted live stream");
     liveSts.setAccessKeyId("The temporary AccessKey ID");
     liveSts.setAccessKeySecret("The temporary AccessKey secret");
     liveSts.setSecurityToken("The security token");
     liveSts.setDomain("The name of the streaming domain");
     liveSts.setApp("The name of the application to which the live stream belongs");
     liveSts.setStream("The name of the live stream");
     // Set the playback source.
     aliyunVodPlayer.setDataSource(liveSts);
     ......
     // Prepare for playback.
     aliyunVodPlayer.prepare();
    ```

2.  Monitor whether the STS token is valid.

    The encryption key may change during the playback of encrypted live streams. When the key is changed, the player requests the latest key from STS. You must monitor whether the STS token is valid. If the token is invalid, the playback of encrypted live streams is affected. Sample code:

    ```
    mAliyunVodPlayer.setOnVerifyStsCallback(new IPlayer.OnVerifyStsCallback() {
        @Override
        public IPlayer.StsStatus onVerifySts(StsInfo info) {
            if (info can be used) {
                return IPlayer.StsStatus.Valid;
            }
    
            if(A valid STS token can be obtained){
                Obtain STS();// This operation can be synchronously or asynchronously performed.
                return IPlayer.StsStatus.Pending;
            }
            // If info is invalid and the latest STS token cannot be obtained, we recommend that you stop the playback to prevent screen flickers.
            mAliyunVodPlayer.stop();
            return IPlayer.StsStatus.Invalid;
        }
    });
    ```

    After you obtain a valid STS token, you must call the `updateStsInfo` method to update the STS token. If you fail to obtain the token, we recommend that you stop the playback.

    ```
    mAliyunVodPlayer.updateStsInfo(stsInfo);
    ```

    **Note:** If you do not call the updateStsInfo method, the player uses the expired STS token to obtain the encryption key. If the STS token becomes invalid, screen flickers may occur or the playback may fail.


