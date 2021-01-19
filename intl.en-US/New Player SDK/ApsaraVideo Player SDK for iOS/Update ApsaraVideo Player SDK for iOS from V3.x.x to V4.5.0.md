Update ApsaraVideo Player SDK for iOS from V3.x.x to V4.5.0 
================================================================================

This topic describes the changes of ApsaraVideo Player SDK V4.5.0 for iOS compared with V3.x.x. This topic also describes the precautions and procedure for updating ApsaraVideo Player SDK for iOS from V3.x.x to V4.5.0.

Unified player 
-----------------------------------

ApsaraVideo Player SDK V3.x.x for iOS provides ApsaraVideo Player Basic and ApsaraVideo Player Pro.

* AlivcMediaPlayer

  

* AliyunVodPlayer

  




ApsaraVideo Player Basic plays videos from specified URLs. ApsaraVideo Player Pro plays videos with specified video IDs (VIDs). In ApsaraVideo Player SDK V4.5.0 for iOS, ApsaraVideo Player Basic and ApsaraVideo Player Pro are integrated. The AliPlayer class is used to play both videos from specified URLs and videos with specified VIDs.

Changes in dependent frameworks 
----------------------------------------------------

* ApsaraVideo Player SDK V3.x.x for iOS contains the following dependent frameworks:

  * AliyunPlayerSDK.framework

    
  
  * AliyunVodPlayerSDK.framework

    
  
  * AliThirdparty.framework

    
  
  * The SDK also contains a bundle package AliyunLanguageSource.bundle.

    
  

  




<!-- -->

* ApsaraVideo Player SDK V4.5.0 for iOS contains the following dependent frameworks:

  * AliyunPlayer.framework

    
  
  * AliyunMediaDownloader.framework

    
  
  * AlivcConan.framework and alivcffmpeg.framework

    
  

  




Changes in class names and methods 
-------------------------------------------------------

In ApsaraVideo Player SDK V4.5.0 for iOS, some class names are changed, and new features and callbacks are added. Some methods in ApsaraVideo Player SDK V3.x.x for iOS are removed.

Update practices 
-------------------------------------

The following section describes how to update ApsaraVideo Player SDK for iOS from V3.4.10 to V4.5.0.
**Note**

The procedure for updating ApsaraVideo Player SDK for iOS from V3.x.x to V4.x.x is similar. The following example shows how to update ApsaraVideo Player Pro SDK that uses the AliyunVodPlayer class from V3.4.10 to V4.5.0.

1. Integrate frameworks.

   In the Embedded Binaries section of Xcode, replace specific frameworks of V3.4.10 with frameworks of V4.5.0. For more information, see [Integration](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/Integration.md).
   

2. Modify code.

   After you replace the frameworks, an error occurs when you start to compile the project. You must use classes and methods that are provided by ApsaraVideo Player SDK V4.5.0 for iOS to resolve the error. Compared with V3.4.10, class names and method names are changed in V4.5.0. You must pay attention to the following changes:
   1. Referenced header files: Change the referenced framework header file. Example:

          #import <AliyunVodPlayerSDK/AliyunVodPlayerSDK.h>
          is changed to
          #import <AliyunPlayer/AliyunPlayer.h>

      

      
   
   2. Player class name: ApsaraVideo Player SDK V3.4.10 for iOS provides the AliyunVodPlayer class for you to define a player object. ApsaraVideo Player SDK V4.5.0 for iOS provides the AliPlayer class for you to define a player object. Example:

          self.player = [[AliyunVodPlayer alloc] init];
          is changed to
          self.player = [[AliPlayer alloc] init];

      

      
   
   3. Delegate methods: In ApsaraVideo Player SDK V3.4.10 for iOS, the delegate class is `AliyunVodPlayerDelegate`. In ApsaraVideo Player SDK V4.5.0 for iOS, the delegate class is `AVPDelegate`. The effects of specific delegate methods remain unchanged. Only names are changed. The following code shows an example of the `onEventCallback` method:

          - (void)vodPlayer:(AliyunVodPlayer *)vodPlayer onEventCallback:(AliyunVodPlayerEvent)event ;
          is changed to
          -(void)onPlayerEvent:(AliPlayer*)player eventType:(AVPEventType)eventType;

      
      **Note**

      Event types of members basically remain unchanged except for specific tiny differences. For more information, see [API operations](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/API operations.md).
      
   
   4. Changes in listeners.

      The following table describes the changes of the delegate methods in ApsaraVideo Player SDK V3.4.10 for iOS.
      

      |                   Method                   |                          Feature                          |                         Change                          |
      |--------------------------------------------|-----------------------------------------------------------|---------------------------------------------------------|
      | onEventCallback                            | Indicates a playback event.                               | onPlayerEvent                                           |
      | playBackErrorModel                         | Indicates a playback error.                               | onError                                                 |
      | willSwitchToQuality                        | Indicates that the video resolution will be switched.     | Deleted                                                 |
      | didSwitchToQuality                         | Indicates that the video resolution is switched.          | onTrackChanged                                          |
      | failSwitchToQuality                        | Indicates that the video resolution fails to be switched. | Deleted                                                 |
      | onCircleStartWithVodPlayer                 | Indicates that the player starts loop playback.           | AVPEventLoopingStart method of the onPlayerEvent member |
      | onTimeExpiredErrorWithVodPlayer            | Indicates a timeout error.                                | Deleted                                                 |
      | vodPlayerPlaybackAddressExpiredWithVideoId | Indicates that the playback URL is about to expire.       | Deleted                                                 |

      

      The following table describes the new delegate methods in ApsaraVideo Player SDK V4.5.0 for iOS.
      

      |            Method             |                     Feature                      |
      |-------------------------------|--------------------------------------------------|
      | onPlayerEvent:eventWithString | Indicates specific playback events.              |
      | onVideoSizeChanged            | Indicates that the video resolution is switched. |
      | onCurrentPositionUpdate       | Indicates the playback progress.                 |
      | onBufferedPositionUpdate      | Indicates the caching progress.                  |
      | onLoadingProgress             | Indicates the buffering progress.                |
      | onTrackReady                  | Indicates that various bitrates are available.   |
      | onSubtitleShow                | Indicates that subtitles are displayed.          |
      | onSubtitleHide                | Indicates that subtitles are hidden.             |
      | onGetThumbnailSuc             | Indicates that thumbnails are obtained.          |
      | onGetThumbnailFailed          | Indicates that thumbnails fail to be obtained.   |
      | onPlayerStatusChanged         | Indicates that the playback status changes.      |
      | onCaptureScreen               | Indicates that a snapshot is captured.           |

      
   

   

3. Set the playback source.

   ApsaraVideo Player SDK V3.4.10 for iOS calls the `prepareWithVid` method to set parameters for the playback source, and then automatically prepares the player. In ApsaraVideo Player SDK V4.5.0 for iOS, you must call the `setSource` method to set parameters for the playback source and then call the prepare method to prepare the player. Example:

       /**
        @brief Play videos based on the URL.
        @param source The playback source type is AVPUrlSource.
        @see AVPUrlSource
        */
       - (void)setUrlSource:(AVPUrlSource*)source;
       /**
        @brief Play videos based on the VID and Security Token Service (STS) token.
        @param source The playback source type is AVPVidStsSource.
        @see AVPVidStsSource
        */
       - (void)setStsSource:(AVPVidStsSource*)source;
       /**
        @brief Play videos based on the VID in ApsaraVideo for Media Processing.
        @param source The playback source type is AVPVidMpsSource.
        @see AVPVidMpsSource
        */
       - (void)setMpsSource:(AVPVidMpsSource*)source;
       /**
        @brief Play videos based on the VID and playAuth.
        @param source The playback source type is AVPVidAuthSource.
        @see AVPVidAuthSource
        */
       - (void)setAuthSource:(AVPVidAuthSource*)source;

   
   **Note**

   For live streaming time shifting, ApsaraVideo Player SDK V4.5.0 for iOS provides a new class AVPLiveTimeShift and adds methods for live streaming time shifting in V3.x.x to this class. You can call these methods as in V3.x.x.
   

4. Obtain the video and audio information.

   After the player is prepared, you must obtain the VID information. In ApsaraVideo Player SDK V3.x.x for iOS, you can call the AliyunVodPlayerVideo method to obtain the information. The following code shows how to obtain the information in ApsaraVideo Player SDK V4.5.0 for iOS:

       if (event == AliyunVodPlayerEventPrepareDone) {
               AliyunVodPlayerVideo *videoModel = [self.vodPlayer getAliyunMediaInfo];
       }
       is changed to
       case AVPEventPrepareDone: 
           AVPTrackInfo *videoInfo = [self.player getCurrentTrack:AVPTRACK_TYPE_VIDEO];

   
   **Note**

   AVPTrackInfo contains information about the bitrate, playback URL, and VID. For more information, see [API operations](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/API operations.md).
   

5. Set playback parameters.

   In ApsaraVideo Player SDK V3.x.x for iOS, you can call specific methods to set parameters. ApsaraVideo Player SDK V4.5.0 for iOS encapsulates these methods to the `config` method. You can call the GetConfig method to obtain player parameters, and call the SetConfig method to modify player parameters.
   

   |      Setting       |                 Feature                 |                        Change                         |
   |--------------------|-----------------------------------------|-------------------------------------------------------|
   | referer            | Sets the referer.                       | The referer parameter of the AVPConfig method.        |
   | timeout            | Indicates a timeout error.              | The networkTimeout parameter of the AVPConfig method. |
   | dropBufferDuration | Indicates the threshold of lost frames. | The maxDelayTime parameter of the AVPConfig method.   |

   
   **Note**

   ApsaraVideo Player SDK V4.5.0 for iOS provides new config methods to help you manage the player. For more information, see [API operations](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/API operations.md).
   

6. Set playback control.

   In ApsaraVideo Player SDK V4.5.0 for iOS, the control methods, such as pause, start, and stop, remain unchanged.

   The following methods for playback control are added:
   * reload: You can call the reload method to send the online request again if a network error occurs.

     
   
   * redraw: You can call the redraw method to refresh the view if the window changes.

     
   

   




Documents of ApsaraVideo Player SDK V3.x.x for iOS 
-----------------------------------------------------------------------

[ApsaraVideo Player Basic](https://help.aliyun.com/document_detail/61431.html)

[ApsaraVideo Player Pro](https://help.aliyun.com/document_detail/61668.html)

[API operations for ApsaraVideo Player Basic](https://help.aliyun.com/document_detail/61899.html)

[API operations for ApsaraVideo Player Pro](https://help.aliyun.com/document_detail/61900.html)
