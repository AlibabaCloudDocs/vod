# FAQ

This topic provides answers to commonly asked questions about ApsaraVideo Player for web.

## How do I choose a proper player?

ApsaraVideo Player supports the HTML5 player, Flash player, and adaptive streaming mode. We recommend that you use the adaptive streaming mode so that ApsaraVideo Player selects the most suitable player based on the type of your terminal and browser and the streaming protocol. For more information, see [online Settings](https://player.alicdn.com/aliplayer/setting/setting.html?spm=a2c4g.11186623.2.28.7224322cKcgNZj).

## How do I enable the HTML5 player?

You can enable the HTML5 player in the following ways:

-   Include the link of the JS file for enabling the HTML5 player in your HTML file.
-   Enable the adaptive streaming mode and set the useh5Prism parameter to **true**.

## How do I enable the Flash player?

You can enable the Flash player in the following ways:

-   Include the link of the JS file for enabling the Flash player in your HTML file.
-   Enable the adaptive streaming mode and set the useFlashPrism parameter to **true**.

## What is adaptive streaming?

In adaptive streaming mode, ApsaraVideo Player selects the most suitable player based on the type of your terminal and browser, the attributes you set, and the streaming protocol.

-   If the useFlashPrism parameter is set to true, and the Real-Time Messaging Protocol \(RTMP\) or HTTP-FLV protocol is used, the Flash player is used.
-   The HTML5 player is used to play videos on mobile devices.
-   If the useH5Prism parameter is set to true, the HTML5 player is used.
-   The HTML5 player is used to play MP4 videos on PCs.
-   If the web browser on your PC supports playback of .m3u8 videos, with or without the ApsaraVideo Player plug-in installed, the HTML5 player is used. Otherwise, the Flash player is used.
-   In other scenarios, the HTML5 player is used.

**Note:** The following basic principle is adopted in adaptive streaming mode: The HTML5 player has the highest priority. Unless you specify the Flash player, videos are played by the HTML5 player.

## Which browsers support the Flash player?

All browsers support the Flash player. The Flash player may be disabled by specific browsers and must be manually enabled. For more information about how to enable the Flash player in different browsers, visit the following websites:

-   [Enable the Flash player in Internet Explorer](https://answers.microsoft.com/zh-hans/ie/forum/ie11-iewindows8_1/windows-81ie/99696880-fbd9-4ac4-b43c-45fbb06f84e5?spm=a2c4g.11186623.2.29.31f8322cHvu6Mh)
-   [Enable the Flash player in Firefox](https://support.mozilla.org/zh-CN/kb/Flash%E6%8F%92%E4%BB%B6?spm=a2c4g.11186623.2.30.31f8322cQ8e7OY#w_uiiunigoce-flash)
-   [Enable the Flash player in Google Chrome](https://support.google.com/chrome/answer/6258784?spm=a2c4g.11186623.2.31.31f8322cR4t8u7)

## What can I do if I cannot drag the slider on the progress bar to a specified point in time for an MP4 or FLV video in the Flash player?

To drag the slider on the progress bar to a specified point in time for an MP4 or FLV video in the Flash player, make sure that the video data of the specified point in time can be obtained from Content Delivery Network \(CDN\). When the slider on the progress bar is dragged, the player sends a request containing the time range information to CDN. After CDN receives such a request, it returns the corresponding video data. To implement this feature, the following two conditions must be met:

-   Index information, such as the timestamp of an MP4 video and meta information of an FLV video, must be contained in the file header. After the player parses the index information, the player obtains data points of the time range specified by the drag operation and sends a request containing the time range information to CDN.
-   CDN supports requests that contain the time range or byte range information. For more information about how to enable this feature in the CDN console, see [Configure video seeking](/intl.en-US/Domain Management/Video-related settings/Configure video seeking.md).

## How do I disable automatic full-screen playback in WeChat for Android?

If you use an Android mobile phone, a video is played in full-screen mode in the Tencent browser or WeChat. By default, the Tencent browser hijacks the video tag to use the default player to play the video. In this case, the Dom element is overwritten. You cannot modify this default configuration of the Tencent browser. However, you can enable the immersive mode to prevent the Dom element from being overwritten. For more information, see [How do I enable the immersive mode for the HTML5 player](/intl.en-US/FAQ/How do I enable the immersive mode for the HTML5 player?.md).

## How do I enable the autoplay feature in WeChat for iOS?

To enable the autoplay feature in WeChat for iOS, use the following sample code:

```
<script src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>
<script>
function autoPlay() {
            wx.config({
                // The configuration information. The wx.ready method is available even if the configuration information is invalid.
                debug: false,
                appId: '',
                timestamp: 1,
                nonceStr: '',
                signature: '',
                jsApiList: []
            });
            wx.ready(function() {
                if(player)// The ApsaraVideo Player object that is created.
                {
                  player.play();
                }
            });
    };
    // Enable video autoplay on iOS mobile phones.
    autoPlay();
</script>
```

## How do I specify the start time for video playback in a player?

-   For the HTML5 player, use the following sample code:

    ```
    var seeked = false;
    player.on('canplaythrough',function  (e) {
      if(! seeked)
      {
        seeked = true;
        player.seek(100);
      }
    });
    ```

-   For the Flash player, use the following sample code:

    ```
    var seeked = false;
    player.on('loadedmetadata',function  (e) {
      if(! seeked)
      {
        seeked = true;
        player.seek(20);
      }
    });
    ```


## How do I disable the progress bar?

Go to the [Online Settings](https://player.alicdn.com/aliplayer/setting/setting.html?spm=a2c4g.11186623.2.34.31f8322c3rVxEt) page. On the Custom UI tab, set the skinLayout attributes: Clear all check boxes or the Seek Bar check box in the Status Bar Settings section. Example:

```
skinLayout: [
    {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
    {
      name: "H5Loading", align: "cc"
    },
    {
      name: "controlBar", align: "blabs", x: 0, y: 0,
      children: [
        //{name: "progress", align: "tlabs", x: 0, y: 0},
        {name: "playButton", align: "tl", x: 15, y: 26},
        {name: "timeDisplay", align: "tl", x: 10, y: 24},
        {name: "fullScreenButton", align: "tr", x: 20, y: 25},
        {name: "volume", align: "tr", x: 20, y: 25},
      ]
    }
  ]
```

## What can I do if the video ID and playAuth change?

-   You can call the `replayByVidAndPlayAuth` method to replace the existing HTML5 player. Example:

    ```
     player.replayByVidAndPlayAuth(newVid, newPlayAuth)
    ```

-   You must destroy the existing Flash player and create a new one based on the new video ID and playAuth. Example:

    ```
     // Destroy the existing player.
         FlashPlayer.dispose();
         $('#FlashPlayer').empty();
         // Create a player.
         FlashPlayer = new Aliplayer({
                id: 'FlashPlayer',
                autoplay: true,
                playsinline:true,
                vid: newVid,
                playauth: newPlayAuth,
                useFlashPrism:true
            });
    ```


## How do I obtain the playback time at regular intervals?

You can call the getCurrentTime method every second by using a timer to obtain the playback time. Clear the timer when the video playback is paused, fails, or ends. Example:

```
 var timer = null;
function getTime()
{
   var currentTime = player.getCurrentTime();
   //to do
   timer = setTimeout(getTime,1000);
}
// Clear the timer.
function clear()
{
   if(timer)
   {
      clearTimeout(timer);
      timer = null;
   }
}
player.on('ended',function  (e) {
  clear();
 });
player.on('pause',function  (e) {
  clear();
 });
player.on('error',function  (e) {
  clear();
 });
```

## How do I adjust the size and location of the play button in the HTML5 player?

-   Rewrite the CSS code for the play button. The following sample code narrows the button size to a half:

    ```
     .prism-player .prism-big-play-btn {
        width: 45px;
        height: 45px;
        background-size: 128px 256px;
    }
    ```

-   To adjust the location of the play button, set the values of the x and y fields in the bigPlayButton parameter of the skinLayout attributes. Example:

    ```
    skinLayout: [
        {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
        {
          name: "H5Loading", align: "cc"
        },
        {
          name: "controlBar", align: "blabs", x: 0, y: 0,
          children: [
            {name: "progress", align: "tlabs", x: 0, y: 0},
            {name: "playButton", align: "tl", x: 15, y: 26},
            {name: "timeDisplay", align: "tl", x: 10, y: 24},
            {name: "fullScreenButton", align: "tr", x: 20, y: 25},
            {name: "volume", align: "tr", x: 20, y: 25},
          ]
        }
      ]
    ```


## How do I disable automatic full-screen playback for my mobile phone?

-   If you use an iOS mobile phone, set the playsinline attribute to **true** to disable automatic full-screen playback.
-   If you use an Android mobile phone, a video is played in full-screen mode in the Tencent browser or WeChat. By default, the Tencent browser hijacks the video tag to use the default player to play the video. In this case, the Dom element is overwritten. You cannot modify this default configuration of the Tencent browser. However, you can enable the immersive mode to prevent the Dom element from being overwritten. For more information, see [How do I enable the immersive mode for the HTML5 player](/intl.en-US/FAQ/How do I enable the immersive mode for the HTML5 player?.md).

## How do I display the content in the highest available mode in Internet Explorer?

You must enable the highest available mode to display the content in Internet Explorer versions earlier than Internet Explorer 10. Example:

```
<meta http-equiv="x-ua-compatible" content="IE=edge" >
```

## What can I do if I receive a message indicating a cross-domain error when the Flash player plays streams based on M3U8 playlists?

Add a cross-domain policy file for the player to implement cross-domain access. You must add the cross-domain access permission to the crossdomain.xml file and add the file to the root directory of the domain to which the streaming URL belongs. Example:

```
<? xml version="1.0" encoding="UTF-8"? >
<cross-domain-policy>
    <allow-access-from domain="*"/>
    <allow-http-request-headers-from domain="*" headers="*" secure="false"/>
</cross-domain-policy>
```

## What can I do if the Flash player cannot display the thumbnail?

-   Check whether the thumbnail URL that is entered in the cover field is valid.
-   Check whether a valid crossdomain.xml file exists in the root directory of the domain to which the thumbnail URL entered in the cover field belongs.

