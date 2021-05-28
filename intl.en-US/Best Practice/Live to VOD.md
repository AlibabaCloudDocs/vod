# Live to VOD

The Live-to-VOD feature allows you to synchronously record live streams as on-demand videos and supports various processing operations. The operations include media asset management, CDN acceleration, and content production such as online editing. The Live-to-VOD feature also supports media processing. For example, you can transcode streams. You can also use the video AI technologies such as content moderation and intelligent thumbnail to process streams. To use the Live-to-VOD feature, you can configure an automatic workflow or use the API or SDK.

## Preparations

-   Activate ApsaraVideo VOD. For more information, see [Get started with ApsaraVideo VOD](/intl.en-US/Quick Start/Get started with ApsaraVideo VOD.md).
-   Activate ApsaraVideo Live. For more information, see [Activate ApsaraVideo Live and purchase resource plans](/intl.en-US/Pricing/Billing-related operations/Activate ApsaraVideo Live and purchase resource plans.md).
-   Configure settings for the Live-to-VOD feature. For more information, see [Store live recordings in ApsaraVideo VOD](/intl.en-US/Console Guide/Domain Names/Recording management/Store live recordings in ApsaraVideo VOD.md).

After the preceding preparations are completed, you can start to use the Live-to-VOD feature.

**Note:** If you want to use a template group for storage or merging, contact the technical support of ApsaraVideo VOD.

## Terms

You can apply the Live-to-VOD feature to various business scenarios by using it together with other features of ApsaraVideo VOD, such as transcoding, online editing, AI processing, and event notification.

Terms:

-   Template group for recording and transcoding: After a live stream is recorded as an on-demand video, ApsaraVideo VOD uses this template group to transcode the recorded video.
-   Template group for merging and transcoding: After a live stream is recorded, ApsaraVideo VOD uses this template group to automatically merge the recorded videos and transcode the merged video.
-   Template group for storage: After a live stream is recorded, ApsaraVideo VOD performs no subsequent operation on the recorded videos.
-   Template group for merging: After the recorded videos of a live streaming are merged, ApsaraVideo VOD performs no subsequent operation on the merged video.
-   Recording period of live streams: the interval at which the recording of a live stream starts. If a live streaming lasts for 3 hours and you want to provide the recorded video on demand during the live streaming, you can set the recording period to an hour. This way, an hour after the live streaming starts, content in the previous hour can be played on demand.

## Practice 1

**Record a live stream + Enable automatic transcoding + Use CDN to accelerate content delivery**

After a live stream is recorded, the recorded video is transcoded and delivered to CDN nodes as soon as possible so that the video can be played on demand. This practice applies to most live streaming scenarios where you do not need to process recorded videos.

The following figure shows the process.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7043815161/p178459.png)

1.  A stream ingest is started.
2.  When a recording period is reached, the recorded video is automatically delivered to ApsaraVideo VOD.
3.  After the delivery is recorded, ApsaraVideo VOD generates a unique video ID. Then, ApsaraVideo VOD sends the video information and live streaming-related parameters including DomainName, AppName, and StreamName to you by using the AddLiveRecordVideoComplete callback. After you receive the callback, record the video information and use the video ID as an index to update the subsequent video status.
4.  ApsaraVideo VOD detects the ID of the template group that is configured for live stream recording. In this practice, a template group for recording and transcoding that contains specific transcoding tasks is used. ApsaraVideo VOD processes the recorded video based on configuration of the template group.
5.  After a snapshot is taken, a single stream is transcoded, or all streams are transcoded, a callback is sent to you. The callbacks are sent without a time sequence. You can update the video status based on the video ID in the callbacks. After the transcoding is completed, the video can be played. The transcoding callback message contains the streaming URL. You can also obtain the streaming URL by specifying the video ID in the GetPlayInfo operation. The streaming URL is a CDN URL.

## Practice 2

**Record a live stream + Store recorded videos to ApsaraVideo VOD + Manually trigger transcoding + Use CDN to accelerate content delivery**

You may want to store recorded videos to ApsaraVideo VOD without transcoding. In this case, you can select a template group for storage when you configure the Live-to-VOD feature. To use template groups for storage, contact the technical support of ApsaraVideo VOD. When you want to transcode the recorded videos, you can manually trigger transcoding as needed. In addition, this practice can work with the online editing feature to deliver better effects.

This practice applies to scenarios where you want to process the recorded videos after a live streaming ends, such as editing the recorded videos of sports matches and games. Then, you can initiate transcoding and CDN acceleration as needed. After the transcoding is completed, ApsaraVideo VOD automatically performs CDN acceleration for the transcoded videos.

The following figure shows the process.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7043815161/p178460.png)

1.  A stream ingest is started.
2.  When a recording period is reached, the recorded video is automatically delivered to ApsaraVideo VOD.
3.  After the delivery is recorded, ApsaraVideo VOD generates a unique video ID. Then, ApsaraVideo VOD sends the video information and live streaming-related parameters including DomainName, AppName, and StreamName to you by using the AddLiveRecordVideoComplete callback. After you receive the callback, record the video information and use the video ID as an index to update the subsequent video status.
4.  ApsaraVideo VOD detects the ID of the template group that is configured for the live stream recording. In this practice, a template group for storage is used. Therefore, ApsaraVideo VOD does not transcode the recorded video.
5.  You can manually trigger transcoding by calling the SubmitTranscodeJobs operation. Before you trigger transcoding, you can also perform other operations such as online editing on the recorded video.
6.  After a snapshot is taken, a single stream is transcoded, or all streams are transcoded, a callback is sent to you. The callbacks are sent without a time sequence. You can update the video status based on the video ID in the callbacks. After the transcoding is completed, the video can be played. The transcoding callback message contains the streaming URL. You can also obtain the streaming URL by specifying the video ID in the GetPlayInfo operation. The streaming URL is a CDN URL.

## Practice 3

**Record a live stream + Enable automatic merging of recorded videos generated in different recording periods**

You may want to merge the recorded videos that are generated in different recording periods and then process the merged video. If the recording period is 20 minutes and a live streaming lasts for an hour, three recorded videos are generated. ApsaraVideo VOD can automatically merge the recorded videos. When you configure live stream recording, you can enable automatic merging and specify a template group for merging and transcoding. You can also use a template group for merging and manually trigger transcoding later. The differences between the two methods are similar to the differences between the previous two practices. When a live streaming is interrupted for the specified duration, ApsaraVideo VOD automatically merges the recorded videos that are generated for the live streaming and processes the merged video based on the transcoding configuration. You can specify the interruption period in ApsaraVideo Live.

## Merging + Automatic transcoding

This method applies to scenarios where you want all recorded videos to be automatically merged and then transcoded after a live streaming ends, such as sports games and online classes.

The following figure shows the process.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7043815161/p178461.png)

1.  A stream ingest is started.
2.  When a recording period is reached, the recorded video is automatically delivered to ApsaraVideo VOD.
3.  After the delivery is recorded, ApsaraVideo VOD generates a unique video ID. Then, ApsaraVideo VOD sends the video information and live streaming-related parameters including DomainName, AppName, and StreamName to you by using the AddLiveRecordVideoComplete callback. After you receive the callback, record the video information and use the video ID as an index to update the subsequent video status.
4.  The interruption duration of the live streaming reaches the specified timeout duration. You can also manually interrupt the live streaming.
5.  ApsaraVideo VOD receives a message that indicates the end of the live streaming from ApsaraVideo Live.
6.  ApsaraVideo VOD detects the merging configuration of the live stream recording and determines whether to trigger automatic merging. If automatic merging is required, ApsaraVideo VOD uses the specified template group for merging and transcoding to merge the recorded videos and transcode the merged video.
7.  ApsaraVideo VOD starts to merge the recorded videos and generates a unique ID for the merged video. ApsaraVideo VOD sends the video information and live streaming-related parameters including DomainName, AppName, and StreamName to you by using the LiveRecordVideoComposeStart callback. After you receive the callback, record the video information and use the video ID as an index to update the subsequent video status.
8.  After the recorded videos are merged, ApsaraVideo VOD sends you a notification of the merging status by using the FileUploadComplete callback.
9.  After a snapshot is taken, a single stream is transcoded, or all streams are transcoded, a callback is sent to you. The callbacks are sent without a time sequence. You can update the video status based on the video ID in the callbacks. After the transcoding is completed, the video can be played. The transcoding callback message contains the streaming URL. You can also obtain the streaming URL by specifying the video ID in the GetPlayInfo operation. The streaming URL is a CDN URL.

## Merging + Manual transcoding

When you configure live stream recording, you can enable automatic merging and specify a template group for merging and transcoding. In this practice, a template group for merging is used. You can manually trigger transcoding later.

This method applies to scenarios where you want all recorded videos to be merged but not to be transcoded after a live streaming ends. You can process the merged video by using features such as online editing. Then, you can manually transcode the video. For example, you can cut the built-in ads in the video. You can also cut the content of the rest duration if the video content is a sports game.

The following figure shows the process.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8904815161/p178462.png)

1.  A stream ingest is started.
2.  When a recording period is reached, the recorded video is automatically delivered to ApsaraVideo VOD.
3.  After the delivery is recorded, ApsaraVideo VOD generates a unique video ID. Then, ApsaraVideo VOD sends the video information and live streaming-related parameters including DomainName, AppName, and StreamName to you by using the AddLiveRecordVideoComplete callback. After you receive the callback, record the video information and use the video ID as an index to update the subsequent video status.
4.  The interruption duration of the live streaming reaches the specified timeout duration. You can also manually interrupt the live streaming.
5.  ApsaraVideo VOD receives a message that indicates the end of the live streaming from ApsaraVideo Live.
6.  ApsaraVideo VOD detects the merging configuration of the live stream recording and determines whether to trigger automatic merging. If automatic merging is required, ApsaraVideo VOD uses the specified template group to merge the recorded video. In this practice, a template for merging is used. Therefore, ApsaraVideo VOD does not automatically transcode the merged video.
7.  ApsaraVideo VOD starts to merge the recorded videos and generates a unique ID for the merged video. ApsaraVideo VOD sends the video information and live streaming-related parameters including DomainName, AppName, and StreamName to you by using the LiveRecordVideoComposeStart callback. After you receive the callback, record the video information and use the video ID as an index to update the subsequent video status.
8.  After the recorded videos are merged, ApsaraVideo VOD sends you a notification of the merging status by using the FileUploadComplete callback. In this case, the merged video is ready. You can perform subsequent operations on the video. For example, you can trigger transcoding for the video.
9.  You can manually trigger transcoding by calling the transcoding task operation. Before you trigger transcoding, you can also perform other operations such as online editing on the recorded video.
10. After a snapshot is taken, a single stream is transcoded, or all streams are transcoded, a callback is sent to you. The callbacks are sent without a time sequence. You can update the video status based on the video ID in the callbacks. After the transcoding is completed, the video can be played. The transcoding callback message contains the streaming URL. You can also obtain the streaming URL by specifying the video ID in the GetPlayInfo operation. The streaming URL is a CDN URL.

