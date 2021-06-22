# Implementation

This topic shows you how to implement various features of ApsaraVideo Player SDK for web. This topic also provides sample code so that you can implement these features with ease.

## Continuous playback

The operations required for autoplay of the next video at the end of the current video differ based on the player type and the URL format of the next video.

-   Playback based on the URLs of videos that use the same streaming protocol

    For an HTML5 or a Flash player, you must configure the player to subscribe to the `ended` event. After the player receives the `ended` event, it calls the `loadByUrl` method to load the next video based on the specified URL. The following code provides an example:

    ```
    function endedHandle()
    {
      var newUrl = "";
      player.loadByUrl(newUrl);
    }
    player.on("ended", endedHandle);
    ```

-   Playback based on video IDs and playback credentials
    -   For an HTML5 player, you can configure the player to call the `replayByVidAndPlayAuth` method after it receives the `ended` event. The ID and playback credential of the next video must be passed to the method.```` The following code provides an example:

        ```
        function endedHandle()
        {
         var newPlayAuth = "";
         player.replayByVidAndPlayAuth(vid,newPlayAuth);
        }
        player.on("ended", endedHandle);
        ```

    -   A Flash player does not provide a method to switch to a video based on the video ID and playback credential. To switch to a video, you must destroy the existing player and create another player.```` The following code provides an example:

        ```
        function endedHandle()
        {
           var newPlayAuth = "";
           player.dispose(); // Destroy the existing player.
           $('#J_prismPlayer').empty();// The ID is the container ID of the player that is specified in HTML.
            // Create another player.
           player = new Aliplayer({
                     id: 'J_prismPlayer',
                     autoplay: true,
                     playsinline:true,
                     vid: vid,
                     playauth:newPlayAuth,
                     useFlashPrism:true
                });
           }
        }
        player.on("ended", endedHandle);
        ```

        **Note:** A playback credential is valid only for 100s. When a player calls the `replayByVidAndPlayAuth` method, the player must pass a new playback credential to the method. For more information, see [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md).``

-   Playback based on URLs of videos that use different streaming protocols

    Assume that an MP4 video is being played and the next video uses the HTTP Live Streaming \(HLS\) protocol. To enable autoplay of the next video at the end of the current video, you must create another player. The following code provides an example:

    ```
    function endedHandle()
    {
        var newUrl = ""; // The URL of the new video.
        player.dispose(); // Destroy the existing player.
         // Create another player.
       setTimeout(function(){
         player = new Aliplayer({
                  id: 'J_prismPlayer',
                  autoplay: true,
                  playsinline:true,
                  source:newUrl
             });
          }
       },1000);
    }
    player.on("ended", endedHandle);
    ```


## Resolution switching

The resolution switching feature is enabled only when videos of ApsaraVideo VOD and ApsaraVideo for Media Processing are played based on video IDs.

You can set the qualitySort attribute to list the resolutions in ascending or descending order.

-   A value of desc indicates the descending order from the highest to the lowest resolution.
-   A value of asc indicates the ascending order from the lowest to the highest resolution.

**Note:**

-   For an HTML5 player, you can set the format attribute to determine whether to play videos by using the MP4 or MP3 format. By default, the MP4 format is used.
-   The player remembers the resolution that you select when you change the resolution. The player plays a video in the previously selected resolution. If no resolution was previously selected, the player plays the video in the lowest resolution.
-   If the video fails to be played in the selected resolution, the player automatically switches to the next lower resolution and displays a message. This feature is supported only by HTML5 players.

## Screenshot

ApsaraVideo Player SDK V2.1.0 and later allow you to take snapshots in the JPEG format when you play a video. The player returns Base64-encoded and binary data of the snapshots along with the points in time of the snapshots.

-   Enable the snapshot feature for a Flash player

    Set the `snapshot` attribute to `true` to enable the snapshot feature for a Flash player. RTMP streams do not support this feature.

-   Enable the snapshot feature for an HTML5 player

    Add the settings of the snapshot user interface \(UI\) to the skinLayout attribute. The following code provides an example:

    ```
        skinLayout:[
        {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
        {
          name: "H5Loading", align: "cc"
        },
        {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
        {name: "infoDisplay"},
        {name:"tooltip", align:"blabs",x: 0, y: 56},
        {name: "thumbnail"},
        {
          name: "controlBar", align: "blabs", x: 0, y: 0,
          children: [
            {name: "progress", align: "blabs", x: 0, y: 44},
            {name: "playButton", align: "tl", x: 15, y: 12},
            {name: "timeDisplay", align: "tl", x: 10, y: 7},
            {name: "fullScreenButton", align: "tr", x: 10, y: 12},
            {name:"subtitle", align:"tr",x:15, y:12},
            {name:"setting", align:"tr",x:15, y:12},
            {name: "volume", align: "tr", x: 15, y: 10},
            {name: "snapshot", align: "tr", x: 5, y: 12},
          ]
        }
      ]
    ```

    To enable the snapshot feature for an HTML5 player, you must enable cross-origin resource sharing \(CORS\) for videos to allow anonymous requests. The following code provides an example:

    ```
      extraInfo:{
        crossOrigin:"anonymous"
      }
    ```

    **Note:** When you play Flash Video \(FLV\) videos by using an HTML5 player in Safari, the snapshot feature is not supported. The snapshot button does not appear even if you enable this feature.

-   Set snapshot size and quality

    Set the snapshot size and quality by calling the `setSanpshotProperties(width,height,rate)` method. By default, the size of a JPEG image is the same as that of the snapshot that is taken when you play a video. The following code provides an example:

    ```
    player.setSanpshotProperties(300,200,0.9)
    ```

-   Subscribe to the snapshoted event

    After a snapshot is taken, the `snapshoted event` is triggered and the snapshot data is returned. The following code provides an example:

    ```
    player.on("snapshoted", function(data) {
         console.log(data.paramData.time);
         console.log(data.paramData.base64);
         console.log(data.paramData.binary);
     });
    ```

    The preceding code contains the following parameters:

    -   time: the point in time of the snapshot.
    -   base64: the Base64-encoded string of the snapshot. This string can be directly used to display the image.
    -   binary: the binary data of the snapshot. The binary data can be used to upload the image.
-   Add a header that is used to enable CORS for an HTML5 player

    Canvas is the element that enables the snapshot feature for an HTML5 player. You must add a header that is used to enable CORS to the playback domain name. For more information, see [Configure CORS](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure CORS.md).

-   Add text watermarks to snapshots taken in an HTML5 player

    Set the `snapshotWatermark` attribute to enable the text watermark feature. The following table describes the parameters in the attribute.

    |Parameter|Description|
    |---------|-----------|
    |left|The distance to the left side.|
    |top|The height of the upper-left corner, including the height of text.|
    |text|The text in the watermark.|
    |font|The format of the text. You can set multiple font attributes together by separating them with spaces.     -   **font-style**: specifies the font style.
    -   **font-weight**: specifies the font weight.
    -   **font-size**: specifies the font size.
    -   **font-family**: specifies the font family. |
    |strokeColor|The color that is used to stroke the path of the shape.|
    |fillColor|The color that is used to fill the shape.|

    The following code provides an example:

    ```
    snapshotWatermark:{
        left:"100",
        top:"100",
        text:"test",
        font:"italic bold 48px arial",
        strokeColor:"red"
        fillColor:'green'
      }
    ```


## Time shifting in an HTML5 player

-   Enable time shifting
    -   You must enable time shifting in ApsaraVideo Live. For more information, see [Time shifting](/intl.en-US/API Reference/Time shifting/Time shifting.md).
    -   The following table describes the attributes that you must set to enable time shifting for a player.

        |Attribute|Description|
        |---------|-----------|
        |isLive|Set the value to **true**.|
        |liveTimeShiftUrl|The URL that is used to query the time shifting information.|
        |liveStartTime|The start time of live streaming.|
        |liveOverTime|The end time of live streaming.|
        |liveShiftSource|The HLS URL for time shifting. **Note:** This attribute is set only for FLV live streams. |

-   Time shifting UI

    The time shifting UI consists of a progress bar, which displays time in the area that supports time shifting.

    ![Time display](../images/p183664.png)

    **Note:** The time area displays the current playback time, end time of live streaming, and current live streaming time from left to right.

-   Change the end time of live streaming

    You can call the `liveShiftSerivce.setLiveTimeRange` method to change the start and end time of live streaming. The UI changes along with the changes. The following code provides an example:

    ```
    player.liveShiftSerivce.setLiveTimeRange("",'2018/01/04 20:00:00')
    ```

-   FLV for live streaming and HLS for time shifting

    To reduce latency, we recommend you use FLV for live streaming and HLS for time shifting.

    ApsaraVideo Player SDK provides the following attributes for you to enable this feature:

    -   source: the FLV URL for live streaming.
    -   liveShiftSource: the HLS URL for time shifting.
    The following code provides an example:

    ```
    {
     source:'http://localhost/live/test.flv',
     liveShiftSource:'http://localhost/live/test.m3u8',
    }
    ```

    In addition, you must register a callback for recreatePlayer so that a new player can be created when the playback switches to FLV live streaming. The following code provides an example:

    ```
    var player = "";
    var create = function(){
       player = new Aliplayer({
          source:'http://localhost/live/test.flv',
          liveShiftSource:'http://localhost/live/test.m3u8',
          recreatePlayer:function(){
          create();
          },
          .....
         },
         function(player){
          console.log('The player is created');
        });
    }
    ```


## Rotation and mirroring

-   The `videoHeight` and `videoWidth` attributes are used to set the height and width of a video. Typically, the height and width of a video are smaller than those of the container. This prevents the video from overflowing from the parent container during rotation and mirroring. The following code provides an example:

    ```
     width: 100% ', // The width of the container.
     height: 100% ', // The height of the container.
     videoHeight:"200px", // The height of the video.
    ```

    ![Effects](../images/p183673.png)

-   Method description

    |Parameter|Description|
    |---------|-----------|
    |setRotate|Sets the rotation angle. A positive value indicates clockwise rotation, whereas a negative value indicates anticlockwise rotation. Example: setRotate\(90\).|
    |getRotate|Obtains the rotation angle.|
    |setImage|Sets the mirroring type. Valid values:    -   **horizon**: horizontal mirroring.
    -   **vertical**: vertical mirroring. |

-   Browser adaptability
    -   Web browsers for PC and iOS support rotation and mirroring.
    -   Chrome and Firefox for Android support rotation and mirroring.
    -   WeChat and many other web browsers for Android may modify the settings of ApsaraVideo Player SDK without your permission or knowledge. In this case, rotation and mirroring are not supported.

## Multi-resolution playback

-   The source parameter specifies the URLs of streams in multiple resolutions in a JSON structure. The following code provides an example:

    ```
    source:'{"HD":"http://common.qupai.me/player/qupai.mp4","SD":"http://common.qupai.me/player/qupai.mp4"}'
    ```

-   Each key in the JSON structure maps a text value. The following code provides an example:

    ```
       "OD": "Original quality"
       "FD": "Low definition"
       "LD": "Standard definition"
       "SD": "High definition"
       "HD": "Ultra high definition"
       "2K": "2K"
       "4K": "4K"
    ```

    **Note:** If no text value is predefined for a key, the key is displayed as the text value on the UI.


## Usage notes

-   When an HTML5 player plays a video, the message "No 'Access-Control-Allow-Origin' header is present on the requested resource" may be displayed in the web browser console. To resolve this issue, configure CORS. For more information, see [Configure CORS](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure CORS.md).``
-   When a Flash player plays a video, a Canonical Name \(CNAME\) or CORS error may occur. To resolve this issue, configure CORS. For more information, see [Configure CORS](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure CORS.md).
-   When you play a video in WeChat or QQ on an Android mobile phone, the Tencent X5 browser hijacks the video tag to automatically play the video in full-screen mode. To resolve this issue, enable the immersive mode for the HTML5 player. For more information, see [How do I enable the immersive mode for the HTML5 player?](/intl.en-US/FAQ/How do I enable the immersive mode for the HTML5 player?.md).

## Other features

-   [Progress bar marking](https://developer.aliyun.com/article/686043)
-   [Customize components](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Customize components.md)
-   [Use the diagnostic tool](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Use the diagnostic tool.md)
-   [Configure the playback delay](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure the playback delay.md)
-   [Customize the error UI for the HTML5 player](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Customize the error UI for the HTML5 player.md)
-   [Configure CORS](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure CORS.md)
-   [Handle an error and resume live streaming](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Handle an error and resume live streaming.md)
-   [Configure the skinLayout attribute](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure the skinLayout attribute.md)
-   [Configure the player skin](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure the player skin.md)

