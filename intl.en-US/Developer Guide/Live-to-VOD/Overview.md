Overview 
=============================

The Live to VOD feature synchronously records live streams into on-demand videos and supports various operations. The operations include media asset management, media processing (transcoding and AI-based processing such as content moderation and intelligent thumbnail), content production (online editing), and CDN acceleration. You can configure Live to VOD as an automatic workflow in the ApsaraVideo VOD or ApsaraVideo Live console or flexibly start live-to-VOD processing by using the API or SDK. This topic describes the overall architecture, benefits, access methods, and query methods of the Live to VOD service.

Architecture 
---------------------------------

The following figure shows the overall architecture of Live to VOD.![Architecture](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1655401161/p183806.png)

Benefits 
-----------------------------

Compared with storing recorded videos in OSS, storing recorded videos in ApsaraVideo VOD has the following benefits:

* One-stop video production: ApsaraVideo VOD supports automatic transcoding and CDN-based content delivery for recorded videos, which enables a one-stop video production process.

  

* Various media asset management capabilities: ApsaraVideo VOD provides various media asset management capabilities that you can use to mange recorded videos.

  

* Powerful content production capabilities: You can directly edit recorded videos online by using the online editing service of ApsaraVideo VOD, which eliminates the need for traditional production processes.

  

* Media processing capabilities such as automated review and AI: Based on powerful AI capabilities, ApsaraVideo VOD can perform operations such as automated review, intelligent thumbnailing, and media fingerprinting on recorded videos.

  




Procedure 
------------------------------

ApsaraVideo Live records live streams and stores the recorded videos in ApsaraVideo VOD for management.

Under the same CDN domain name of ApsaraVideo Live, live-to-VOD configurations of live streams are distinguished by their `AppName` and `StreamName` parameters. All live streams with the same `application name` and `stream name` use the same live-to-VOD configuration specified for the `application name` and `stream name`. 

1. Activate ApsaraVideo VOD For more information, see [Get started with ApsaraVideo VOD](/intl.en-US/Quick Start/Get started with ApsaraVideo VOD.md).

   

2. On the [Add Transcoding Template Group](https://vod.console.aliyun.com/#/settings/transcode/add) page of the ApsaraVideo VOD console, create the transcoding template required to process videos recorded by ApsaraVideo Live. For more information, see [Audio and video transcoding](/intl.en-US/Developer Guide/Media processing/Audio and video transcoding.md).

   

3. Activate ApsaraVideo Live. For more information, see [Activate ApsaraVideo LiveActivate](/intl.en-US/Pricing/Billing-related operations/Activate ApsaraVideo Live and purchase resource plans.md).

   

4. On the [Domain Management](https://live.console.aliyun.com//domain/list#/domain/list) page of the ApsaraVideo Live console, specify the live-to-VOD configuration. Select the template that you created earlier as the recording and transcoding template, as shown in the following figure. For more information, see [Store live recordings in ApsaraVideo VOD](/intl.en-US/Console Guide/Domain Names/Recording management/Store live recordings in ApsaraVideo VOD.md).

   You can also add recording configurations by calling the AddLiveRecordVodConfig operation. For more information, see [AddLiveRecordVodConfig](/intl.en-US/API Reference/Store live recordings to ApsaraVideo VOD/AddLiveRecordVodConfig.md).
   **Note**

   For more information about transcoding templates and production templates in the live-to-VOD configuration, see [FAQ about Live to VOD](/intl.en-US/Developer Guide/Live-to-VOD/FAQ about Live to VOD.md).
   

5. After the preceding preparations, you can start to use the Live to VOD feature.

   **Note**

   When a stream is interrupted, the system waits for 3 minutes before it stops recording the stream. This can avoid unexpected truncation of recorded videos caused by network jitter or temporary stream interruption. If a stream is re-ingested within 3 minutes after interruption, the system considers that the new stream is the original stream. If a stream is re-ingested after 3 minutes, the system considers that the new stream is different from the original stream.
   




Query recorded videos 
------------------------------------------

After live streams are recorded into on-demand videos, ApsaraVideo VOD provides various media asset management capabilities that you can use to mange recorded videos. You can use the following methods to obtain a list of recorded videos:

* View recorded videos in the console

  * On the [Video and Audio](https://vod.console.aliyun.com/?/media/video/list#/media/video/list) page of the ApsaraVideo VOD console, set Source to **ApsaraVideo Live** to view recorded videos, as shown in the following figure.

    
  
  * On the [Recording Management](https://live.console.aliyun.com/#/live/record) page of the ApsaraVideo Live console, query recorded videos based on the AppName and StreamName parameters, as shown in the following figure.

    
  

  

* Obtain recorded videos by using callback events

  ApsaraVideo VOD sends callback events when live streams are recorded. You can obtain information about the newly recorded videos from the callback events. For more information, see [AddLiveRecordVideoComplete](/intl.en-US/Developer Guide/Event notification/Events/AddLiveRecordVideoComplete.md).
  

* Query recorded videos by calling API operations

  ApsaraVideo VOD provides the ListLiveRecordVideo operation for you to query recorded videos based on the domain name, `application name`, and `stream name`. For more information, see [ListLiveRecordVideo](/intl.en-US/API Reference/Live to VOD/ListLiveRecordVideo.md)
  



