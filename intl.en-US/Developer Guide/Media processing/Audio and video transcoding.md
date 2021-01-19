Audio and video transcoding 
================================================

Transcoding is an essential part of media processing. This topic provides an overview of transcoding and describes how to trigger transcoding by using the console and by calling the API when you upload videos, and how to upload videos without transcoding them. This topic also explains Narrowband HD ^TM^ 1.0 and the parameters for transcoding templates.

Overview 
-----------------------------

**Concept** 

Video transcoding refers to the process of converting a compressed and encoded video stream to another video stream to adapt to different network bandwidths, terminal processing capabilities, and user needs. Transcoding is essentially a process of decoding and encoding. Streams before and after transcoding may use the same or different video encoding standards.

The following figure shows where video transcoding takes place in a video production workflow.

![Flowchart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6748301161/p180475.png)

**Features** 

* Video processing: ApsaraVideo VOD provides comprehensive [transcoding](~~99380~~) and [format conversion](~~99380~~) capabilities to convert between various media file formats.

  

* Audio processing: ApsaraVideo VOD provides audio processing features such as audio transcoding and audio extraction.

  

* Watermark: ApsaraVideo VOD supports static image watermarks, dynamic image watermarks such as GIF and MOV files, and text watermarks. You can add multiple watermarks to a video. For more information, see [Video watermarks](/intl.en-US/Developer Guide/Media processing/Video watermark.md).

  

* Multiple preset definitions: ApsaraVideo VOD provides multiple preset definitions, such as Standard Definition, High Definition, Ultra High Definition, 2K, and 4K. ApsaraVideo VOD provides the best empirical settings and lowers the requirements on users.

  

* Multi-scenario solutions such as audio extraction: You can extract an audio track of the standard or high quality from videos as audio output. This applies to scenarios such as broadcasting at a radio station.

  

* Content protection: ApsaraVideo VOD supports content encryption for various scenarios such as online education and originality protection.

  




**Benefits** 

* Adaptation to multiple terminals: generates content that can be played on PCs, TVs, and mobile devices.

  

* Adaptation to multiple network environments: allows you to select the most appropriate bitrate based on your network bandwidth for smooth playback.

  

* Reduction of storage and distribution costs: allows you to adjust video bitrates, improve video compression efficiency, and reduce file sizes without changing the image quality. This ensures smooth playback and saves storage space and traffic.

  

* Content protection: supports content encryption for various scenarios such as online education and originality protection.

  

* Watermarking: allows you to add information such as enterprise logos, TV station logos, user IDs, and nicknames as watermarks for video copyright declaration or brand promotion.

  




ApsaraVideo VOD provides multiple scenario-specific preset definitions and streamlines the process from uploading to transcoding based on long-term data analysis.

**No transcoding** 

* Some videos such as short videos are compressed when they are captured. They can be directly played on multiple terminals. In this case, you can distribute them without transcoding.

  

* For videos that have been transcoded locally, ApsaraVideo VOD does not need to transcode them again. In this case, you can also distribute these videos without transcoding.

  




Narrowband HD 
----------------------------------

Based on the proprietary transcoding technology of Alibaba Cloud, Narrowband HD^TM^ 1.0 intelligently analyzes each scene, action, content, and texture in videos. It reduces the bitrate and bandwidth cost without changing the image quality. For more information, see [the article posted in Yunqi Community](https://yq.aliyun.com/articles/73018).

ApsaraVideo VOD presets multiple definitions that support Narrowband HD. Narrowband HD transcoding supports the MP4, FLV, and HLS formats. The following table lists the parameter settings for each definition.


|      Definition       | Bitrate range (kbit/s) | Resolution: Width (pixels) |
|-----------------------|------------------------|----------------------------|
| Low Definition        | ≤ 400                  | 640                        |
| Standard Definition   | ≤ 800                  | 848                        |
| High Definition       | ≤ 1500                 | 1280                       |
| Ultra High Definition | ≤ 3000                 | 1920                       |
| 2K                    | ≤ 4000                 | 2048                       |
| 4K                    | ≤ 8000                 | 3840                       |



**Configuration method** 

For more information about the configuration method, see [AddTranscodeTemplateGroup](). Specify a preset definition to configure Narrowband HD transcoding.
**Note**

* The billing method for Narrowband HD transcoding is different from that for common transcoding. Submit a ticket for consultation.

  

* Narrowband HD ^TM^ 2.0 is available in the following regions: China (Hangzhou), China (Shanghai), and China (Beijing). Only H.264 videos are supported and the price is ten times of that of Narrowband HD ^TM^ 1.0.

  




Instructions 
---------------------------------

* Automatically transcode uploaded videos

  * You can directly upload videos in the ApsaraVideo VOD console. ApsaraVideo VOD automatically transcodes the uploaded videos based on the specified transcoding template. For more information, see [Upload media assets](/intl.en-US/User Guide/Media library/Upload media assets.md).![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6748301161/p178278.png)

    
  
  * You can also specify a transcoding template ID when you obtain an upload credential. After you upload a video by using the upload credential, ApsaraVideo VOD automatically transcodes the video based on the transcoding template. Then, ApsaraVideo VOD returns the information of the transcoded stream to you based on your callback settings. For more information, see [Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md).

    
  

  

* Perform video transcoding by using the console

  You can use the console to transcode videos that are stored in ApsaraVideo VOD.
  1. On the Video and Audio page of the ApsaraVideo VOD console, find the video that you want to transcode, and choose **More** \> Media Processing in the Actions column.![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6748301161/p178279.png)

     
  
  2. In the Media Processing dialog box, select a transcoding template group and click **OK** to start transcoding.![Transcoding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6748301161/p180483.png)

     
  

  

* Perform video transcoding by calling the API

  You can also call an API operation to specify a transcoding template and manually initiate transcoding. For more information, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). This operation is often used to re-transcode existing videos, encrypt existing videos in standard HLS encryption mode, and override watermark parameters.
  

* Upload videos without transcoding

  You can also use the **No Transcoding template** to upload videos. In this case, uploaded videos are not transcoded. ApsaraVideo VOD adds information about the video mezzanine files to the information list of video streams that can be played. You can obtain the playback URLs of the video mezzanine files from the playback information returned by the GetPlayInfo operation. The No Transcoding template is often used to upload short videos.
  




Transcoding templates 
------------------------------------------

Transcoding parameters are often complex. To relieve users of complex parameter management, ApsaraVideo VOD saves complex parameters as templates. You can customize transcoding templates. A custom transcoding template contains a set of transcoding parameters such as audio, video, and container parameters to satisfy your personalized transcoding needs. A transcoding template can generate multiple output streams. In addition, ApsaraVideo VOD provides recommended parameter settings based on the video definition and audio quality, which allows you to start transcoding videos without learning the technical details.

The following figure shows the **[Added Transcoding Template Group](https://vod.console.aliyun.com/#/settings/transcode/add)** page of the ApsaraVideo VOD console.![转码模板 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7056348061/p182466.png)

**Transcoding template details** 

ApsaraVideo VOD provides seven video definitions, which are Low Definition, Standard Definition, High Definition, Ultra High Definition, 2K, 4K, and Original, as well as two audio definitions, which are Standard Quality and High Quality. ApsaraVideo VOD provides recommended parameter settings for each definition. When you select a definition, ApsaraVideo VOD automatically sets parameters to recommended values to help you quickly customize a template.
**Note**

For more information about the parameter description, see [Terms](/intl.en-US/Introduction/Glossary.md).

The following table describes the parameters of transcoding templates.


| No. |                                   Category                                   |         Parameter         |                                                                                                                                                                                                                                                                                        Description                                                                                                                                                                                                                                                                                        |
|-----|------------------------------------------------------------------------------|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | Basic Parameters                                                             | Encapsulation Format      | * Supported video formats: HLS, MP4, and FLV.   * Supported audio format: MP3.    For more information about each format, see [Terms](/intl.en-US/Introduction/Glossary.md).                                                                                                                                                                                                                                                                                                           |
| 1   | Basic Parameters                                                             | Definition                | * Video: Low Definition, Standard Definition, High Definition, Ultra High Definition, 2K, 4K, and Original that is used for format conversion.   * Audio: Standard Quality and High Quality                                                                                                                                                                                                                                                                                                            |
| 2   | Video Parameters                                                             | Disable Video             | If you select this check box, the transcoded stream does not contain video information. You can select this check box to extract audio in scenarios such as radio broadcasts.                                                                                                                                                                                                                                                                                                                                                                                                             |
| 2   | Video Parameters                                                             | Encoding Format           | Valid values: H.264 and H.265.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| 2   | Video Parameters                                                             | Bitrate                   | Valid values: 10 to 50000. Unit: Kbit/s. The bitrate is used to control the definition. We recommend that you use the recommended value for each definition.                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 2   | Video Parameters                                                             | Resolution                | Valid values of the width or height: 128 to 4096. Unit: pixels. You can specify only one of the width and height options. The other option is automatically set based on the aspect ratio of the video mezzanine file.                                                                                                                                                                                                                                                                                                                                                                    |
| 2   | Video Parameters                                                             | Frame Rate                | The number of frames per second. We recommend that you use the recommended value for each definition.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 2   | Video Parameters                                                             | Maximum Keyframe Interval | The number of frames in a GOP. We recommend that you use the recommended value for each definition.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 2   | Video Parameters                                                             | Watermark                 | Specifies whether to add watermarks to a video. To add watermarks to a video, you must add watermark materials in watermark settings and select this check box. For more information, see [Video watermarks](/intl.en-US/Developer Guide/Media processing/Video watermark.md).                                                                                                                                                                                                                                                                                            |
| 3   | Audio Parameters                                                             | Disable Audio             | If you select this check box, the transcoded stream does not contain audio information. If you want to generate a video stream with no sound, select this check box.                                                                                                                                                                                                                                                                                                                                                                                                                      |
| 3   | Audio Parameters                                                             | Encoding Format           | If you set Encapsulation Format to hls or mp4, you can set this parameter to AAC or MP3. If you set Encapsulation Format to mp3, you can set this parameter only to MP3.                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 3   | Audio Parameters                                                             | Sample Rate               | We recommend that you use the recommended value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 3   | Audio Parameters                                                             | Bitrate                   | Valid values: 8 to 1000. Unit: Kbit/s. We recommend that you use the recommended value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 3   | Audio Parameters                                                             | Audio Channels            | We recommend that you use the recommended value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 4   | Advanced Parameters (available only when Encapsulation Format is set to hls) | Fragment Length           | The duration of each TS fragment. We recommend that you use the recommended value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| 4   | Advanced Parameters (available only when Encapsulation Format is set to hls) | Video Encryption          | The HLS format supports encryption. After you enable **HLS encryption** , you must integrate an official playback SDK that supports video encryption to play videos. This service offers free trial. **Note** The HLS encryption feature configured here encrypts videos by using Alibaba Cloud proprietary cryptography. To encrypt videos in standard HLS encryption mode, call the SubmitTranscodeJobs operation. For more information, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). |
| 5   | Conditional Transcoding Parameters                                           | Video Resolution Check    | Checks whether the resolution of the video mezzanine file is lower than the resolution specified in the transcoding template.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 5   | Conditional Transcoding Parameters                                           | Video Bit Rate Check      | Checks whether the bitrate of the video mezzanine file is lower than the bitrate specified in the transcoding template.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 5   | Conditional Transcoding Parameters                                           | Audio Bit Rate Check      | Checks whether the bitrate of the audio mezzanine file is lower than the bitrate specified in the transcoding template.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |



`Conditional transcoding parameters` are often configured when you want to generate streams in higher definitions. For example, if you set the definition to 4K but the resolution of the video mezzanine file is lower than 4K, the images are stretched, which lowers the image quality. In this case, you can configure conditional transcoding parameters.

The following processing methods are supported:

* If the bitrate or resolution specified in the transcoding template is higher than that of the video mezzanine file, the video is not transcoded to the template specifications.

  

* If the bitrate or resolution specified in the transcoding template is higher than that of the video mezzanine file, the video is transcoded to the template specifications. However, the bitrate or resolution of the transcoded stream is the same as that of the video mezzanine file.

  




**No Transcoding template** 

Videos distributed without transcoding are directly used as video mezzanine files for playback. If this template is used, ApsaraVideo VOD automatically distributes video mezzanine files and writes the file information to video stream information. When you call the GetPlayInfo operation to obtain playback information, the URLs of the video mezzanine files are returned as playback URLs. For more information, see [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md). This template is often used in scenarios such as short video and live-to-VOD scenarios. You can directly play the video mezzanine files.
**Note**

The uploaded video mezzanine files must be playable.

Best practices 
-----------------------------------

For more information, see [Select a transcoding type](/intl.en-US/Best Practice/Select a transcoding type based on your transcoding scenario.md).
