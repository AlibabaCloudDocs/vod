# Implementation

This topic describes how to implement various features of ApsaraVideo Player SDK for Flutter. This topic also provides sample code so that you can implement the features with ease.

## Playback

This section describes how to use ApsaraVideo Player SDK for Flutter to play videos.

1.  Create a player.

    You can use the `FlutterAliPlayerFactory` class to create two player objects: `FlutterAliplayer` and `FlutterAliListPlayer`. Sample code:

    ```
    FlutterAliplayer fAliplayer;
    fAliplayer = FlutterAliPlayerFactory().createAliPlayer();
    ```

    To play an on-premises video that is downloaded by using the secure download feature of ApsaraVideo Player SDK for Flutter, you must configure a security file for encryption verification.

    ```
    var bytes = await rootBundle.load("The path of the encryptedApp.dat file");
    FlutterAliPlayerFactory().initService(bytes.buffer.asUint8List());
    ```

2.  Set listeners.

    ApsaraVideo Player SDK for Flutter provides a variety of listeners, such as `onPrepared` and `onCompletion`. Sample code:

    ```
    fAliplayer.setOnCompletion(() {
        // The listener for the completion of playback.
    });
    
    fAliplayer.setOnError((errorCode, errorExtra, errorMsg) {
        // The listener for the occurrence of errors.
    });
    
    fAliplayer.setOnPrepared(() {
        // The listener for the completion of preparation.
    });
    
    fAliplayer.setOnVideoSizeChanged((width, height) {
        // The listener for the change of the video resolution.
    });
    
    fAliplayer.setOnRenderingStart(() {
        // The listener for the appearance of the first frame.
    });
    
    fAliplayer.setOnInfo((infoCode, extraValue, extraMsg) {
        // The listener for other events, such as the start of loop playback, buffer position, current playback position, and the start of autoplay.
    });
    
    fAliplayer.setOnLoadingStatusListener(
        loadingBegin: () {
            // The listener for the start of buffering.
        },
        loadingProgress: (percent, netSpeed) {
            // The listener for the buffering progress.
        },
        loadingEnd: () {
            // The listener for the completion of buffering.
        });
    });
    
    fAliplayer.setOnSubtitleHide((trackIndex, subtitleID) {
        // The listener for the hiding of subtitles.
    });
    
    fAliplayer.setOnSubtitleShow((trackIndex, subtitleID, subtitle) {
        // The listener for the display of subtitles.
    });
    
    fAliplayer.setOnTrackChanged((value) {
        // The listener for the switching between audio and video streams or between resolutions.
    });
    
    fAliplayer.setOnStateChanged((newState) {
        // The listener for the change of the player status.
    });
    
    fAliplayer.setOnSnapShot((path) {
        // The listener for the capture of snapshots.
    });
    ```

3.  Set the playback source.

    ApsaraVideo Player SDK for Flutter supports the following playback sources:

    -   VidSts
    -   VidAuth
    -   VidMps
    -   UrlSource
    **Note:** You can use UrlSource for URL-based playback, and use the other three playback sources for video ID-based playback. VidSts and VidAuth can be used by ApsaraVideo VOD users. VidMps can be used by ApsaraVideo for Media Processing users only.

    In this example, VidSts is used. Sample code:

    ```
    // Set the playback source.
    fAliplayer.setVidSts(vid:Video ID,region:Access region,accessKeyId:Temporary AccessKey ID,accessKeySecret:Temporary AccessKey secret,securityToken:Security token);
    // Prepare for playback.
    fAliplayer.prepare();
    ```

4.  Set the user interface \(UI\) view.

    In Flutter, the native UI view is used. You can use the `AliPlayerView` class to create a UI view. Sample code:

    ```
    // x and y are coordinate points in the UI view.
    AliPlayerView aliPlayerView = AliPlayerView(
            onCreated: onViewPlayerCreated,
            x: x,
            y: y,
            width: width,
            height: height);
    ```

    **Note:** After a UI view is created, the UI view is automatically set for ApsaraVideo Player SDK for Flutter based on the callback.

5.  Set playback control.

    You can create playback control buttons and associate click events with playback control methods to implement playback control. The basic control features include play, stop, pause, and seek. The seek feature is valid only for ApsaraVideo VOD. If you pause a live stream, the playback stops at the current position. After you resume the live stream, the playback starts from the paused position. Sample code:

    ```
    // Start the playback.
    fAliplayer.play();
    // Pause the playback.
    fAliplayer.pause();
    // Stop the playback.
    fAliplayer.stop();
    // Seek to a position. This operation may not navigate you to the video image at the precise point in time. FlutterAvpdef.ACCURATE indicates the precise seek mode. FlutterAvpdef.INACCURATE indicates the imprecise seek mode.
    fAliplayer.seekTo(int position, int seekMode);
    // Release the player. The player cannot be used after it is released.
    fAliplayer.destroy();
    ```

6.  Set multi-bitrate switching.

    ApsaraVideo Player SDK for Flutter allows you to play videos in different bitrates by using the HTTP Live Streaming \(HLS\) protocol. After the player is prepared, you can call the getMediaInfo method to obtain the value of the TrackInfo parameter. The TrackInfo parameter indicates the bitrate information. Sample code:

    ```
    fAliplayer.getMediaInfo().then((value) {
        val trackInfos = value['tracks'];
    };
    ```

    During the playback, you can call the selectTrack method to switch the bitrate. Sample code:

    ```
    int index = trackInfo.getIndex();
    fAliplayer.selectTrack(index);
    ```

    You can view the switching result after the OnTrackChanged callback is fired. You must set the OnTrackChanged callback before you call the selectTrack method. Sample code:

    ```
    fAliplayer.setOnTrackChanged((value) {
    }
    ```

7.  Set the autoplay feature.

    ApsaraVideo Player SDK for Flutter supports the autoplay feature. To set the autoplay feature, call the setAutoPlay method before you call the prepare method. Sample code:

    ```
    fAliplayer.setAutoPlay(true);
    ```

8.  Set the loop playback feature.

    ApsaraVideo Player SDK for Flutter supports the loop playback feature. To set the loop playback feature, call the setLoop method. The loop playback feature enables the player to play a video all over again each time the playback is complete. Sample code:

    ```
    fAliplayer.setLoop(true);
    ```

    A notification for the start of loop playback is returned after the onInfo callback is fired. Sample code:

    ```
    fAliplayer.setOnInfo((infoCode, extraValue, extraMsg) {
        if (infoCode == FlutterAvpdef.LOOPINGSTART) {
            // The listener for the start of loop playback.
        }
    });
    ```

9.  Set video image rotation, scaling, and mirroring.

    ApsaraVideo Player SDK for Flutter provides multiple methods for you to precisely control video images. You can set the rotation angle, scaling mode, and mirroring mode for video images. Sample code:

    ```
    // Set the mirroring mode for video images to horizontal mirroring, vertical mirroring, or no mirroring.
    fAliplayer.setMirrorMode(int mirrorMode)
    // Set the rotation angle for video images to 0°, 90°, 180°, or 270°.
    fAliplayer.setRotateMode(int rotateMode);
    // Set the scaling mode for video images to padding by keeping the original aspect ratio, fitting by keeping the original aspect ratio, or stretching.
    fAliplayer.setScalingMode(int scaleMode);
    ```

10. Set the mute mode and volume control.

    ApsaraVideo Player SDK for Flutter allows you to control video volumes. You can call the setMute method to set the mute mode for the player. In addition, you can call the setVolume method to set the player volume in the range of 0 to 1. Sample code:

    ```
    // Mute the player.
    fAliplayer.setMute(true);
    // Set the player volume. Valid values: 0 to 1.
    fAliplayer.setVolume(1f);
    ```

11. Set the playback speed.

    ApsaraVideo Player SDK for Flutter allows you to set the playback speed. You can call the setRate method to change the playback speed from 0.5x to 2x. The audio pitch remains unchanged at different speeds. Sample code:

    ```
    // Set the playback speed. You can change the playback speed from 0.5x to 2x.
    fAliplayer.setRate(1.0f);
    ```

12. Set the snapshot feature.

    ApsaraVideo Player SDK for Flutter provides the snapshot feature, which can be used to capture video snapshots. When you capture a snapshot, the player saves the source data of the video image to be captured and converts the source data to a bitmap. You can obtain the information about the captured snapshot after the OnSnapShot callback is fired. Sample code:

    ```
    // Set the callback for snapshot capture.
    fAliplayer.setOnSnapShot((path) {
        // Obtain the on-premises path in which the returned image is stored.
    });
    // Capture a snapshot of the current video image and set a path for storing the snapshot.
    fAliplayer.snapshot(String path);
    ```

13. Set the play-and-cache feature.

    ApsaraVideo Player SDK for Flutter supports the play-and-cache feature. This feature saves your data traffic during loop playback. To set the play-and-cache feature, call the CacheConfig method before you call the prepare method. Sample code:

    ```
    var map = {
        "mMaxSizeMB": the maximum size of the cache directory.
        "mMaxDurationS": the maximum length of a single cached file.
        "mDir": the cache directory.
        "mEnable": specifies whether to enable the play-and-cache feature.
    };
    fAliPlayer.setCacheConfig(map);
    ```

14. Set the preview feature.

    After you specify the preview duration, ApsaraVideo Player SDK for Flutter allows you to preview a video for the specified duration instead of the whole video.

    You can use the preview feature by using ApsaraVideo Player SDK for Flutter with ApsaraVideo VOD. The playback sources that support the preview feature are VidSts and VidAuth. In this example, VidSts is used. Sample code:

    ```
    fAliplayer.setVidSts(vid:Video ID,region:Access region,accessKeyId:Temporary AccessKey ID,accessKeySecret:Temporary AccessKey secret,securityToken:Security token,previewTime:Preview duration);
    ```

15. Enable or disable hardware decoding.

    ApsaraVideo Player SDK for Flutter supports hardware decoding based on the H.264 and H.265 standards. By default, the hardware decoding feature is enabled. If hardware decoding fails to be initialized, the player switches to software decoding to ensure normal video playback. Sample code:

    ```
    // Enable hardware decoding. By default, hardware decoding is enabled.
    fAliplayer.setEnableHardwareDecoder(bool isHardWare);
    ```

    You can set the onInfo callback. When hardware decoding is switched to software decoding, the onInfo callback is fired. Sample code:

    ```
    fAliplayer.setOnInfo((infoCode, extraValue, extraMsg) {
        if (infoCode == FlutterAvpdef.SWITCHTOSOFTWAREVIDEODECODER) {
            // Switch to software decoding.
        }
    });
    ```

16. Set a blacklist.

    ApsaraVideo Player SDK for Flutter allows you to set a blacklist for hardware decoding. If hardware decoding is not allowed for a device, you can use software decoding to avoid decoding failures. Sample code:

    ```
    // Obtain device information.
    flutterAliPlayre.createDeviceInfo().then((value) {
        //type : {FlutterAvpdef.BLACK_DEVICES_H264 / FlutterAvpdef.BLACK_DEVICES_HEVC}
        fAliplayer.addBlackDevice(type,value);
    });
    ```

17. Set the PlayerConfig class.

    You can use the PlayerConfig class to set the referer, user agent, network timeout period and number of retries, and HTTP headers, and configure buffer and delay settings. Sample code:

    ```
    var configMap = {
        'mStartBufferDuration': the startup loading time. Unit: milliseconds.
        'mHighBufferDuratio': the peak buffer duration. Unit: milliseconds.
        'mMaxBufferDuration': the maximum buffer duration. Unit: milliseconds.
        'mMaxDelayTime': the maximum buffer delay. This parameter is valid only for live streaming. Unit: milliseconds.
        'mNetworkTimeout': the network timeout period. Unit: milliseconds.
        'mNetworkRetryCount': the number of retries when a timeout occurs.
        'mMaxProbeSize': the maximum size of the probe. Unit: byte.
        'mReferrer': the referrer.
        'mHttpProxy': the HTTP proxy.
        'mEnableSEI': specifies whether to enable supplemental enhancement information (SEI).
        'mClearFrameWhenStop': specifies whether to clear video frames after the video playback stops.
    };
    fAliplayer.setConfig(configMap);
    ```


## List playback

1.  Create a list player.

    ```
    FlutterAliListPlayer fAliListPlayer;
    FlutterAliPlayerFactory().createAliListPlayer();
    ```

2.  Set the number of videos to be preloaded.

    You can significantly reduce the startup loading time by setting the number of videos to be preloaded to a proper value. Sample code:

    ```
    // Set the number of videos to be preloaded. The total number of loaded videos equals 1 plus twice the specified number.
    fAliListPlayer.setPreloadCount(count);
    ```

3.  Add or remove multiple playback sources.

    List playback supports the VidSts and UrlSource playback sources. You can use UrlSource for URL-based playback, and use VidSts for video ID-based playback. Sample code:

    ```
    // Add a VidSts playback source.
    fAliListPlayer.addVidSource({@required vid, @required uid});
    // Add a UrlSource playback source.
    fAliListPlayer.addUrlSource({@required url, @required uid});
    // Remove a playback source.
    fAliListPlayer.removeSource(String uid);
    ```

4.  Play a playback source.

    After you add one or more playback sources, call the moveTo method to play the content from the specified playback source. Sample code:

    ```
    // Call the method for URL-based playback or video ID-based playback. For the URL-based playback, you must enter the unique ID of a video. For the video ID-based playback, you must update the Security Token Service (STS) token.
    fAliListPlayer.moveTo({@required String uid,String accId,String accKey,String token,String region});
    ```

5.  Play the previous or next video in the list.

    You can call the moveToPrev method to play the previous video or call the moveToNext method to play the next video. Sample code:

    ```
    // The following methods are valid for URL-based playback, without the need to specify parameters.
    fAliListPlayer.moveToNext({@required accId,@required accKey,@required token,@required region}));
    fAliListPlayer.moveToPre({@required accId,@required accKey,@required token,@required region}));
    ```


## Video download

ApsaraVideo Player SDK for Flutter allows you to download videos from ApsaraVideo VOD by using VidSts and VidAuth. ApsaraVideo VOD supports the secure download mode and the normal download mode. You can set a download mode in the ApsaraVideo VOD console.

1.  Create and set a downloader.

    ```
    FlutterAliDownloader flutterAliDownloader;
    flutterAliDownloader = FlutterAliDownloader.init();
    // Set a path for storing downloaded files.
    flutterAliDownloader.setSaveDir(String path);
    ```

    ApsaraVideo Player SDK for Flutter allows you to download videos that are encrypted by using Alibaba Cloud proprietary cryptography. For security reasons, you must configure a security file for encryption verification in the SDK.

    ```
    var bytes = await rootBundle.load("The path of the encryptedApp.dat file");
    FlutterAliPlayerFactory().initService(bytes.buffer.asUint8List());
    ```

2.  Prepare for download.

    After you call the prepare method, a download source is prepared and operations for the prepare method are performed. Sample code:

    ```
    flutterAliDownloader.prepare(String type, String vid, {int index,String accessKeyId,String accessKeySecret,
          String securityToken, String playAuth})
    ```

3.  Start the download.

    After you call the start method, listeners are automatically set. A message is returned after a callback is fired. Sample code:

    ```
    // In the following code, vid specifies the ID of a video to be downloaded and index specifies the index of video resolution.
    flutterAliDownloader.start(String vid, int index).listen((event){
        if(event["method"] == "download_progress"){
            // The listener for the download progress.
            val progress = event["download_progress"];
        }else if(event["method"] == "download_process"){
            // The listener for the processing progress.
            vall process = event["download_process"];
        }else if(event["method"] == "download_completion"){
            // The listener for the completion of the download.
        }else if(event["method"] == "download_error"){
            // The error occurred during the download.
            // The error code.
            val errorCode = event['errorCode'];
            // The error message.
            val errorMsg = event['errorMsg'];
        }
        
    });
    ```

4.  Stop the download.

    ```
    flutterAliDownloader.stop(String vid, int index)
    ```

5.  Delete the content to be downloaded.

    If the deletion is complete, the downloaded on-premises file is also deleted. Sample code:

    ```
    flutterAliDownloader.delete(String vid, int index)
    ```

6.  Release a downloader.

    When a downloader is no longer required, call the release method to release it to prevent a memory leak. Sample code:

    ```
    flutterAliDownloader.release(String vid, int index)
    ```

7.  Update the download authentication information.

    ```
    flutterAliDownloader.updateSource(String type, String vid, String index,{String accessKeyId,
            String accessKeySecret,String securityToken,String playAuth})
    ```

8.  Configure the download.

    ```
    flutterAliDownloader.setDownloaderConfig(String vid, String index,{String userAgent,String referrer,
          String httpProxy,int connectTimeoutS,int networkTimeoutMs})
    ```

9.  Obtain the directory of the downloaded file.

    ```
    flutterAliDownloader.getFilePath(String vid, int index)
    ```


