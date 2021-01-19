FAQ about Live to VOD 
==========================================



How many on-demand videos are generated during recording? 
------------------------------------------------------------------------------

The number of videos generated during a live stream varies according to the recording period you specify and interruptions during the live stream. During a live stream, an on-demand video is generated each time the recording period is reached. By default, the system considers that a live stream ends when it is interrupted for 3 minutes. In this case, an on-demand video is also generated based on the content recorded until the interruption.

For example, the recording period is set to 30 minutes and the live stream is interrupted 38 minutes after it starts. Then, a 30-minute video and an 8-minute video are generated in ApsaraVideo VOD.

What is a recording and transcoding template? 
------------------------------------------------------------------

A recording and transcoding template can be used by ApsaraVideo VOD to automatically transcode on-demand videos whenever they are generated.

If the template specifies a standard and a high definitions stream, two streams are generated after a video is transcoded.
**Notice**

You must create the transcoding template in the ApsaraVideo VOD console before a live stream starts.

Can on-demand videos be generated without being transcoded? 
--------------------------------------------------------------------------------

Yes. To generate on-demand videos without transcoding, you can use the **No Transcoding** template as the transcoding template. In this case, an on-demand video is not transcoded, and the URL of the mezzanine video file is returned when a user requests playback information.
**Notice**

We recommend that you always transcode on-demand videos. If a live stream is in a high bitrate, frame freezing may frequently occur during the playback of the on-demand video recorded from the live stream that is not transcoded. For on-demand videos that are not transcoded, you can manually submit a media processing task to transcode them later.

What is automatic production? 
--------------------------------------------------

Automatic production refers to the process where ApsaraVideo VOD automatically generates an on-demand video whenever the recording period is reached.

For example, if the recording period is set to 30 minutes, two on-demand videos are generated for a one-hour live stream. If automatic production is enabled, ApsaraVideo VOD automatically performs production based on the two on-demand videos when the live stream ends. After the production, ApsaraVideo VOD returns the ID of the produced video in callback mode. In this case, you obtain three videos in total, including two on-demand videos and one merged video.

When do I enable automatic production? 
-----------------------------------------------------------

You can enable automatic production when you want to obtain a complete on-demand video for a live stream. For quick playback, you may set a short recording period such as 10 minutes.

In this case, an on-demand video is generated in ApsaraVideo VOD for playback every 10 minutes after the live stream starts. You can enable automatic production so that ApsaraVideo VOD can automatically merge all the 10-minute on-demand videos into a single video. You can also manually call an online editing operation to perform video production.

Is video production performed if only one on-demand video is generated? 
--------------------------------------------------------------------------------------------

After automatic production is enabled, ApsaraVideo VOD performs video production regardless of the number of videos generated.

For example, if you set the recording period to 30 minutes but the live stream lasts for only 20 minutes, a 20-minute on-demand video is recorded in ApsaraVideo VOD. In addition, a 20-minute video is produced from the only mezzanine file.

Is production asynchronous? 
------------------------------------------------

Yes. The production process is asynchronous and takes time. You can obtain the production result by receiving a callback event. For more information, see [Scenario practices](/intl.en-US/Developer Guide/Live-to-VOD/Scenario practices.md).

What is a production and transcoding template? 
-------------------------------------------------------------------

ApsaraVideo VOD can automatically transcode produced videos after automatic production is enabled, which is similar to transcoding of on-demand videos.
**Note**

The ID of the production and transcoding template can be different from the ID of the recording and transcoding template.

For example, you can select a recording and transcoding template to generate only one stream of the standard definition for quick playback. For a produced video, you can select a production and transcoding template to generate streams of multiple definitions, such as high definition, ultra high definition, and 2K. This way, intermediate on-demand videos are transcoded in a low bitrate for quick playback. The complete video of the live stream is transcoded in multiple bitrates after the live stream ends.

Can I perform video production without transcoding the produced video? 
-------------------------------------------------------------------------------------------

Yes. To perform video production without transcoding the produced video, use the **No Transcoding** template as the production and transcoding template.

What is the maximum number of videos that can be merged in automatic video production? 
-----------------------------------------------------------------------------------------------------------

Up to 40 videos can be merged in automatic video production. For example, if the recording period is set to 1 hour, only the videos recorded within the first 40 hours are merged in automatic video production. Therefore, we recommend that you set an appropriate recording period.

What is an appropriate recording period? 
-------------------------------------------------------------

We recommend that you set the recording period to the default value of 1 hour if you do not need on-demand videos for quick playback. You can set the recording period based on your business needs. Generally, we recommend that you set a recording period of longer than 20 minutes.
