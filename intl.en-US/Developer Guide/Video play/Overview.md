Overview 
=============================

ApsaraVideo VOD allows you to play audio and video files. You can preview audio and video files in the ApsaraVideo VOD console. You can also integrate ApsaraVideo Player SDK and third-party players to play audio and video files. This topic describes the overall process, preparations, prerequisites, playback methods, playback URLs, and playback security of the audio and video playback.

Overview 
-----------------------------

ApsaraVideo VOD allows you to play the following types of audio and video files:

* Transcoded stream files: If you enable **transcoding** when you upload audio and video files, transcoded stream files are generated after the upload.

  

* Mezzanine files: If you disable **transcoding** when you upload audio and video files, the uploaded mezzanine files are played in original quality.

  




You can use the one of the following methods to play audio and video files:

* [ApsaraVideo VOD console](https://vod.console.aliyun.com/#/media/video/list) (for preview). For more information, see [Media asset management](/intl.en-US/User Guide/Media library/Manage media assets.md).

  

* Integrate ApsaraVideo Player SDK. For more information, see [Product description of Player SDK](/intl.en-US/New Player SDK/Overview.md).

  

* Integrate thrid-party players.

  




You can use one of the following methods to obtain the playback URLs:

* Directly obtain playback URLs: View the event notification after transcoding is complete or call the [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md) operation.

  

* Automatically obtain playback URLs based on playback credentials: Use ApsaraVideo Player SDK by calling the [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md) operation to obtain playback credentials. ApsaraVideo Player SDK can automatically obtain playback URLs based on playback credentials.

  




Preparations 
---------------------------------

* Configure a domain name for CDN. Make sure that the domain name that you want to use in ApsaraVideo VOD is registered. For more information, see [Domain verification](/intl.en-US/User Guide/Domain management/Domain verification.md).

  

* Bind a CNAME record to the domain name. If this operation is not performed, video playback fails. For more information, see [Configure a CNAME record in Alibaba Cloud DNS](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure a CNAME record in Alibaba Cloud DNS.md). You can also use [Xinnet](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure a CNAME record on Xinnet.md) or [DNSPod](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure a CNAME record on DNSPod.md) to bind a CNAME record to the domain name.

  

* Confirm the transcoding configuration. ApsaraVideo VOD can **transcode uploaded files** or **does not transcode** uploaded files. For more information, see [Audio and video transcoding](/intl.en-US/Developer Guide/Media processing/Audio and video transcoding.md).

  

* Confirm the security configuration. ApsaraVideo VOD protects your video content by using a variety of measures, which include **access control** **, URL authentication** , **CDN reauthentication** , **video encryption** , and **secure download** . The security configuration determines whether a video can be played. For more information, see [Video security](/intl.en-US/Developer Guide/Video security/Overview.md).

  




Prerequisites 
----------------------------------

* **Status** 

  When audio or videos are produced, processed, or distributed, the status of the audio and video changes. The video status is a key condition that determines whether videos can be played. For more information about the video status, see [Status](/intl.en-US/API Reference/Appendix/Basic data types.md).
  

* **Judgment conditions** 

  * Only videos whose `Status` is **Normal** can be played. You can obtain the playback URLs of these videos by using the API or SDK.

    
  
  * Videos whose `Status` is **Checking** or **Blocked** can be played only in the ApsaraVideo VOD console or from IP addresses that have been added to review security groups. You can add IP addresses to [review security groups](/intl.en-US/Developer Guide/Media review/Security IP address preview.md) by using the API or SDK.

    
  

  

* **Judgment methods** 

  After you upload a video, the video is not immediately ready for playback. ApsaraVideo VOD must confirm that the video is completely received. You can determine whether videos are ready for playback based on **event notifications** .
  * You can play a video or audio that does not need to be transcoded when you receive a [FileUploadComplete](/intl.en-US/Developer Guide/Event notification/Events/FileUploadComplete.md) event notification. You can call the [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md) operation to obtain the playback URL.

    
  
  * You can play a video or audio that must be transcoded when you receive a [StreamTranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/StreamTranscodeComplete.md) event notification. To ensure that streams in all definitions can be obtained, wait until you receive a[TranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/TranscodeComplete.md) event notification.

    
  

  




Playback mode 
----------------------------------

* Use the ApsaraVideo VOD console to preview videos

  * You can preview a video after you choose [Video](https://vod.console.aliyun.com/#/media/video/list)[and Audio](https://vod.console.aliyun.com/#/media/video/list) in the ApsaraVideo VOD console. An encrypted stream of the video is preferentially played.

    
  
  * You can select a stream that you want to preview after you click **Video and Audio** in the ApsaraVideo VOD console. On the Video and Audio page, click Manage in the Actions column. Click the Video URL tab. To ensure video security, ApsaraVideo VOD allows you to preview only unencrypted streams.

    
  

  




<!-- -->

* Integrate ApsaraVideo Player SDK

  * You can obtain and transmit the playback credential of a video from the ApsaraVideo VOD server to your player. This method provides higher security. For more information, see [Use playback credentials for playback](/intl.en-US/Developer Guide/Video play/Use playback credentials to play videos.md).

    
  
  * ApsaraVideo Player can play a video from a playback URL. Therefore, you can send the obtained playback URL to ApsaraVideo Player for playback. For more information, see [Use playback credentials for playback](/intl.en-US/Developer Guide/Video play/Obtain playback URLs to play videos.md).

    
  

  




<!-- -->

* Integrate third-party players

  * You can integrate a third-party player to [obtain playback URLs](/intl.en-US/Developer Guide/Video play/Obtain playback URLs to play videos.md) for playback.

    
  
  * You can obtain the playback URL of a video and send the URL to your player. This method is convenient, but requires you to perform development operations such as converting the definition and handling exceptions.

    
  

  




Playback URLs 
----------------------------------

* Configure a domain name for CDN

  If a domain name for CDN is configured in the ApsaraVideo VOD console, playback URLs are file URLs of CDN. You can view playback URLs on the Video and Audio page in the ApsaraVideo VOD console. after you click Manage in the Actions column and click the Video URL tab. Playback URLs are classified into fixed URLs and dynamic URLs, which is based on whether URL authentication is enabled. For more information about how to enable and configure URL authentication, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md).
  * Fixed URLs

    are URLs that do not contain authentication information (`auth_key`). They are generated when URL authentication is disabled. Fixed URLs are permanently valid and are suitable for scenarios that have low security requirements. By default, URL authentication is disabled for a domain name when URL authentication is configured in the ApsaraVideo VOD console.
    
  
  * Dynamic URLs

    are dynamically generated and expire after a specific period of time. They are suitable for scenarios that have high security requirements. The default validity period of a dynamic URL is determined by the `Default Validity Period` parameter that you set when you enable URL authentication. You can set the validity period when the [playback URL is generated](/intl.en-US/Developer Guide/Video security/URL authentication.md) or [playback URL is obtained](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md). When you access a playback URL after the URL expires, CDN returns an `HTTP 403` status code.

    Example:

        http://vod.example.com/video/aliyun-sample.mp4?auth_key=1500523200-0-0-80cd3862d699b7118eed99103f2a3a4f

    
    **Note**

    In this example, the numeral before the first hyphen (-) in the value of the auth_key parameter is 1500523200, which indicates the time 12:00:00 on July 20, 2017. If the **Default Validity Period** parameter is set to 60 minutes, this URL expires at 13:00:00 on July 20, 2017.
    
  

  




<!-- -->

* No domain name for CDN is configured

  * If no domain name for CDN is configured, playback URLs are object URLs of OSS and URL authentication cannot be used. In this case, OSS authentication information is generated by default. For more information, see [Generate a signed URL](/intl.en-US/API Reference/Access control/Generate a signed URL.md) in the OSS documentation. You can still use the `AuthTimeout` parameter to specify the expiration time of OSS URLs when you call the [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md) operation. However, you cannot customize authentication information based on the AccessKey pair.

    
  
  * If you set the permissions to **Public Read and Private Write** for the `bucket` allocated by ApsaraVideo VOD on the **[Storage](https://vod.console.aliyun.com/#/storage/list)** page, OSS authentication information is ignored. For more information, see [Manage VOD resources](/intl.en-US/User Guide/Global settings/Manage VOD resources.md). In this case, playback URLs are permanently valid, which creates the risks of hotlinking and illegal download. We recommend that you set the permissions to **Private Read and Write** for the `bucket` allocated by ApsaraVideo VOD.

    
  

  




For more information about common playback URL settings, see [Common playback settings](/intl.en-US/Developer Guide/Video play/Common playback settings.md).

Playback security (limits on playback and download) 
------------------------------------------------------------------------

* Video security

  ApsaraVideo VOD protects your video content by using a variety of measures, which include [access control](/intl.en-US/Developer Guide/Video security/Access control.md), [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md), and video encryption. Video encryption includes [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md) and [HLS Encryption](/intl.en-US/Developer Guide/Video security/HLS Encryption.md). For more information, see [Overview](/intl.en-US/Developer Guide/Video security/Overview.md).
  

* Account security

  To ensure the security of your account, do not use the AccessKey pair of your Alibaba Cloud account or a RAM user on the clients, especially web clients to connect to ApsaraVideo VOD. For more information, see [Overview](/intl.en-US/Developer Guide/Access authorization/Overview.md).
  



