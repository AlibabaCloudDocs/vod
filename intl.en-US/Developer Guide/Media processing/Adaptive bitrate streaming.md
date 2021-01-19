Adaptive bitrate streaming 
===============================================

ApsaraVideo VOD transcodes a video into video streams at different bitrates and packages these video streams into a single file. This way, media players can switch to the most appropriate video stream based on the network bandwidth. This topic describes the operations, templates, parameters, and examples of adaptive bitrate streaming.

Overview 
-----------------------------

ApsaraVideo VOD transcodes a video into video streams at different bitrates and packages these video streams into a file that contains the bitrate and resolution information of each video stream. In this way, media players can switch automatically to the most appropriate video stream based on the network bandwidth.
**Note**

The most widely used adaptive bitrate streaming methods are HTTP Live Streaming (HLS) and Dynamic Adaptive Streaming over HTTP (DASH). ApsaraVideo VOD supports only HLS adaptive bitrate streaming.

**Benefits** 

Adaptive bitrate streaming enables media players to switch automatically to the most appropriate video stream based on the network bandwidth and terminal. This optimizes user experience of video playback.

Usage notes 
--------------------------------

1. On the **[Added Transcoding Template Group](https://vod.console.aliyun.com/settings/transcode/add#/settings/transcode/add)** page, create a video packaging template that supports adaptive bitrate streaming.

   
   **Note**

   In ApsaraVideo VOD, you can use video packaging templates and subtitle packaging templates to package video streams that have different bitrates and subtitles. ApsaraVideo VOD stores the bitrate and subtitle information in a file so that media players can switch between bitrates or subtitles.

   

2. Upload a video by using the video packaging template.

   

3. After the system packages video streams for adaptive bitrate streaming, check the playlist.

   




Template management 
----------------------------------------

You can use the ApsaraVideo VOD console or API to manage adaptive bitrate streaming templates.

* Manage templates by using the console

  You can use the ApsaraVideo VOD console to manage adaptive bitrate streaming templates. For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).
  

* Manage templates by calling API operations

  For information about API operations for managing adaptive bitrate streaming templates, see [AddTranscodeTemplateGroup](~~102665~~).
  




Template types 
-----------------------------------

ApsaraVideo VOD provides two types of adaptive bitrate streaming templates, which are video packaging templates and subtitle packaging templates. For more information, see the TranscodeTemplate section of the [Basic data types](/intl.en-US/API Reference/Appendix/Basic data types.md) topic.
**Note**

A subtitle packaging template must be associated with a video packaging template and cannot be created separately.

* Video packaging templates

  * You can use a video packaging template to transcode a video into video streams at different bitrates, and package these video streams into a file that contains the bitrate and resolution information of each video stream. This allows media players to switch to the most appropriate video stream based on the network bandwidth.

    
  

  

* Subtitle packaging templates

  * You can use a subtitle packaging template to configure subtitles for a video and store the subtitle information in the adaptive bitrate streaming file. This allows media players to switch between subtitles.

    
  

  
  **Note**
  * Subtitle files must be in the VTT format.

    
  
  * To implement dynamic subtitle overriding, you can call the SubmitTranscodeJobs operation. For more information, see [SubmitTranscodeJobs](~~68570~~).

    
  

  
  




Template parameters 
----------------------------------------

This section describes only some of the special parameters of adaptive bitrate streaming templates. For more information, see [Basic data types](/intl.en-US/API Reference/Appendix/Basic data types.md).

Parameters of an adaptive bitrate streaming template vary according to the template types.

Video packaging parameters:


| API parameter |  Console parameter  |                                                                                                   Description                                                                                                   |
|---------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PackageType   | Packaging Type      | The packaging type. The output files can be in the HLS or DASH format. Valid values: HLSPackage and DASHPackage. **Note** You can set this parameter only to HLSPackage.                        |
| BandWidth     | Bandwidth Threshold | The bandwidth threshold, based on which media players switch between video streams at different bitrates. Unit: bit/s. **Note** This parameter takes effect only for video packaging templates. |



Subtitle packaging parameters:


|  API parameter  |   Console parameter   |                                                                                                                                                                                                         Description                                                                                                                                                                                                          |
|-----------------|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Language        | Language              | The tag of the subtitle language, such as ja or en-US. The tag must comply with the rules specified by **RFC 5646** . **Note** This parameter takes effect only for subtitle packaging templates.                                                                                                                                                                                                            |
| Name            | Subtitle Display Name | The display name of the subtitle in the media player, such as **Chinese** or **English** .                                                                                                                                                                                                                                                                                                                                   |
| Format          | Subtitle Format       | The format of subtitle files. HLS packaging supports only VTT subtitle files. Example: `subtitle.vtt`                                                                                                                                                                                                                                                                                                        |
| SubtitleUrlList | OSS URL               | The Object Storage Service (OSS) endpoint for storing subtitle files. CDN URLs and HTTPS URLs are not supported. Subtitle files can only be stored in buckets allocated by ApsaraVideo VOD. Example: `http://outin-4051403e7.oss-cn-shanghai.aliyuncs.com/subtitles/4dba87c2-a787-42cd-8328-2369aeb8bff3-cn.vtt` **Note** This parameter takes effect only for subtitle packaging templates. |


