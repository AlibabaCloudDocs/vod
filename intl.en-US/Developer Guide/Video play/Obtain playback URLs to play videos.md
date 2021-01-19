Obtain playback URLs to play videos 
========================================================

ApsaraVideo VOD allows you to play audio and video files by using playback URLs. You can obtain playback URLs from event notifications that are sent when transcoding is complete or by using the API or SDK that is used to obtain playback URLs. This topic describes the process, method to obtain the URL, and instructions of playback.

Playback process 
-------------------------------------

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2210401161/p178253.png)
**Notice**

The server must have the AccessKey of a RAM user and must be granted the playback permission. For more information, see [Overview](/intl.en-US/Developer Guide/Access authorization/Overview.md).

If you use ApsaraVideo Player, see [Use ApsaraVideo Player](/intl.en-US/Developer Guide/Video play/Use ApsaraVideo Player SDK.md).

Obtain the playback URL 
--------------------------------------------

You can obtain playback URLs from event notifications or by using the API or SDK that is used to obtain playback URLs.

* Event notification

  You can obtain the playback URL by receiving the [StreamTranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/StreamTranscodeComplete.md) or [TranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/TranscodeComplete.md) event notification. After you save the event notification to your own server, you can access your own server to obtain the stored playback URL when you play audio and video files.

  **Usage notes:** 
  * The playback URLs that are obtained from event notifications are `fixed URLs`. If [URL authentication](/intl.en-US/Developer Guide/Video security/URL signing.md) is enabled, you must generate playback URLs that have authentication keys (auth_key). If you do not generate the playback URLs, video playback fails.

    
  
  * If the old domain name is disabled or deleted, replace the domain name in the saved playback URL with a new domain name. If you do not replace the domain name, video playback fails.

    
  
  * If video encryption is configured, players must decrypt the returned playback URL to play videos.

    
  

  




<!-- -->

* API/SDK

  To obtain playback URLs by calling the [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md) operation or by using the ApsaraVideo VOD API or SDK, you must keep the video IDs returned when you upload audio or video files.

  **Call methods:** 
  * We recommend that you use a server SDK to obtain media asset information by calling the API operations. This method is simple and efficient. For more information, see [Usage notes](/intl.en-US/Server SDK Reference/Usage notes.md). For more information about APIs, see SDK examples for each API operation.

    
  
  * For more information about how to generate HTTP or HTTPS requests, see [Common parameters](/intl.en-US/API Reference/Calling methods/Common parameters.md) and [Examples](/intl.en-US/API Reference/Calling methods/Call Examples.md).

    
  

  

  **Limits:** 
  * By default, the GetPlayInfo operation returns only the latest transcoded stream in each definition and format to ensure that the latest transcoded stream is played each time. When you call the [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md) operation, you can set `ResultType` to `Multiple` to obtain the playback URLs of all the transcoded streams of the audio or video.

    
  
  * If videos in [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md) mode are encrypted, only ApsaraVideo Player SDK can play the videos. By default, the system does not return the playback URL of a stream that is encrypted in Alibaba Cloud video encryption mode when you call the GetPlayInfo operation. This ensures video security. You can set `ResultType` to `Multiple` to obtain the playback URLs of all the transcoded streams.

    
  
  * By default, if videos in [HLS Encryption](/intl.en-US/Developer Guide/Video security/Standard HLS encryption.md) mode are encrypted, the system preferentially returns the playback URL of a stream that is transcoded in HLS Encryption mode.

    
  

  




Instructions 
---------------------------------

You can obtain and send the playback URL of a video to your player.

* ApsaraVideo Player can directly play a video by using a playback URL. For more information, see [Use ApsaraVideo Player](/intl.en-US/Developer Guide/Video play/Use ApsaraVideo Player SDK.md).

  

* You can also use the player that is built in the system, an open source player, or your self-developed player.

  



