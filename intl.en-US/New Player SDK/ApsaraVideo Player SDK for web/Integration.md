# Integration

ApsaraVideo Player SDK for web supports playback in Flash and HTML5 players. This topic describes the supported formats and the player adaptability. This topic also provides sample code for you to use the SDK with ease.

## Supported formats

ApsaraVideo Player SDK for web supports playback in Flash and HTML5 players.

-   Flash player \(update stopped\):
    -   Video formats: MP4, FLV, M3U8, and RTMP
    -   Video encoding format: H.264
    -   Audio encoding formats: AAC and MP3
    -   Audio format: MP3
-   HTML5 player:
    -   Video formats: MP4, FLV, and M3U8
    -   Video encoding format: H.264
    -   Audio encoding format: AAC
    -   Audio format: MP3

## Adaptability

-   Flash player

    |Browser|MP4|FLV|M3U8|RTMP|MP3|
    |-------|---|---|----|----|---|
    |Google Chrome|√|√|√|√|√|
    |Firefox|√|√|√|√|√|
    |Internet Explorer|Internet Explorer 8 and later|Internet Explorer 8 and later|Internet Explorer 8 and later|Internet Explorer 8 and later|Internet Explorer 8 and later|
    |Microsoft Edge|√|√|√|√|√|
    |Opera|√|√|√|√|√|
    |Safari|√|√|√|√|√|

    **Note:** Flash players are not supported on mobile terminals, such as iOS and Android terminals.

    To use a Flash player in Internet Explorer 8, you must add a link to reference the json.min.js file in Internet Explorer 8. The following code provides an example:

    ```
    https://g.alicdn.com/de/prismplayer/2.9.3/json/json.min.js
    ```

-   HTML5 player

    |Browser|MP4|FLV|M3U8|RTMP|MP3|
    |-------|---|---|----|----|---|
    |Google Chrome|√|Google Chrome 34 and later|Google Chrome 34 and later|×|√|
    |Firefox|√|Firefox 49 and later|Firefox 49 and later|×|√|
    |Internet Explorer|Internet Explorer 9 and later|    -   Internet Explorer 11 and later
    -   Windows 8.1 and later
|    -   Internet Explorer 11 and later
    -   Windows 8.1 and later
|×|Internet Explorer 9 and later|
    |Microsoft Edge|√|√|√|×|√|
    |Opera|√|√|√|×|√|
    |Safari|√|Safari 8 and later|Safari 8 and later|×|√|

    **Note:**

    -   To play FLV and M3U8 videos, you must enable [cross-origin resource sharing \(CORS\)](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Advanced features/Configure CORS.md) for browsers on PCs.
    -   The [Native HLS Playback](https://chrome.google.com/webstore/detail/native-hls-playback/emnphkkblegpebimobpbekeedfgemhof?hl=zh-CN) plug-in must be installed to play M3U8 videos in Google Chrome that uses mobile simulators on PCs.
    -   You cannot play video streams in the FLV format in Internet Explorer 11 for Windows 8 and later. This is because the value of the mseLiveFlvPlayback parameter is false in the flv.js file for Internet Explorer 11.
    |Mobile terminal|MP4|FLV|M3U8|RTMP|MP3|
    |---------------|---|---|----|----|---|
    |iOS|√|×|√|×|√|
    |Android|√|×|Android 4.0 and later|×|√|

    **Note:** HTML5 players do not support the playback of FLV and RTMP videos on mobile terminals.

-   HTML5 playback of videos on which Alibaba Cloud HTTP-Live-Streaming \(HLS\) encryption is performed

    |Encryption|iOS|Android|PC|
    |----------|---|-------|--|
    |HLS encryption|√|√|    -   Google Chrome
    -   FireFox
    -   Safar
    -   iEdge
    -   Internet Explorer 11 and later
    -   Windows 8.1 and later |
    |Proprietary cryptography|×|Google Chrome for Android|    -   Google Chrome
    -   FireFox
    -   Safar
    -   iEdge
    -   Internet Explorer 11 and later
    -   Windows 8.1 and later |

    Encrypted playback:

    -   For more information about encrypted playback in ApsaraVideo VOD, see [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md).
    -   For more information about encrypted playback in ApsaraVideo for Media Processing, see [Encryption]().
    **Note:** We recommend that you use Google Chrome to play videos on which Alibaba Cloud proprietary cryptography is performed.

-   Enable anti-debugging for Alibaba Cloud proprietary cryptography

    You can import the aliplayer-vod-anti-min.js file to enable the anti-debugging feature. Considering the debugging during development, you can import the JavaScript file to a published product. You can use the following sample code to import the JavaScript file:

    ```
      <script src="https://g.alicdn.com/de/prismplayer/2.9.3/hls/aliplayer-vod-anti-min.js"></script>
    ```

    **Note:** If you cannot open the page after you close the development tool, you must open the page on a new tab.


## HTML5 adaptability

-   By default, browsers on mobile terminals play videos in full-screen mode. You must complete the settings based on specific scenarios.
    -   iOS: To enable inline playback on an iOS app, you must set the `playsinline` parameter to `true` and set the WebView parameter `allowsInlineMediaPlayback` for ApsaraVideo Player. This way, videos are played in inline mode on the app.
    -   Android: The Android system supports different custom versions. Different versions use different methods to implement the HTML5 video tag. Therefore, the consistency in video playback in Android is harder to ensure than that in iOS. If browsers on mobile terminals support inline playback, you can set the `playsinline` parameter to `true`. You can also enable the immersive mode in X5-kernel browsers, such as QQ Browser and WeChat, to achieve an effect similar to inline playback.
    -   Safari: In iOS earlier than iOS 10, automatic video playback in full-screen mode cannot be disabled in Safari.
-   Autoplay is not triggered even though you have set the `autoplay` parameter to `true`.
    -   Browsers on mobile terminals: To enable autoplay in an HTML5 player, you can set the `autoplay` parameter or call the `play()` method. However, autoplay is disabled on mobile terminals. A common solution is to manually trigger playback. For example, you can listen to user click events and call the `play()` method.

        **Note:** Autoplay may be supported by specific browsers and WebView-based applications, especially those in Android.

    -   Safari: Autoplay is not supported in Safari later than Safari 11 in macOS High Sierra.
    -   Google Chrome: Autoplay is not supported in Google Chrome later than Google Chrome 55.
-   The `getVolume` and `setVolume` methods do not take effect on iOS apps and specific Android apps.
-   The playback speed control does not take effect when the speed control settings are not supported by specific browsers on mobile terminals, such as WeChat for Android.
-   Specific mobile terminals do not support the snapshot feature due to security reasons. For example, you may obtain black snapshots in Android 4.4.1 or due to browser issues. You can use the [snapshot testing tool](https://static.qupaicloud.com/aliplayer/snapshot.html?spm=a2c4g.11186623.2.20.3f571c4cvvF7Kj) to verify whether a browser supports the snapshot feature.

## Import a reference file

You can initialize a player by referencing a .js file with the following content on the page, without the need to add the dependency on a frontend .js library:

```
https://g.alicdn.com/de/prismplayer/2.9.3/aliplayer-min.js
```

**Note:** If gibberish text occurs, you can use the `<script></script>` tags to add the charset attribute and set this attribute to `"utf-8"`.

The referenced .js file contains the adaptation logic across mobile terminals for Flash and HTML5. If you want to use only one of Flash and HTML5 players, you can reference only the required .js file to reduce the file size.

-   Flash player:

    ```
    https://g.alicdn.com/de/prismplayer/2.9.3/aliplayer-flash-min.js
    ```

-   HTML5 player:

    ```
    https://g.alicdn.com/de/prismplayer/2.9.3/aliplayer-h5-min.js
    ```


If you need to use an HTML5 player, reference a .css file with the following content:

```
<!DOCTYPE html>
<html>
    <head>
     <link rel="stylesheet" href="https://g.alicdn.com/de/prismplayer/2.9.3/skins/default/aliplayer-min.css" />
     <script charset="utf-8" type="text/javascript" src="https://g.alicdn.com/de/prismplayer/2.9.3/aliplayer-min.js"></script>
    </head>
</html>
```

## SDK usage

In addition to video playback by using video source files, ApsaraVideo Player SDK can also play videos by ApsaraVideo.

-   For more information about ApsaraVideo VOD, see [Use playback credentials to play videos](/intl.en-US/Developer Guide/Video play/Use playback credentials to play videos.md).
-   For more information about ApsaraVideo for Media Processing, see [Play videos]().

The following code provides an example:

```
<!DOCTYPE html>
<html>
    <head>
     <meta charset="UTF-8">
     <meta name="viewport"   content="width=device-width, height=device-height, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no"/>
     <title>User test case</title>
     <link rel="stylesheet" href="https://g.alicdn.com/de/prismplayer/2.9.3/skins/default/aliplayer-min.css" />
     <script charset="utf-8" type="text/javascript" src="https://g.alicdn.com/de/prismplayer/2.9.3/aliplayer-min.js"></script>
    </head>
    <body>
        <div  class="prism-player" id="J_prismPlayer"></div>
        <script>
            var player = new Aliplayer({
            id: 'J_prismPlayer',
            width: '100%',
            autoplay: true,
            // Playback based on a streaming URL. This method has the highest priority.
            source: 'Streaming URL',
            // Playback method 2: recommended for ApsaraVideo VOD users.
            vid : '1e067a2831b641db90d570b6480fbc40',
            playauth : 'ddd',
            cover: 'http://liveroom-img.oss-cn-qingdao.aliyuncs.com/logo.png',
            encryptType:1, // Set this parameter when you play video streams on which Alibaba Cloud proprietary cryptography is performed.
            // Playback method 3: applicable only to ApsaraVideo for Media Processing users.
            vid : '1e067a2831b641db90d570b6480fbc40',
            accId: 'dd',
            accSecret: 'dd',
            stsToken: 'dd',
            domainRegion: 'dd',
            authInfo: 'dd',
            // Playback mode 4: playback based on Security Token Service (STS).
            vid : '1e067a2831b641db90d570b6480fbc40',
            accessKeyId: 'dd',
            securityToken: 'dd',
            accessKeySecret: 'dd',
             region:'cn-shanghai',//eu-central-1,ap-southeast-1
            },function(player){
                console.log ('The player is created.')
           });
        </script>
    </body>
</html>
```

You can configure the player settings on the [Online Settings](https://player.alicdn.com/aliplayer/setting/setting.html?spm=a2c4g.11186623.2.23.3f571c4cpkLsks) page.

**Note:**

-   Set the isLive parameter to true for the playback of live streams.
-   For more information about the playback parameters in ApsaraVideo for Media Processing, see [Play videos]().
-   For more information about the methods in ApsaraVideo VOD, see [Attributes and methods](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Attributes and methods.md).

## QR code for demos

Use DingTalk to scan the following QR code and experience the demos of ApsaraVideo Player.

![QR code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1249162261/p183624.png)

