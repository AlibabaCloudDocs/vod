# Select a transcoding type

To meet the transcoding requirements of users from different sectors, ApsaraVideo VOD provides a transcoding solution that is suitable for various business scenarios. ApsaraVideo VOD abstracts custom scenario requirements of users. This way, it can deal with the same or similar scenario requirements of other ApsaraVideo VOD users.

## Preparations

-   Activate ApsaraVideo VOD. For more information, see [Get started with ApsaraVideo for VOD]().
-   Add a transcoding template group. For more information, see [Transcoding settings]().

## Terms

-   File upload: Upload files to ApsaraVideo VOD. You can upload files by using the upload SDK, the Live-to-VOD feature, or the short video SDK. You can also manually upload files after you obtain the upload credential by calling the API.
-   Transcoding: Transcode the content of uploaded files, including video and audio files, based on the specified transcoding parameters.
-   Online editing: Edit files that are uploaded to ApsaraVideo VOD online, such as merging or cropping files.
-   AI processing: Use AI technologies to process videos that are uploaded to ApsaraVideo VOD. For example, ApsaraVideo VOD provides the features of automated review, intelligent thumbnail, segment extraction of news, and content analysis such as tag analysis, speech recognition, and text recognition.
-   CDN acceleration: Deliver audio or video files to Content Delivery Network \(CDN\) nodes across the network to accelerate content access and improve user experience.
-   Videos of different specifications: Videos can be transcoded to streams with different encoding parameter settings, such as the resolution and bitrate. Videos of different specifications can apply to different network bandwidth conditions.
-   Delivery after Transcoding: After a video is uploaded, the mezzanine file is transcoded to streams of different specifications. Then, the videos are accelerated by CDN for playback on terminals.
-   Delivery without Transcoding: After a video is uploaded, the mezzanine file is accelerated by CDN for playback on terminals, but is not transcoded.

## Common transcoding

**Asynchronous processing and delayed playback** After a video is uploaded to ApsaraVideo VOD, the video is transcoded to streams of different specifications to adapt to different network bandwidth conditions and terminals. Then, the video is accelerated by CDN and played on terminals. **Method**: Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?#/vod/settings/transcode/vod) and choose Media Processing \> Transcode. Create a transcoding template group and set it as the default one. Then, after you upload videos, ApsaraVideo VOD automatically completes the subsequent process. The following figure shows the video processing flowchart of this method.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6223815161/p178457.png)

## Delivery without transcoding

**Fast delivery: real-time playback of short videos without transcoding**

For videos that are recorded and uploaded by using the short video SDK, the encoding settings of the videos can adapt to different network bandwidth conditions and terminals. Therefore, you can deliver these videos by using CDN acceleration without transcoding them. This method accelerates the response to playback requests and saves your transcoding costs. **Method**: Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/?#/vod/settings/transcode/vod) and choose Media Processing \> Transcode. Set the No Transcoding template group as the default one. Then, you can upload videos as needed.

> Note: After you activate ApsaraVideo VOD, ApsaraVideo VOD provides the No Transcoding template group and sets it as the default one.

The following figure shows the video processing flowchart of this method.![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6223815161/p178458.png)

