# How do I enable the immersive mode for the HTML5 player?

This topic answers the frequently asked question about how to enable the immersive mode for the HTML5 player.

ApsaraVideo Player V2.0.1 and later support video playback in immersive mode for the HTML5 player in Android-based WeChat mini programs. This feature is supported only for the Android-based Tencent X5 browser.

If the immersive mode is disabled in Android-based WeChat, videos are played in full screen and overwrite the elements in the HTML DOM.

## Properties of the immersive mode

|Property|Type|Description|
|--------|----|-----------|
|x5\_type|STRING|Enables the immersive mode. Set the value to h5.|
|x5\_fullscreen|BOOLEAN|Specifies whether to enter the full-screen mode of Tencent Browsing Service \(TBS\) during video playback. Set the value to true.|
|x5\_video\_position|STRING|The position of the video player on the screen. The default value is center. Valid values:-   top
-   center |
|x5\_orientation|STRING|The orientation of the video that is played by TBS. Valid values:-   landscape
-   portrait |

## Configurations of the immersive mode

-   **Configure the immersive mode for video playback in windowed mode**

    To enable the immersive mode for video playback in windowed mode, set the x5\_type property to h5 and the playsinline property to false.

    Use the x5\_video\_position property to specify the position of the video player on the screen. If you want the video player to appear at the center of the screen, set the value of this property to center. If you want the video player to appear at the top of the screen, set the value of this property to top. The default value is center.

    For more information, download the [HTML5 demo](https://github.com/alilmq/h5demo).

    ![](../images/p190051.png)

-   Configure the immersive mode for video playback in full-screen mode

    To enable the immersive mode, set the x5\_type property to h5 and the playsinline property to false. To enable the full-screen mode, set the x5\_fullscreen property to true. You do not need to set the x5\_video\_position property for full-screen video playback.

    By default, a video that is playing in full-screen mode fills the whole screen. If you do not want the video to fill the whole screen, you can change the value of the object-fit property. For example, you can change the value to contain.

    ```
    video {
        object-fit: contain !important;
        }            
    ```

    For more information, download the [HTML5 live demo](https://github.com/alilmq/h5livedemo).

    ![](../images/p190052.png)


Suggestions for configuring the immersive mode

When you configure the immersive mode, take note of the following suggestions:

-   You can listen to the resize event, so that the viewport can be automatically resized when videos are playing.
-   Make sure that interactive elements, such as pop-up windows and bullet comments, are inside the video area during video playback.
-   For a live video in full-screen mode, we recommend that you do not put interactive elements at the top of the video.
-   For a video that involves interaction in full-screen mode, you can set the size of the video area to that of the viewport.

## More configurations

-   Layout adjustment during the entering or exit of the immersive mode

    In most cases, layout adjustment is necessary when you enter or exit the immersive mode. To meet this requirement, you can define logic for layout adjustment in the events that are used to enter or exit the immersive mode. For example, you can define the logic to switch to or out of the full-screen mode or change the position of an element.

    The event that is used to enter the immersive mode is x5requestFullScreen.

    The event that is used to exit the immersive mode is x5cancelFullScreen.

-   More custom configurations

    If the valid values of the x\_video\_position property cannot meet your requirements, you can use the object-fit and object-position properties to flexibly specify the position of the video player.

-   object-fit property

    object-fit: a CSS property that specifies how the content of a replaced element is fitted to the box that is established by the height and width of the element.

    Valid values:

    -   fill
    -   contain
    -   cover
    -   none
    -   scale-down
    The following figure shows the display effects of the preceding values.

    ![](../images/p190053.png)

    The following code provides an example on how to use the object-fit property:

    ```
     video {
        object-fit: contain !important;
        }            
    ```

-   object-position property

    object-position: a CSS property that specifies the alignment of the content of a replaced element within the element box. This property is similar to the background-position property.

    The following code provides an example on how to use the object-fit property:

    ```
    img {
       width: 300px;
       height: 250px;
       border: 1px solid black;
       background-color: silver;
       margin-right: 1em;
       object-fit: none;
    }
    
    #object-position-1 {
      object-position: 10px;
    }
    
    #object-position-2 {
      object-position: 100% 10%;
    }       
    ```

    The following figure shows different display effects based on different values of the object-position property.

    ![](../images/p190054.png)

-   Height adjustment for the player container

    After you set the position of the video player, the control bar may not be displayed in the lower part of the screen. In this case, you can adjust the height of the player container by subscribing to the resize and requestFullScreen events.

    ```
    var setLayout = function()
    {    
        // Set a height for the player container.
        var height ; // Set a height based on actual needs.
        player.el().style.height = height;
    }
    
    window.onresize = function(){
        setLayout();
    }
    
    player.on("requestFullScreen", function(){
        setLayout();
    });  
    ```


