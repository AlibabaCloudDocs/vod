# Attributes and methods

This topic describes the attributes and events of ApsaraVideo Player SDK for web. This topic also provides the sample code of ApsaraVideo Player methods.

## Player attributes

|Attribute|Type|Description|
|---------|----|-----------|
|id|String|The ID of the dom element for the external container of the player.|
|source|String|The video playback URL. The URL is a separate URL. By default, a video is played based on the `video ID (VID) and playAuth`. **Note:** Source-based playback has the highest priority. You can use the source attribute to set multiple resolutions. Example: source:'\{"HD":"address1","SD":"address2"\}'. For more information, see [Multi-resolution playback](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Implementation.md). |
|vid|String|The media ID for media transcoding.|
|playauth|String|The unique credential for video playback. For more information about how to obtain the playAuth, see [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md).|
|height|String|The height of the player. Valid values:-   **100%**
-   **100px**

**Note:** The size cannot be smaller than 397 × 297 pixels for a Flash player in Google Chrome. |
|width|String|The width of the player. Valid values:-   **100%**
-   **100px**

**Note:** The size cannot be smaller than 397 × 297 pixels for a Flash player in Google Chrome. |
|videoWidth|String|The width of the video. This attribute is supported only by HTML5 players. For more information, see [Rotation and mirroring](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Implementation.md).|
|videoHeight|String|The height of the video. This attribute is supported only by HTML5 players. For more information, see [Rotation and mirroring](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Implementation.md).|
|preload|Boolean|Specifies whether to enable automatic loading for the player. This attribute is supported only by HTML5 players.|
|cover|String|The default thumbnail of the player. Enter a valid image URL. This attribute takes effect only when the autoplay attribute is set to **false**. [Cross-origin resource sharing \(CORS\)](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure CORS.md) must be enabled for the thumbnail when the video is played by Flash players.|
|isLive|Boolean|Specifies whether the playback is live streaming. If the playback is live streaming, you are not allowed to drag the progress bar.|
|autoplay|Boolean|Specifies whether to enable autoplay. This attribute does not take effect for mobile platforms. Safari 11 does not automatically enable autoplay. For more information, see [Enable Safari 11 \(MacOS High Sierra\) video autoplay](https://h5.m.youku.com//ju/safari11guide.html?spm=a2c4g.11186623.2.20.3b97bf802A2FeQ).|
|rePlay|Boolean|Specifies whether to enable automatic loop playback.|
|useH5Prism|Boolean|Specifies whether to use an HTML5 player for playback.|
|useFlashPrism|Boolean|Specifies whether to use a Flash player for playback.|
|playsinline|Boolean|Specifies whether to enable HTML5 embedded playback. This attribute does not take effect for specific Android-based web browsers.|
|showBuffer|Boolean|Specifies whether to show a buffer icon during playback. The default value is **true**.|
|skinRes|Url|The skin image. Do not modify this attribute unless necessary. For more information about how to modify the attribute, see [How do I configure the skin for the player?](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure the player skin.md)|
|skinLayout|Array \| Boolean|The layout of the components. If you do not set this attribute, the default layout is used for components. If this attribute is set to **false**, all the functional components are hidden. For more information, see [Configure the skinLayout attribute](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure the skinLayout attribute.md).|
|controlBarVisibility|String|The mode to display the control panel. The default value is **hover**. Valid values:-   **click**
-   **hover**
-   **always** |
|showBarTime|String|The length of time during which the control bar is automatically hidden, in milliseconds.|
|extraInfo|String|A JSON string that is used to customize operation information. This attribute is supported only by Flash players. Valid values:-   fullTitle: indicates that the video title is displayed when the video is played in full-screen mode. Example: test page.
-   m3u8BufferLength: the time duration of buffered TS fragments during the playback of M3U8 videos, in seconds.
-   liveStartTime: the start time of live streaming. It is used to indicate that the live streaming has not started. Example: 2016/08/17 12:00:00.
-   liveOverTime: the end time of live streaming. It is used to indicate that the live streaming ends. Example: 2016/08/17 14:00:00. |
|enableSystemMenu|Boolean|Specifies whether to display the shortcut menu upon a right-click. The default value is **false**.|
|format|String|The streaming URL format. This attribute is supported only by VID-based playback. Valid values:-   **mp4**
-   **m3u8**
-   **flv**
-   **mp3**

By default, this attribute is empty. This attribute is supported only by HTML5 players.|
|mediaType|String|The media type of the returned content. This attribute is supported only by VID-based playback. The default value is **video**. Valid values:-   **video**
-   **audio**: The value is set to audio only if audio files, such as audio files in the MP4 format, are played. This attribute is supported only by HTML5 players. |
|qualitySort|String|The sorting method. This attribute is supported only by playback based on the VID and playAuth. Valid values:-   **desc**: the descending order from higher to lower resolutions.
-   **asc**: the ascending order from lower to higher resolutions.

The default value is **asc**. This attribute is supported only by HTML5 players.|
|definition|String|The video resolution. Different resolutions are separated by commas \(,\), such as FD,LD. The value is a subset of resolutions of the stream corresponding to the VID. Valid values:-   **FD**: low definition
-   **LD**: standard definition
-   **SD**: high definition
-   **HD**: ultra high definition
-   **OD**: original quality
-   **2K**
-   **4K**

This attribute is supported only by HTML5 players.|
|defaultDefinition|String|The default video resolution. The value is the resolution of the stream corresponding to the VID. Valid values:-   **FD**: low definition
-   **LD**: standard definition
-   **SD**: high definition
-   **HD**: ultra high definition
-   **OD**: original quality
-   **2K**
-   **4K**

This attribute is supported only by HTML5 players.|
|x5\_type|String|Declares to use the immersive mode of the HTML5 player. Set this attribute to **H5** when you enable the immersive mode of the HTML5 player. For more information, see [How do I enable the immersive mode for the HTML5 player?](/intl.en-US/FAQ/How do I enable the immersive mode for the HTML5 player?.md).|
|x5\_fullscreen|Boolean|Specifies whether to enter the full-screen mode during video playback by Tencent Browsing Service \(TBS\). The default value is **false**. Valid values:-   **false**: disables background playback.
-   **true**: enables background playback.

For more information, see [How do I enable the immersive mode for the HTML5 player?](/intl.en-US/FAQ/How do I enable the immersive mode for the HTML5 player?.md).|
|x5\_video\_position|String|The position of a video player on the screen. The default value is **center**. Valid values:-   **center**
-   **top**

For more information, see [How do I enable the immersive mode for the HTML5 player?](/intl.en-US/FAQ/How do I enable the immersive mode for the HTML5 player?.md).|
|x5\_orientation|String|The orientation of the video that is played by TBS. Valid values:-   **landscape**
-   **portrait**

For more information, see [How do I enable the immersive mode for the HTML5 player?](/intl.en-US/FAQ/How do I enable the immersive mode for the HTML5 player?.md).|
|x5LandscapeAsFullScreen|String|Specifies whether to enable the landscape mode for full-screen playback by TBS. The default value is **true**. Valid values:-   **true**: Enable the landscape mode.
-   **false**: Enable the portrait mode. |
|autoPlayDelay|Number|The playback delay, in seconds. For more information, see [Configure the playback delay](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure the playback delay.md).|
|autoPlayDelayDisplayText|String|The text that notifies users of the playback delay. For more information, see [Configure the playback delay](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure the playback delay.md).|
|language|String|The language that is used by the player. The default value is **zh-cn**. If this attribute is empty, the language of the web browser applies. Valid values:-   **zh-cn**: Chinese
-   **en-us**: English |
|languageTexts|JSON|The JSON structure of the custom player language text. The key value must correspond to the value of the language attribute. Example: \{jp:\{Play:"Play"\}\}. For more information about custom values, see [JSON structure](https://player.alicdn.com/lang.json?spm=a2c4g.11186623.2.27.6bdcbf809nmsYQ&file=lang.json).|
|snapshot|Boolean|Specifies whether to enable the snapshot capture feature in Flash players.|
|snapshotWatermark|Object|The snapshot watermark in HTML5.|
|useHlsPluginForSafari|Boolean|Specifies whether to enable the HTTP Live Streaming \(HLS\) plug-in for playback in Safari, except for Safari 11.|
|enableStashBufferForFlv|Boolean|Specifies whether to enable playback caching during FLV playback in HTML5. This attribute takes effect only for live streaming.|
|stashInitialSizeForFlv|Number|The initial cache size for FLV playback in HTML5. This attribute takes effect only for live streaming.|
|loadDataTimeout|Number|The buffering duration that is required to display a message prompting users to switch to a lower resolution, in seconds. The default value is 20.|
|waitingTimeout|Number|The maximum buffer duration, in seconds. After the specified duration, an error message appears. The default value is 60.|
|liveStartTime|String|The start time of live streaming, in the format of yyyy/MM/dd HH:mm:ss. Example: 2018/01/04 12:00:00.|
|liveOverTime|String|The end time of live streaming, in the format of yyyy/MM/dd HH:mm:ss. Example: 2018/01/04 12:00:00.|
|liveTimeShiftUrl|String|The URL for querying available time shifting during live streaming. For more information, see [Time shifting](/intl.en-US/API Reference/Time shifting/Time shifting.md).|
|liveShiftSource|String|The HLS URL for FLV playback. For more information, see [Time shifting](/intl.en-US/API Reference/Time shifting/Time shifting.md).|
|recreatePlayer|Function|The method that is used to create a player during the switching between FLV live streaming and HLS time shifting. For more information, see [Time shifting](/intl.en-US/API Reference/Time shifting/Time shifting.md).|
|diagnosisButtonVisible|Boolean|Specifies whether to display the diagnosis button. The default value is **true**. Valid values:-   **true**: yes
-   **false**: no |
|disableSeek|Boolean|Specifies whether to disable the seeking feature of the progress bar. The default value is **false**.-   **true**: yes
-   **false**: no

This attribute is supported only by Flash players.|
|encryptType|int|The encryption type. When a video that is encrypted by using Alibaba Cloud proprietary cryptography is played, the default value is **0**. Valid values:-   **0**: Enables encryption.
-   **1**: Disables encryption.

**Note:**

-   A video that is encrypted by using Alibaba Cloud proprietary cryptography is played based on the VID and [playAuth](/intl.en-US/FAQ/Player/FAQ about parameter parsing.md).
-   A video that is encrypted in HLS encryption mode is played based on the URL. For more information, see [Encrypt videos for playback](/intl.en-US/New Player SDK/Best Practices/Encrypt videos for playback.md). |
|progressMarkers|Array|The content array of the marker on the progress bar. For more information, see [Mark on the progress bar](https://developer.aliyun.com/article/686043).|
|vodRetry|int|The number of retry times when VOD playback fails. The default value is 3.|
|liveRetry|int|The number of retry times when live stream playback fails. The default value is 5.|
|hlsFrameChasing|boolean|Specifies whether to enable frame synchronization for HLS-based playback.|
|chasingFirstParagraph|number|The latency after which frame synchronization of phase 1 is enabled. The default value is 20. The unit is seconds.|
|chasingSecondParagraph|number|The latency after which frame synchronization of phase 2 is enabled. The default value is 40. The unit is seconds.|
|chasingFirstSpeed|number|The playback speed when frame synchronization of phase 1 is enabled. The default value is 1.1.|
|chasingSecondSpeed|number|The playback speed when frame synchronization of phase 2 is enabled. The default value is 1.2.|

## Player methods

Operations must be used after the ready event occurs or during callback in the player creation ready state. In HTML5, operations can be called by the callback function of the constructor that is used to create a player. The following code snippets provide examples:

-   Flash player

    ```
    // Flash player
     player.on('ready',function(e) {
        player.play();
     });
    ```

-   HTML5 player

    ```
    // HTML5 player
     var player = new Aliplayer({},function(player) {
        player.play();
     });
    ```


|Method|Method|Description|
|------|------|-----------|
|play|N/A|Plays a video.|
|pause|N/A|Pauses a video.|
|replay|N/A|Replays a video.|
|seek|time|Seeks to the video image at the specific point in time to start playing. The unit of the time parameter is seconds.|
|getCurrentTime|N/A|Obtains the current playback time, in seconds.|
|getDuration|N/A|Obtains the total duration of a video, in seconds. The value can be obtained only after the video is loaded or after the play event occurs.|
|getVolume|N/A|Obtains the current volume. The return value is a real number ranging from **0 to 1**. This method does not take effect on iOS terminals and specific Android terminals.|
|setVolume|N/A|Sets the volume. The volume value is a real number ranging from **0 to 1**. This method does not take effect on iOS terminals and specific Android terminals.|
|loadByUrl|url and time|Obtains the URL for video playback. The value of the time parameter is optional and the unit of the time parameter is seconds. Only switching between videos of the same format, such as MP4, FLV, or M3U8, is supported. Switching between Real-Time Messaging Protocol \(RTMP\) live streams is not supported.|
|replayByVidAndPlayAuth|vid: the video ID. playauth: the playback credential.|Only HTML5 players are supported. Switching between videos of different formats is not supported. Switching between RTMP live streams is not supported.|
|replayByVidAndAuthInfo|This method is available for ApsaraVideo for Media Processing users only. Parameters in sequence are vid, accId, accSecret, stsToken, authInfo, and domainRegion.|Only HTML5 players are supported. Switching between videos of different formats is not supported. Switching between RTMP live streams is not supported.|
|setPlayerSize|w and h|Sets the size of the player. Valid values:-   **400px**
-   **60%**

The size cannot be smaller than 397 × 297 pixels for a Flash player in Google Chrome.|
|setSpeed|speed|Manually sets the playback speed. Playback speed control is supported only by HTML5 players. This method may not take effect for mobile platforms, such as WeChat for Android. By default, the user interface \(UI\) of playback speed control is enabled. If the `skinLayout` attribute is customized, you must add `speedButton` to the array. Example: \{name:"speedButton",align:"tr",x:10,y:23\}.|
|setSanpshotProperties|width: the width of the snapshot. height: the height of the snapshot. rate: the quality of the snapshot.|Sets parameters for snapshots.|
|fullscreenService.requestFullScreen|N/A|Enables the full-screen mode of the player. This method is supported only by HTML5 players.|
|fullscreenService.cancelFullScreen|N/A|Exits the full-screen mode of a player. This method does not take effect on iOS terminals. This method is supported only by HTML5 players.|
|fullscreenService.getIsFullScreen|N/A|Obtains the full screen status of the player. This method is supported only by HTML5 players.|
|getStatus|N/A|Obtains the player status. Valid values:-   **init**: The player is initializing.
-   **ready**: The player is ready.
-   **loading**: The player is loading data.
-   **play**: The player is resumed from the Pause state.
-   **pause**: The player is paused.
-   **playing**: The player is playing.
-   **waiting**: The player is waiting for buffering.
-   **error**: An error has occurred.
-   **ended**: The playback ends. |
|liveShiftSerivce.setLiveTimeRange|Start time and end time|Sets the start time and end time of live streaming. This method can be called only for time shifting during live streaming. Example: player.liveShiftSerivce.setLiveTimeRange \("", '2018/01/04 20:00:00'\).|
|setRotate|rotate: the rotation angle.|Sets the rotation angle. A positive value indicates clockwise rotation, whereas a negative value indicates anticlockwise rotation. Example: setRotate\(90\). For more information, see [Rotation and mirroring](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Implementation.md).|
|getRotate|N/A|Obtains the rotation angle. For more information, see [Rotation and mirroring](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Implementation.md).|
|setImage|image: the image type.|Sets the image type. Valid values:-   **horizon**: horizontal
-   **vertical**: vertical

Example: setImage\('horizon'\). For more information, see [Rotation and mirroring](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Implementation.md).|
|dispose|N/A|Destroys a player.|
|setCover|cover: the thumbnail URL.|Sets the thumbnail URL.|
|setProgressMarkers|marker: the marker dataset.|Sets markers.|
|setPreviewTime|time: the preview duration.|Sets the preview duration, in seconds. For more information, visit [Preview \(URL\)](https://player.alicdn.com/aliplayer/presentation/index.html?spm=a2c4g.11186623.2.35.6bdcbf80h3YEIM&type=preview).|
|getPreviewTime|N/A|Obtains the preview duration.|
|isPreview|N/A|Specifies whether to enable the preview feature.|

## Player events

|Event|Description|
|-----|-----------|
|ready|The event that is invoked when the video initialization button of the player is rendered. Initial setting of the UI must be triggered after this event to prevent the UI from being overwritten during initialization. The methods that are provided by a player can be called only after this event occurs.|
|play|The event that is invoked when a paused video is played again.|
|pause|The event that is invoked when a video is paused.|
|canplay|The event that is invoked when an audio or video file is ready for playback. This event can be invoked many times and is supported only by HTML5 players.|
|playing|The event that is invoked during playback. This event can be invoked many times.|
|ended|The event that is invoked at the end of the current video.|
|liveStreamStop|The event that is invoked when live streams are interrupted. For the playback of M3U8, FLV, and RTMP videos, this event is invoked when the player fails to obtain data after five consecutive retries. This event indicates that live streams are interrupted or the video needs to be loaded again. **Note:** If the live streams of M3U8, FLV, and RTMP videos are interrupted or an error occurs, the player automatically retires five times. You do not need to set the retry event for the player. |
|onM3u8Retry|The retry event that is invoked when M3U8 live streams are interrupted. This event is invoked only once when streaming is interrupted.|
|hideBar|The event to automatically hide the control bar.|
|showBar|The event to automatically display the control bar.|
|waiting|The data caching event.|
|timeupdate|The event that is invoked when the playback position changes. This event is supported only by HTML5 players. You can obtain the current playback time by using the getCurrentTime method.|
|snapshoted|The event that is invoked when a snapshot is captured.|
|requestFullScreen|The event to enable the full-screen mode. This event is supported only by HTML5 players.|
|cancelFullScreen|The event to exist the full-screen mode. This event is not invoked on iOS terminals. This event is supported only by HTML5 players.|
|error|The error event.|
|startSeek|The event that is invoked when seeking starts. The return value is the start time of seeking.|
|completeSeek|The event that is invoked when seeking is complete. The return value is the end time of seeking.|
|resolutionChange|The event that is invoked when the resolution is switched for live stream playback.|
|seiFrame|The event that is invoked when the supplemental enhancement information \(SEI\) notification is received for HLS-based playback.|

## Event subscription

-   You can subscribe to an event by using the on method of a player instance. The following code provides an example:

    ```
    var handleReady = function(e)
    {
        console.log(e);
    }
    player.on('ready',handleReady);
    ```

-   You can unsubscribe from an event by using the off method of a player instance. The following code provides an example:

    ```
    player.off('ready',handleReady);
    ```


## Error codes

|Code|Description|
|----|-----------|
|4001|The error message returned because the parameter is invalid.|
|4002|The error message returned because the playAuth expired.|
|4003|The error message returned because the streaming URL is invalid.|
|4004|The error message returned because the streaming URL does not exist.|
|4005|The error message returned because an error has occurred when the player starts to download data. Check whether the network or the streaming URL is available.|
|4006|The error message returned because an error has occurred when the player starts to download metadata.|
|4007|The error message returned because a playback error has occurred.|
|4008|The error message returned because the loading has timed out. Check whether the network or the streaming URL is available.|
|4009|The error message returned because a data request error has occurred. Check whether the network or the streaming URL is available.|
|4010|The error message returned because encrypted videos are not supported for playback.|
|4011|The error message returned because the format of the video to be played is not supported.|
|4012|The error message returned because a playAuth parsing error has occurred.|
|4013|The error message returned because a playback data decoding error has occurred. Check whether the browser supports the video format.|
|4014|The error message returned because the network is unavailable.|
|4015|The error message returned because retrieving data is aborted.|
|4016|The error message returned because data loading failed due to a network error.|
|4017|The error message returned because the returned streaming URL is empty.|
|4100|The error message returned because a signaling request error occurs.|
|4110|The error message returned because WebRTC is not supported.|
|4111|The error message returned because the browser is not supported.|
|4112|The error message returned because the browser version is outdated.|
|4113|The error message returned because H.264 is not supported.|
|4114|The error message returned because the offer fails to be created.|
|4115|The error message returned because autoplay fails.|
|4116|The error message returned because the streaming URL uses an invalid protocol.|
|4118|The error message returned because the specified HTML element is not an audio stream or a video stream.|
|4200|The error message returned because the playback failed.|
|4400|The error message returned because an unknown error has occurred. Loading resources failed due to a server or network error or an unsupported format.|
|4500|The error message returned because a server request error has occurred. Check the VOD request on the network.|

