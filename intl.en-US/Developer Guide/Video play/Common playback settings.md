Common playback settings 
=============================================

When you play videos in ApsaraVideo VOD, you can select different playback URL types based on the playback scenarios. You can configure domain names, transcoding templates, and playback to control the playback URL type. This topic describes the common playback settings.

Configure domain names 
-------------------------------------------

* Add a domain name

  * Configure a domain name. Make sure that the domain name that you want to use in ApsaraVideo VOD is registered. For more information, see [Domain verification](/intl.en-US/User Guide/Domain management/Domain verification.md).

    
  
  * Bind a CNAME record to the domain name. If you do not perform this operation, video playback fails. For more information, see [Configure a CNAME record in Alibaba Cloud DNS](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure a CNAME record in Alibaba Cloud DNS.md). You can also use [Xinnet](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure a CNAME record on Xinnet.md) or [DNSPod](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure a CNAME record on DNSPod.md) to bind a CNAME record to the domain name.

    
  
  * Configure a domain name. For more information, see [Add a domain name](/intl.en-US/User Guide/Domain management/Add a domain name.md).

    
  

  




<!-- -->

* URL authentication

  * You can set the `AuthTimeout` parameter to specify an expiration time for CDN URLs. For more information, see the "URL expiration time" section of the [URL authentication](/intl.en-US/Developer Guide/Video security/URL signing.md) topic.

    
  
  * CDN reauthentication:

    * If CDN reauthentication is enabled, you can set the `ReAuthInfo` parameter to add the uid and rand parameters to CDN authentication parameters. For more information, see the "ReAuthInfo" section of the [Request parameters](/intl.en-US/API Reference/Appendix/Request parameters.md) topic.

      
    
    * If CDN reauthentication is disabled, you can set the `rand` parameter in the `ReAuthInfo` parameter to ensure that a different URL is generated each time. For example, you can set the rand parameter to UUID. For more information, see the "ReAuthInfo" section of the [Request parameters](/intl.en-US/API Reference/Appendix/Request parameters.md) topic.

      
    

    
  

  

* Select multiple domain names

  If multiple domain names are configured for your origin, you can set `PlayDomain` in the `PlayConfig` parameter to specify the CDN domain name included in playback URLs. For more information, see the "PlayConfig" section of the [Request parameters](/intl.en-US/API Reference/Appendix/Request parameters.md) topic.
  

* HTTPS secure acceleration

  By default, the image URLs and playback URLs returned by the API are HTTP URLs. To obtain HTTPS URLs, you can enable HTTPS secure acceleration for a CDN domain name in ApsaraVideo VOD. For more information, see [Enable HTTPS secure acceleration](/intl.en-US/User Guide/Domain management/Set HTTPS security acceleration/Enable HTTPS secure acceleration.md).
  




Configure transcoding templates 
----------------------------------------------------
ApsaraVideo VOD allows you to choose whether to transcode the uploaded media files.
* If media files are transcoded, the playback URLs are the playback URLs of transcoded streams. The format of a playback URL and the definition, encryption, and watermark ID parameters in the playback URL base on your transcoding settings.


* If media files are not transcoded, the playback URLs are the playback URLs of the uploaded mezzanine files for playback in original quality.



For more information, see the "[Transcoding template](/intl.en-US/Developer Guide/Media processing/Audio and video transcoding.md)" section of the Audio and video playback topic. {#h2--div-id-domain-div-2}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Configure playback 
---------------------------------------

The playback service supports the following three playback modes:

* Preview in the console: You do not need to configure this mode.

  

* Playback URL: You can call the [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md) operation to obtain different playback URLs based on different playback settings.

  

* Player SDK: You can configure player settings. The player automatically filters the playback URL to play a video.

  




**Playback operation settings:** 

ApsaraVideo VOD allows you to configure the following parameters of the [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md) operation to obtain required playback URLs in different playback scenarios.

* Definition

  `Definition`: The GetPlayInfo operation allows you to specify multiple definitions at a time, which enables you to switch the definition based on the network conditions. If you do not set this parameter, the GetPlayInfo operation returns the playback URLs of video streams in all definitions for the specified video.
  

* Formats

  `Formats`: The container format of a transcoded stream. Only the `MP4`, `MP3`, and `M3U8` formats are supported. The GetPlayInfo operation allows you to specify multiple formats at a time, which enables you to select a video stream of the appropriate format based on the playback scenario.
  

* Stream type

  The `stream type`. Valid values: video and audio. You can select a stream type based on the playback scenario.
  

* Output type

  `OutputType`:
  * By default, if no CDN domain name is configured, the GetPlayInfo operation returns OSS URLs.

    
  
  * By default, if a CDN domain name is configured, the GetPlayInfo operation returns CDN URLs.

    
  
  * You can set the `OutputType` parameter to obtain the OSS back-to-origin URLs or CDN URLs.

    
  

  

* Result type

  `ResultType`. By default, ApsaraVideo VOD provides only one playback URL for each definition and format. If you submit a media transcoding job for a video that is transcoded, multiple playback URLs are available for each definition and format. By default, the GetPlayInfo operation returns only the latest transcoded stream in each definition and format. This ensures that the latest transcoded stream is played each time. To obtain the playback URLs of all the transcoded streams, you can set the `ResultType` parameter to `Multiple`.
  **Notice**

  If the `ResultType` parameter is set to `Multiple`, the GetPlayInfo operation returns a maximum of 100 playback URLs even if a video has more than 100 playback URLs.
  




**Player settings:** 

ApsaraVideo Player SDKs can automatically obtain playback URLs based on playback credentials. ApsaraVideo Player SDKs for Web (HTML5 and Flash), Android, and iOS are provided. The following section describes the player settings supported for each terminal.

* ApsaraVideo Player SDK for Web

  * For an HTML5 player that is integrated with ApsaraVideo Player SDK, you can configure the `mediaType` parameter to specify the output stream type, the `format` parameter to specify the output file format, and the `definition` parameter to specify the definition. For more information, see [Feature instructions](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Features.md).

    
  
  * A Flash player that integrates ApsaraVideo Player SDK can play only video files. For a Flash player that is integrated with ApsaraVideo Player SDK, you can configure the `mediaType` parameter to specify the output stream type and the `format` parameter to specify the output file format.

    
  

  




<!-- -->

* ApsaraVideo Player SDK for iOS

  You can configure the `format` parameter to specify the output file format and the `quality` parameter to specify the expected definition.
  

* ApsaraVideo Player SDK for Android

  You can configure the `format` parameter to specify the output file format and the `quality` parameter to specify the expected definition.
  



