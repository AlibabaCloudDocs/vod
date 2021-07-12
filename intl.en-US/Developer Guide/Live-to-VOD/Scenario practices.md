Scenario practices 
=======================================

Features of ApsaraVideo VOD such as transcoding, online editing, AI-based processing, and event notification enable Live to VOD to meet the needs of various business scenarios. This topic describes three typical methods where the features are combined.

Glossary 
-----------------------------

* Recording and transcoding template group: ApsaraVideo VOD uses this template group to transcode a video that is a recording of a live stream.

  

* Production and transcoding template group: ApsaraVideo VOD uses this template group to merge multiple recorded videos and transcode the produced video.

  

* Storage only: After a live stream is recorded, the No Transcoding template group is used and no subsequent operation is performed.

  

* Production only: After ApsaraVideo VOD performs video production based on live streams, the No Transcoding template group is used and no subsequent operation is performed.

  

* Live recording period: This is the interval at which live streams are recorded to ApsaraVideo VOD. For example, if a live stream lasts for 3 hours and you want to provide an video-on-demand (VOD) of the recorded content before the live stream ends, you can set the recording period to 1 hour. After the live stream starts, content broadcast within the previous hour can be played on demand.

  




Practice 1: Live stream recording + Automatic transcoding + CDN acceleration 
-------------------------------------------------------------------------------------------------

After a live stream is recorded, the recorded file is automatically transcoded and CDN accelerated for users to play on demand.

**Applicable scenarios** : This practice is applicable to most live streaming scenarios where no further processing is required.

**The following figure shows the procedure.** 

![Practice 1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4725401161/p183845.png)



1. A user starts stream ingest.

   

2. When the stream ingest reaches a recording period, the recorded file is automatically added to ApsaraVideo VOD.

   

3. After the VOD is recorded, a unique video ID is generated in ApsaraVideo VOD. The video information is sent to the user by using the AddLiveRecordVideoComplete callback event that contains live streaming-related parameters such as DomainName, AppName, and StreamName. After the user receives the callback event, the user records the video information and uses the video ID as an index to update the subsequent video status.

   

4. ApsaraVideo VOD detects the recording and transcoding template group ID in the live-to-VOD configuration specified by the user. The transcoding template group contains the specific code stream transcoding task.

   

5. After a snapshot is taken and all code streams are transcoded, callback events are sent to the user without a time sequence. The user must update the video status based on the video ID in the callback events. After transcoding, the stream can be played. The transcoding callback message contains the stream playback URL. Alternatively, the stream playback URL can be obtained based on the video ID returned by the GetPlayInfo operation. The stream playback URL is CDN accelerated.

   




Practice 2: Live stream recording + Storage only to ApsaraVideo VOD + Manual transcoding triggering + CDN acceleration 
-------------------------------------------------------------------------------------------------------------------------------------------

If you want to only store recorded live stream videos to ApsaraVideo VOD without subsequent transcoding, you can select the storage only template group as the recording and transcoding template group when you create the recording configuration. You can later manually trigger video transcoding. This practice can work with the online editing feature of ApsaraVideo VOD for better effect.
**Note**

To activate only the storage only template group, contact ApsaraVideo VOD technical support.

**Applicable scenarios** : After a live stream ends, you need to perform further content processing, such as live stream editing for sports matches and video games. Then, you can initiate transcoding and CDN acceleration processes. After transcoding, ApsaraVideo VOD automatically performs CDN acceleration for the output files.

**The following figure shows the procedure.** 

![Practice 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4725401161/p183846.png)

1. 

   A user starts stream ingest.
   

2. 

   When the stream ingest reaches a recording period, the recorded file is automatically added to ApsaraVideo VOD.
   

3. 

   After the VOD is recorded, a unique video ID is generated in ApsaraVideo VOD. The video information is sent to the user by using the AddLiveRecordVideoComplete callback event that contains live streaming-related parameters such as DomainName, AppName, and StreamName. After the user receives the callback event, the user records the video information and uses the video ID as an index to update the subsequent video status.
   

4. The user manually triggers transcoding by calling the transcoding task operation for the video. Before that, operations such as online editing can be performed.

   

5. 

   After a snapshot is taken and all code streams are transcoded, callback events are sent to the user without a time sequence. The user must update the video status based on the video ID in the callback events. After transcoding, the stream can be played. The transcoding callback message contains the stream playback URL. Alternatively, the stream playback URL can be obtained based on the video ID returned by the GetPlayInfo operation. The stream playback URL is CDN accelerated.
   




Practice 3: Live stream recording + Automatic merging of multiple periodic videos 
------------------------------------------------------------------------------------------------------

If you want to merge multiple videos generated in the recording period and then process the produced video, you can use the automatic production feature. For example, if you set a recording period of 20 minutes for a live stream that lasts for 1 hour, three videos are generated. When you configure live stream recording, you can enable automatic video production and configure the production and transcoding template group for video production. You can also configure the production only template group and manually trigger transcoding later. The difference between the two methods is the same as that described in the preceding two practices. When the streaming is interrupted for longer than the specified duration, ApsaraVideo VOD automatically performs video production based on live streams and performs subsequent operations based on the transcoding configuration. The streaming interruption timeout period can be specified for the live streams.

* Production + Automatic transcoding

  **Applicable scenarios** : After a live stream ends, you need segments in all recording periods automatically merged and the produced video transcoded. Scenarios include sports matches or the composition of online teaching courses.

  **The following figure shows the procedure.** 

  ![Practice 3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5755401161/p183863.png)
  1. 

     A user starts stream ingest.
     
  
  2. 

     When the stream ingest reaches a recording period, the recorded file is automatically added to ApsaraVideo VOD.
     
  
  3. 

     After the VOD is recorded, a unique video ID is generated in ApsaraVideo VOD. The video information is sent to the user by using the AddLiveRecordVideoComplete callback event that contains live streaming-related parameters such as DomainName, AppName, and StreamName. After the user receives the callback event, the user records the video information and uses the video ID as an index to update the subsequent video status.
     
  
  4. The streaming interruption duration reaches the timeout duration, or the user proactively interrupts the streaming.

     
  
  5. ApsaraVideo VOD receives a message from ApsaraVideo Live which indicates that the live stream has ended.

     
  
  6. ApsaraVideo VOD detects the production configuration in the live-to-VOD configuration specified by the user and determines whether it is necessary to trigger automatic production. If it is necessary, production and transcoding are performed based on the production and transcoding template group in the live-to-VOD configuration.

     
  
  7. The video production starts and a unique video ID is generated in ApsaraVideo VOD for the produced video. The video information is sent to the user by using the LiveRecordVideoComposeStart callback event that contains live streaming-related parameters such as DomainName, AppName, and StreamName. After the user receives the callback event, the user records the video information and uses the video ID as an index to update the subsequent video status.

     
  
  8. After video production is completed based on the mezzanine files, ApsaraVideo VOD sends the FileUploadComplete callback event to notify the user of the status.

     
  
  9. 

     After a snapshot is taken and all code streams are transcoded, callback events are sent to the user without a time sequence. The user must update the video status based on the video ID in the callback events. After transcoding, the stream can be played. The transcoding callback message contains the stream playback URL. Alternatively, the stream playback URL can be obtained based on the video ID returned by the GetPlayInfo operation. The stream playback URL is CDN accelerated.
     
  

  

* Production + Manual transcoding

  When you configure live stream recording, you can enable automatic video production and configure the production and transcoding template group for video production. You can also configure the production only template group and manually trigger transcoding later.

  **Applicable scenarios:** After a live stream ends, you need segments in all recording periods automatically merged without any other processing. You want to perform further processing such as online editing on the produced video, and then manually transcode the video, such as cutting built-in ads in the video or the content played during the rest duration in a sports match.

  **The following figure shows the procedure.** 

  ![Practice 4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5755401161/p183865.png)
  1. A user starts stream ingest.

     
  
  2. 

     When the stream ingest reaches a recording period, the recorded file is automatically added to ApsaraVideo VOD.
     
  
  3. 

     After the VOD is recorded, a unique video ID is generated in ApsaraVideo VOD. The video information is sent to the user by using the AddLiveRecordVideoComplete callback event that contains live streaming-related parameters such as DomainName, AppName, and StreamName. After the user receives the callback event, the user records the video information and uses the video ID as an index to update the subsequent video status.
     
  
  4. The streaming interruption duration reaches the timeout duration, or the user proactively interrupts the streaming.

     
  
  5. ApsaraVideo VOD receives a message from ApsaraVideo Live which indicates that the live stream has ended.

     
  
  6. ApsaraVideo VOD detects the production configuration in the live-to-VOD configuration specified by the user and determines whether it is necessary to trigger automatic production. If it is necessary, production and transcoding are performed based on the production and transcoding template group in the live-to-VOD configuration. Because the production only template group is configured in this scenario, ApsaraVideo VOD does not automatically trigger transcoding.

     
  
  7. The video production starts and a unique video ID is generated in ApsaraVideo VOD for the produced video. The video information is sent to the user by using the LiveRecordVideoComposeStart callback event that contains live streaming-related parameters such as DomainName, AppName, and StreamName. After the user receives the callback event, the user records the video information and uses the video ID as an index to update the subsequent video status.

     
  
  8. After video production is completed based on the mezzanine files, ApsaraVideo VOD sends the FileUploadComplete callback event to notify the user of the status. In this case, the mezzanine files involved in this production task are ready. The user can perform subsequent operations on the video, such as triggering transcoding.

     
  
  9. The user manually triggers transcoding by calling the transcoding task operation for the video. Before that, operations such as online editing can be performed.

     
  
  10. 

      After a snapshot is taken and all code streams are transcoded, callback events are sent to the user without a time sequence. The user must update the video status based on the video ID in the callback events. After transcoding, the stream can be played. The transcoding callback message contains the stream playback URL. Alternatively, the stream playback URL can be obtained based on the video ID returned by the GetPlayInfo operation. The stream playback URL is CDN accelerated.
      
  

  

  



