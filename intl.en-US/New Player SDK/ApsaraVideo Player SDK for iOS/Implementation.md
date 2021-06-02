# Implementation

This topic shows you how to implement various features of ApsaraVideo Player SDK for iOS. This topic also provides sample code so that you can implement the features with ease.

## Playback

1.  Create a player.

    You can create the following player objects:

    -   AliPlayer
    -   AliListPlayer
    AliListPlayer and AliPlayer provide the same features, except that AliListPlayer provides the list playback feature. Example:

    ```
    self.player = [[AliPlayer alloc] init];
    self.listPlayer = [[AliListPlayer alloc] init];
    ```

    On-premises videos that are downloaded in secure download mode are encrypted and transcoded by Alibaba Cloud. To play such an on-premises video, you must configure a security file for encryption verification. We recommend that you configure the security file in your application, once for all. Example:

    ```
    NSString *encrptyFilePath = [[NSBundle mainBundle] pathForResource:@"encryptedApp" ofType:@"dat"];
    [AliPrivateService initKey:encrptyFilePath];
    ```

    **Note:** If you do not configure a correct security file for encryption verification, the ERROR\_DEMUXER\_OPENSTREAM error message appears when you play a video that is downloaded in secure download mode.

2.  Set player delegates.

    ApsaraVideo Player SDK for iOS provides multiple delegate methods, such as `onPlayerEvent` and `onError`. For more information, see [API reference](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/API reference.md). Example:

    ```
    @interface SimplePlayerViewController ()<AVPDelegate>
    @end
    - (void)viewDidLoad {
        self.player = [[AliPlayer alloc] init];
        self.player.playerView = self.avpPlayerView.playerView;
        self.player.delegate = self;
        //...
    }
    /**
     @brief The callback for an invalid delegate.
     @param player The method pointer for the player.
     @param errorModel The description of player errors. This parameter is similar to the AliVcPlayerErrorModel parameter.
     */
    - (void)onError:(AliPlayer*)player errorModel:(AVPErrorModel *)errorModel {
        // Indicate that an error occurs and the playback stops.
    }
    /**
     @brief The callback for player events.
     @param player The method pointer for the player.
     @param eventType The player event type. This parameter is similar to the AVPEventType parameter.
     */
    -(void)onPlayerEvent:(AliPlayer*)player eventType:(AVPEventType)eventType {
        switch (eventType) {
            case AVPEventPrepareDone: {
                // The completion of preparation.
            }
                break;
            case AVPEventAutoPlayStart:
                // The start of autoplay.
                break;
            case AVPEventFirstRenderedStart:
                // The appearance of the first frame.
                break;
            case AVPEventCompletion:
                // The completion of playback.
                break;
            case AVPEventLoadingStart:
                // The start of buffering.
                break;
            case AVPEventLoadingEnd:
                // The end of buffering.
                break;
            case AVPEventSeekEnd:
                // The end of seeking.
                break;
            case AVPEventLoopingStart:
                // The start of loop playback.
                break;
            default:
                break;
        }
    }
    /**
     @brief The callback for the current playback position.
     @param player The method pointer for the player.
     @param position The current playback position.
     */
    - (void)onCurrentPositionUpdate:(AliPlayer*)player position:(int64_t)position {
        // Update the progress bar.
    }
    /**
     @brief The callback for the buffer position.
     @param player The method pointer for the player.
     @ param position The current buffer position.
     */
    - (void)onBufferedPositionUpdate:(AliPlayer*)player position:(int64_t)position {
        // Update the buffer progress.
    }
    /**
     @ brief The callback for obtaining the track information.
     @param player The method pointer for the player.
     @param info track The array of track information. This parameter is similar to the AVPTrackInfo parameter.
     */
    - (void)onTrackReady:(AliPlayer*)player info:(NSArray<AVPTrackInfo*>*)info {
        // Obtain the information of different bitrates.
    }
    /**
     @brief The callback for displaying the subtitle.
     @param player The method pointer for the player.
     @param index The index number for the subtitle.
     @param subtitle The string of the subtitle.
     */
    - (void)onSubtitleShow:(AliPlayer*)player index:(int)index subtitle:(NSString *)subtitle {
        // Obtain the subtitle to display it.
    }
    /**
     @brief The callback for hiding the subtitle.
     @param player The method pointer for the player.
     @param index The index number for the subtitle.
     */
    - (void)onSubtitleHide:(AliPlayer*)player index:(int)index {
        // Indicate that subtitles are hidden.
    }
    /**
     @brief The callback for snapshot capture.
     @param player The method pointer for the player.
     @param image The image.
     */
    - (void)onCaptureScreen:(AliPlayer *)player image:(UIImage *)image {
        // Preview and save the snapshot.
    }
    /**
     @brief track The callback for the completion of switching.
     @param player The method pointer for the player.
     @param info The information after switching. This parameter is similar to the AVPTrackInfo parameter.
     */
    - (void)onTrackChanged:(AliPlayer*)player info:(AVPTrackInfo*)info {
        // Indicate the bitrate switching result.
    }
    //...
    ```

3.  Set a playback source and prepare for playback.

    ApsaraVideo Player SDK for iOS supports the following playback sources:

    -   AVPVidStsSource
    -   AVPVidAuthSource
    -   AVPVidMpsSource
    -   AVPUrlSource
    **Note:** You can use AVPUrlSource for URL-based playback, and use the other three playback sources for video ID \(VID\)-based playback. We recommend that ApsaraVideo VOD users choose AVPVidAuthSource. AVPVidMpsSource is available for ApsaraVideo for Media Processing users only.

    The following code uses AVPVidStsSource as an example:

    ```
        // Create the AVPVidStsSource playback source.
        AVPVidStsSource *source = [[AVPVidStsSource alloc] init];
        source.region = self. Access region;
        source.vid = self. VID;
        source.securityToken = self. Security token;
        source.accessKeySecret = self. Temporary AccessKey secret;
        source.accessKeyId = self. Temporary AccessKey ID;
         // Set the playback source.
        [self.player setStsSource:source];
         // Prepare for playback.
        [self.player prepare];
    ```

    **Note:** For more information about the video playback process and concepts in ApsaraVideo for Media Processing, see [Video playback]().

    For more information about the process of using the playback credential for playback, see [Use playback credentials](/intl.en-US/Developer Guide/Video play/Use playback credentials to play videos.md).

    For more information about region settings, see [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md).

4.  Set the UI view.

    If the playback source contains video images, you must set the UI view to display the video images in the player. Example:

    ```
        self.player.playerView = self.avpPlayerView.playerView;// The displayed UI view.
    ```

5.  Set playback control.

    You can create playback control buttons and associate click events with playback control methods to implement playback control.

    The basic control features include play, stop, pause, and seek. The seek feature is valid only for ApsaraVideo VOD. If you pause a live stream, the live stream stops at the current position. After you resume the playback of the live stream, the live stream starts from the paused position. Example:

    ```
        // Start the playback.
        [self.player start];
        // Pause the playback.
        [self.player pause];
        // Stop the playback.
        [self.player stop];
        // Seek. This operation may not direct the video to the precise point in time.
        [self.player seekToTime:position seekMode:AVP_SEEKMODE_INACCURATE];
         // Reset the player.
        [self.player reset];
        // Release the player. The player cannot be used after it is released.
        [self.player destroy];
        self.player = nil;
    ```

6.  Set multi-bitrate switching.

    ApsaraVideo Player SDK for iOS allows you to play an HTTP Live Streaming \(HLS\) stream in different bitrates. After the player is prepared by calling the `prepare` method, you can call the `getMediaInfo` method to obtain the bitrate information, which is indicated by values of the `TrackInfo` parameter.

    ```
    AVPMediaInfo *info = [self.player getMediaInfo];
    NSArray<AVPTrackInfo*>* tracks = info.tracks;
    ```

    During the playback, you can call the selectTrack method to switch the bitrate.

    ```
    [self.player selectTrack:track.trackIndex];
    ```

    You can call the `onTrackChanged` callback to view the switching result.

    ```
    - (void)onTrackChanged:(AliPlayer*)player info:(AVPTrackInfo*)info {
        if (info.trackType == AVPTRACK_TYPE_VIDEO) {
            // video changed
        }
        // etc
    }
    ```

7.  Set the autoplay feature.

    ApsaraVideo Player SDK for iOS supports the autoplay feature. Set the autoplay feature before you call the `prepare` method.

    ```
    self.player.autoPlay = YES;
    ```

    After you set the autoplay feature and prepare the player, videos are automatically played. Example:

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

    **Note:** When autoplay starts, the `AVPEventAutoPlayStart` callback instead of the `AVPEventPrepareDone` callback is fired.

8.  Set the loop playback feature.

    ApsaraVideo Player SDK for iOS supports the loop playback feature. To set the loop playback feature, call the `loop` method. The loop playback feature allows the player to play a video again when the player plays the video to the end position. Example:

    ```
    self.player.loop = YES;
    ```

    The callback for the start of loop playback is fired by the `AVPEventLoopingStart` callback.

9.  Set video image rotation, scaling, and mirroring.

    ApsaraVideo Player SDK for iOS provides multiple methods for you to precisely control video images. You can set the rotation angle, scaling mode, and mirroring mode for video images. Example:

    ```
    // Set the mirroring mode for video images to horizontal mirroring, vertical mirroring, or no mirroring.
    self.player.mirrorMode = AVP_MIRRORMODE_NONE;
    // Set the rotation angle for video images to 0°, 90°, 180°, or 270°.
    self.player.rotateMode = AVP_ROTATE_0;
    // Set the scaling mode for video images to padding by keeping the original aspect ratio, fitting by keeping the original aspect ratio, or stretching.
    self.player.scalingMode = AVP_SCALINGMODE_SCALEASPECTFIT;
    ```

    The following table describes the supported rotation angles for video images.

    |Value|Description|
    |-----|-----------|
    |AVP\_ROTATE\_0|Indicates that the rotation angle is 0°, in the clockwise direction.|
    |AVP\_ROTATE\_90|Indicates that the rotation angle is 90°, in the clockwise direction.|
    |AVP\_ROTATE\_180|Indicates that the rotation angle is 180°, in the clockwise direction.|
    |AVP\_ROTATE\_270|Indicates that the rotation angle is 270°, in the clockwise direction.|

    The following table describes the supported scaling modes for video images.

    |Value|Description|
    |-----|-----------|
    |AVP\_SCALINGMODE\_SCALEASPECTFIT|Indicates that the video image is scaled down into the UI view without changing the aspect ratio. This prevents image distortion.|
    |AVP\_SCALINGMODE\_SCALEASPECTFILL|Indicates that the video image is scaled up to fill the UI view without changing the aspect ratio. This prevents image distortion.|
    |AVP\_SCALINGMODE\_SCALETOFILL|Indicates that the video image is stretched to fill the UI view. This may cause image distortion if the video image and the UI view do not match in the aspect ratio.|

    The following table describes the supported mirroring modes for video images.

    |Value|Description|
    |-----|-----------|
    |AVP\_MIRRORMODE\_NONE|Indicates no mirroring.|
    |AVP\_MIRRORMODE\_HORIZONTAL|Indicates horizontal mirroring.|
    |AVP\_MIRRORMODE\_VERTICAL|Indicates vertical mirroring.|

10. Set the mute mode and volume control.

    ApsaraVideo Player SDK for iOS allows you to control video volumes. You can call the muted method to set the mute mode for the player. In addition, you can call the volume method to set the player volume in the range of \[0, 1\]. Example:

    ```
    // Mute the player.
    self.player.muted = YES;
    // Set the player volume. Value range: 0 to 1.
    self.player.volume = 1.0f;
    ```

11. Set the playback speed.

    ApsaraVideo Player SDK for iOS allows you to set the playback speed. You can call the rate method to change the playback speed from 0.5x to 2x. The audio pitch remains unchanged at different speeds. Example:

    ```
    // Set the playback speed. You can change the playback speed from 0.5x to 2x.
    self.player.rate = 1.0f;
    ```

12. Set the snapshot feature.

    ApsaraVideo Player SDK for iOS provides the snapshot feature, which can be used to capture video snapshots. When you capture a snapshot, the player saves the source data of the video image to be captured and converts the source data to a bitmap. Then, you can call the `onCaptureScreen` method to obtain the bitmap. Example:

    ```
    // The callback for snapshot capture.
    - (void)onCaptureScreen:(AliPlayer *)player image:(UIImage *)image {
        // Process the snapshot.
    }
    // Capture a snapshot of the current video image.
    aliyunVodPlayer.snapshot();
    ```

    **Note:** A snapshot does not contain the UI.

13. Set the play-and-cache feature.

    ApsaraVideo Player SDK for iOS supports the play-and-cache feature. This feature saves your data traffic during loop playback. To set the play-and-cache feature, call the `AVPCacheConfig` method before you call the `prepare` method. Example:

    ```
        AVPCacheConfig *config = [[AVPCacheConfig alloc] init];
        // Enable the play-and-cache feature.
        config.enable = YES;
        // Specify the maximum length of a single cached file. If a file exceeds the maximum length, it is not cached.
        config.maxDuration = 100;
        // Specify the cache directory. Specify it as required by your application.
        config.path = @"please use your cache path here";
        // Specify the maximum size of the cache directory. If the size of the cache directory exceeds the maximum value, the earliest cached file is deleted.
        config.maxSizeMB = 200;
        // Specify the cache settings for the player.
        [self.player setCacheConfig:config];
    ```

    You can use cached files only after you call the setCacheConfig method. After a video is cached, the cached files are used in the following scenarios:

    -   If you enable loop playback, the cached files are used when the player replays the video.
    -   The cached files are used when you create another player to play the same video.

        **Note:** For VID-based playback, information such as the VID is required to locate cached files. An online request must be sent to obtain the required information that determines which cached files are needed for VID-based playback.

    The following table describes the methods that can be used to query the path of a cached file.

    |Method|Description|Parameter|Return value|
    |------|-----------|---------|------------|
    |\(NSString \*\) getCacheFilePath:\(NSString \*\)URL|Queries the path of a cached file based on the video URL. To obtain the path, make sure that you have called the setCacheConfig method.|URL|The absolute path of the cached file.|
    |\(NSString \*\) getCacheFilePath:\(NSString \*\)vid format:\(NSString \*\)format definition:\(NSString \*\)definition|Queries the path of a cached file based on the VID.|    -   vid: the video ID.
    -   format: the video format.
    -   definition: the video resolution.
    -   previewTime: the preview duration.
|The absolute path of the cached file.|

    The play-and-cache feature does not mean that all videos are cached during playback. In some scenarios, videos are not cached. Example:

    -   When the AVPUrlSource playback source is used for URL-based playback, the video is not cached if the player uses the HLS protocol to play the video based on the video URL in the .m3u8 file. For other supported formats of URL-based playback, the player caches a video during playback as configured.
    -   When the player plays a video based on the VID, the player caches the video during playback as configured.
    -   A video is cached when the player reads all video data. Caching fails if the `stop` or `onError` method is called before the player reads all video data.
    -   Seeking inside the cached part of a video does not affect the caching result. Seeking outside the cached part causes a caching failure.
    -   If the verification information in the security file for encryption verification does not match the application information, caching fails.
    -   The `onPlayerEventInfo` callback returns the caching result.
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

    After you set the preview duration, the server returns the preview video instead of the whole video when you use ApsaraVideo Player SDK for iOS to play the video.

    You can use the preview feature by using ApsaraVideo Player SDK for iOS with ApsaraVideo VOD. The playback sources that support the preview feature are AVPVidStsSource and AVPVidAuthSource. For more information about how to set and use the preview feature, see [Configure the preview feature for VOD resources](/intl.en-US/Best Practice/Configure the preview feature for VOD resources.md). After you enable the preview feature, you can call the `setPreviewTime` method in VidPlayerConfigGen to set the preview duration. The following code uses AVPVidStsSource as an example:

    ```
    AVPVidStsSource *source = [[AVPVidStsSource alloc] init];
    ....
    VidPlayerConfigGenerator* vp = [[VidPlayerConfigGenerator alloc] init];
    [vp setPreviewTime:20];// Set the preview duration to 20s.
    source.playConfig = [vp generatePlayerConfig];// Specify the settings for the player.
    ...
    ```

    **Note:** You can call the VidPlayerConfigGen method to set the request parameters that are supported by the server. For more information, see [Request parameters](/intl.en-US/API Reference/Appendix/Request parameters.md).

15. Enable or disable hardware decoding.

    ApsaraVideo Player SDK for iOS supports hardware decoding based on the H.264 and H.265 standards. You can call the `enableHardwareDecoder` method to enable or disable the hardware decoding feature. By default, the hardware decoding feature is enabled. If hardware decoding fails to be initialized, the player switches to software decoding to ensure normal video playback. Example:

    ```
    // Enable hardware decoding. By default, hardware decoding is enabled.
    self.player.enableHardwareDecoder = YES;
    ```

    When hardware decoding is switched to software decoding, a callback is fired by the `onPlayerEvent` method. Example:

    ```
    -(void)onPlayerEvent:(AliPlayer*)player eventWithString:(AVPEventWithString)eventWithString description:(NSString *)description {
        if (eventWithString == EVENT_SWITCH_TO_SOFTWARE_DECODER) {
            // Switch to software decoding.
        }
    }
    ```

16. Set the referer.

    ApsaraVideo Player SDK for iOS provides the `AVPConfig` class for you to set the request referer. You can implement access control by setting referers in the blacklist or whitelist in the ApsaraVideo VOD console. The following code provides an example:

    ```
    // Query the configuration.
    AVPConfig *config = [self.player getConfig];
    // Set the referer.
    config.referer = referer;
    .... // Set other parameters.
    // Specify the settings for the player.
    [self.player setConfig:config];
    ```

17. Set the UserAgent.

    ApsaraVideo Player SDK for iOS provides the `AVPConfig` class for you to set the request UserAgent. After you set the UserAgent, the UserAgent information is contained in the requests from the player. The following code provides an example:

    ```
    // Query the configuration.
    AVPConfig *config = [self.player getConfig];
    // Set the UserAgent.
    config.userAgent = userAgent;
    .... // Set other parameters.
    // Specify the settings for the player.
    [self.player setConfig:config];
    ```

18. Set the network timeout period and the number of retries.

    You can use the `AVPConfig` class to set the network timeout period and the number of retries for the player. The following code provides an example:

    ```
    // Query the configuration.
    AVPConfig *config = [self.player getConfig];
    // Specify the network timeout period, in milliseconds.
    config.networkTimeout = 5000;
    // Set the number of retries when a timeout occurs. The networkTimeout parameter indicates the retry interval. By default, the networkRetryCount parameter is set to 2. If the networkRetryCount parameter is set to 0, retry is prohibited. The application determines the retry policy.
    config.networkRetryCount = 2;
    .... // Set other parameters.
    // Specify the settings for the player.
    [self.player setConfig:config];
    ```

    **Note:**

    -   If you set the networkRetryCount parameter to a value other than 0, the player retries the playback when it enters the loading status due to network errors. The number of retries is the value of the networkRetryCount parameter and the retry interval is the value of the networkTimeout parameter.
    -   If the loading status persists after the maximum number of retries is reached, the `onError` callback is fired. In this case, the AVPErrorModel.code method returns ERROR\_LOADING\_TIMEOUT.
    -   If the networkRetryCount parameter is set to 0, the onPlayerEvent callback is fired when a network timeout occurs. In this case, the eventWithString method returns EVENT\_PLAYER\_NETWORK\_RETRY. To resolve the issue, you can call the `reload` method of ApsaraVideo Player SDK for iOS to reload network packets or perform other operations as required.
19. Configure buffer and delay settings.

    Buffer control is important for a player. You can significantly shorten the startup loading time and improve playback smoothness with proper configuration. ApsaraVideo Player SDK for iOS provides the `AVPConfig` class for you to configure buffer and delay settings. Example:

    ```
    // Query the configuration.
    AVPConfig *config = [self.player getConfig];
    // Set the maximum buffer delay. Note: This parameter is valid only for live streaming. If the delay time exceeds the maximum limit, ApsaraVideo Player SDK for iOS synchronizes frames to keep the delay under the maximum delay time.
    config.maxDelayTime = 5000;
    // Set the maximum buffer duration. Unit: milliseconds. This parameter indicates the maximum video length that can be loaded by the player.
    config.maxBufferDuration = 50000;
    // Set the peak buffer duration. Unit: milliseconds. The player starts loading data when the network connection is poor. This parameter indicates the buffer duration beyond which the player stops loading.
    config.highBufferDuration = 3000;
    // Set the startup loading time. Unit: milliseconds. The shorter the startup loading time, the sooner the playback starts. A short startup loading time may cause the player to buffer soon after the playback starts.
    config.startBufferDuration = 500;
    // Set other parameters.
    // Specify the settings for the player.
    [self.player setConfig:config];
    ```

    **Note:** Make sure that the value of the startBufferDuration parameter is not greater than that of the highBufferDuration parameter, and that the value of the highBufferDuration parameter is not greater than that of the maxBufferDuration parameter.

20. Set HTTP headers.

    ApsaraVideo Player SDK for iOS provides the `AVPConfig` class for you to add HTTP headers to requests. Example:

    ```
    // Query the configuration.
    AVPConfig *config = [self.player getConfig];
    // Define a header.
    NSMutableArray *httpHeaders = [[NSMutableArray alloc] init];
    // For example, you must set a host when you use Alibaba Cloud HTTPDNS.
    [httpHeaders addObject:@"Host:xxx.com"];
    // Set the header.
    config.httpHeaders = httpHeaders;
    .... // Set other parameters.
    // Specify the settings for the player.
    [self.player setConfig:config];
    ```


## List playback

Nowadays, list playback for short video content is prevalent. ApsaraVideo Player SDK for iOS provides the complete list playback feature with the built-in preloading mechanism. The list playback feature significantly reduces the startup loading time.

1.  Create a player.

    `AliListPlayer` and `AliPlayer` provide the same features, except that AliListPlayer provides the list playback feature. To use the list playback feature, create an `AliListPlayer` object. Example:

    ```
    self.listPlayer = [[AliListPlayer alloc] init];
    ```

2.  Set the count of videos to be preloaded.

    You can significantly reduce the startup loading time by appropriately setting the count of videos to be preloaded. Example:

    ```
        // Set the count of videos to be preloaded. The total number of loaded videos equals 1 plus twice the count.
        self.listplyer.preloadCount = 2;
    ```

3.  Add or remove multiple playback sources.

    List playback supports the AVPVidStsSource and AVPUrlSource playback sources. You can use AVPUrlSource for URL-based playback, and use AVPVidStsSource for VID-based playback. Example:

    ```
    // Add an AVPVidStsSource playback source.
    [self.listPlayer addVidSource:videoId uid:UUIDString];
    // Add an AVPUrlSource playback source.
    [self.listPlayer addUrlSource:URL uid:UUIDString];
    // Remove a playback source.
    [self.listPlayer removeSource:UUIDString];
    ```

    **Note:**

    -   AVPVidAuthSource and AVPVidMpsSource are not supported for list playback.
    -   The uid parameter indicates the unique ID of a video. It is used to differentiate videos. Videos with the same unique ID are considered the same. If the player plays a video that is not the one you specified, check whether you specify a unique ID for multiple videos.
4.  Play a playback source.

    After you add one or more playback sources, you can play the content from the specified playback source. You can call the following methods to play a source:

    ```
        // Call the following method for URL-based playback.
        - (BOOL) moveTo:(NSString*)uid;
          // Call the following method for VID-based playback. You must specify the Security Token Service (STS) token for the stsInfo parameter. Make sure that the STS token is valid.
        - (BOOL) moveTo:(NSString*)uid accId:(NSString*)accId accKey:(NSString*)accKey token:(NSString*)token region:(NSString*)region;
    ```

5.  Play the previous or next video in the list.

    You can call the moveToPrev method to play the previous video or call the moveToNext method to play the next video. Example:

    ```
        // Play the next video. Note: This method is valid only for URL-based playback. The method is invalid for VID-based playback.
        - (BOOL) moveToNext;
        // Play the previous video. Note: This method is valid only for URL-based playback. The method is invalid for VID-based playback.
        - (BOOL) moveToPre;
          // Play the next video. Note: This method is valid only for VID-based playback.
        - (BOOL) moveToNext:(NSString*)accId accKey:(NSString*)accKey token:(NSString*)token region:(NSString*)region;
        // Play the previous video. Note: This method is valid only for VID-based playback.
        - (BOOL) moveToPre:(NSString*)accId accKey:(NSString*)accKey token:(NSString*)token region:(NSString*)region;
    ```


## Video download

ApsaraVideo Player SDK for iOS allows you to download videos from ApsaraVideo VOD by using AVPVidStsSource and AVPVidAuthSource. ApsaraVideo VOD supports the secure download mode and the normal download mode. You can set a download mode in the ApsaraVideo VOD console.

-   Normal download: Videos that are downloaded in normal download mode are not encrypted by Alibaba Cloud and can be played by third-party players.
-   Secure download: Videos that are downloaded in secure download mode are encrypted by Alibaba Cloud. You cannot use third-party players to play the downloaded videos. You can use only ApsaraVideo Player to play them.

1.  Create and set a downloader.

    Create a downloader. Example:

    ```
    AliMediaDownloader *downloader = [[AliMediaDownloader alloc] init];
    [downloader setSaveDirectory:self.downLoadPath];
    [downloader setDelegate:self];
    ```

    ApsaraVideo Player SDK for iOS allows you to download videos that are encrypted by using Alibaba Cloud proprietary cryptography. For security reasons, you must configure a security file for encryption verification in the SDK. We recommend that you configure the security file in your application, once for all. Example:

    ```
    NSString *encrptyFilePath = [[NSBundle mainBundle] pathForResource:@"encryptedApp" ofType:@"dat"];
    [AliPrivateService initKey:encrptyFilePath];
    ```

    **Note:** If you download a video in secure download mode and the information in the security file for encryption verification does not match the application information, the video download fails.

2.  Set listeners.

    The downloader provides multiple listeners. Example:

    ```
    -(void)onPrepared:(AliMediaDownloader *)downloader mediaInfo:(AVPMediaInfo *)info {
        // Indicate that the content to be downloaded is prepared.
    }
    -(void)onError:(AliMediaDownloader *)downloader errorModel:(AVPErrorModel *)errorModel {
        // Indicate that a download error occurs.
    }
    -(void)onDownloadingProgress:(AliMediaDownloader *)downloader percentage:(int)percent {
        // Indicate the percentage of the download progress.
    }
    -(void)onProcessingProgress:(AliMediaDownloader *)downloader percentage:(int)percent {
        // Indicate the percentage of the processing progress.
    }
    -(void)onCompletion:(AliMediaDownloader *)downloader {
        // Indicate that the download succeeds.
    }
    ```

3.  Prepare a download source.

    You can call the `prepare` method to prepare a download source. AVPVidStsSource and AVPVidAuthSource are supported as download sources. The following code uses AVPVidStsSource as an example:

    ```
    // Create the AVPVidStsSource download source.
    AVPVidStsSource* stsSource = [[AVPVidStsSource alloc] init];
    stsSource.vid = source.vid;// The video ID.
    stsSource.region = DEFAULT_SERVER.region;// The access region.
    stsSource.securityToken = DEFAULT_SERVER.securityToken;// The security token.
    stsSource.accessKeySecret = DEFAULT_SERVER.accessKeySecret;// The temporary AccessKey secret.
    stsSource.accessKeyId = DEFAULT_SERVER.accessKeyId;// The temporary AccessKey ID.
    // Prepare the download source.
    [downloader prepareWithVid:stsSource];
    ```

4.  Select the content to be downloaded from the prepared download source.

    After the download source is prepared, the `onPrepared` callback is fired. Select a track to be downloaded:

    ```
    -(void)onPrepared:(AliMediaDownloader *)downloader mediaInfo:(AVPMediaInfo *)info {
        NSArray<AVPTrackInfo*>* tracks = info.tracks;
        // In this example, download the content of the first track.
        [downloader selectTrack:[tracks objectAtIndex:0].trackIndex];
    }
    ```

5.  Update the download source and start the download.

    AVPVidStsSource or AVPVidAuthSource may expire before the download. Therefore, we recommend that you update the download source before you start the download. Example:

    ```
    // Update the download source.
    [downloader updateWithVid:vidSource]
    // Start the download.
    [downloader start];
    ```

6.  Release the downloader after the download succeeds or fails.

    After the download succeeds, call the `destroy` method to release the downloader.

    ```
    [self.downloader destroy];
    self.downloader = nil;
    ```


## Playback of encrypted live streams

ApsaraVideo Player SDK for iOS supports the playback of encrypted live streams. For more information about how to create and use a player, see the Playback section.

1.  Set a playback source.

    You must specify AVPLiveStsSource as the playback source. Example:

    ```
    // Create the AVPLiveStsSource playback source.
    AVPLiveStsSource *liveStsSource = [[AVPLiveStsSource alloc] initWithUrl:@"The URL of the encrypted live stream." accessKeyId:@"The temporary AccessKey ID."accessKeySecret:@"The temporary AccessKey secret." securityToken:@"The security token." region:@"The access region." domain:@"The name of the streaming domain." app:@"The name of the application to which the live stream belongs." stream:@"The name of the live stream."];
     // Set the playback source.
     [self.aliPlayer setLiveStsSource:liveStsSource];
     ......
     // Prepare for playback.
     [self.aliPlayer prepare];
    ```

2.  Monitor whether the STS token is valid.

    The encryption key may change during the playback of encrypted live streams. When the key is changed, the player requests the latest key from STS. You must monitor whether the STS token is valid. If the token is invalid, the playback of encrypted live streams is affected. The following code provides an example:

    ```
     __weak typeof(self) weakSelf = self;
    [self.aliPlayer setVerifyStsCallback:^AVPStsStatus(AVPStsInfo info) {
        if (info can be used) {
            return Valid;
        }
        if(A valid STS token can be obtained){
            Obtain STS();// This operation can be synchronously or asynchronously performed.
            return Pending;
        }
        [weakSelf.aliPlayer stop];
        return Invalid;
    }];
    ```

    After you obtain a valid STS token, you must call the `updateLiveStsInfo` method to update the STS token. If you fail to obtain the token, we recommend that you stop the playback.

    ```
    [self.aliPlayer updateLiveStsInfo:self.liveStsSource.accessKeyId accKey:self.liveStsSource.accessKeySecret token:self.liveStsSource.securityToken region:self.liveStsSource.region];
    ```

    **Note:** If you do not call the updateLiveStsInfo method, the player uses the expired STS token to obtain the encryption key. If the STS token becomes invalid, screen flickers may occur or the playback may fail.


