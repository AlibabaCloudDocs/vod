Overview 
=============================

The production center provides cloud-based video editing and production services. It provides an online visual editing platform and a wide range of APIs This topic describes the workflow, core chain, API operations, and examples of online editing.

Overview 
-----------------------------

Video production is important throughout the process of creating videos, which includes video capture, production, playback and interaction, and media asset management. After videos are produced, the captured videos are available for distribution and playback. The online editing service is the production center of ApsaraVideo VOD. This service supports features that allow you to cut and merge videos, mix audio, add subtitles, overlay images, mask videos, and apply transition effects. Online editing provides an online visual editing platform and related API operations.

Online editing is a cloud-based service that integrates frontend components or pages and backend services.

* Frontend components or pages include features

  that allow you to cut, merge, and mask videos, overlay text, and adjust sequence of videos. For more information, see [Video editing](/intl.en-US/User Guide/Production Center/Production center.md).
  

* Backend service

  includes the media editing service and online editing project management service.
  * You can use online editing tools to edit the materials uploaded to the media library in ApsaraVideo VOD and submit the generated timeline for video production.

    
  
  * You can also organize timeline data and submit the timeline for video production.

    
  

  

  The new videos produced are stored in the media library in ApsaraVideo VOD. You can directly distribute and play the videos without the need to download or upload the videos.
  




The following figure shows the overall architecture of the online editing system.![Overall architecture of online editing](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2119301161/p178318.png)


|          Term          |                                                                                                                                                          Description                                                                                                                                                           |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| material               | The raw materials provided to edit the video. The input resources must be stored in the media library in ApsaraVideo VOD. Supported media resources include videos, audios, images, and texts.                                                                                                                 |
| online editing project | The data involved in one video editing process. Online editing projects generally include the basic metadata such as the title and time when the video is created, the materials required to edit videos, and the timeline that describes the video editing content.                                                           |
| timeline               | The product after a material and special effect design are arranged based on creative ideas.                                                                                                                                                                                                                                   |
| media production       | The task that is used to submit the prepared timeline and to start video production to generate new media resources after video materials are edited. Media resource production is an asynchronous process. A media production task describes the process from task creation to final completion of media resource production. |
| finished product       | The final product after online editing. The final product is stored in the media library in ApsaraVideo VOD.                                                                                                                                                                                                                   |



**Prerequisites** 

* Input: the media resources to be edited. The input resources must be stored in the media library in ApsaraVideo VOD. You can upload media resources to the media library or record live streams into the media library.

  

* Output: the media resources generated after editing and production. The output resources are also stored in the media library in ApsaraVideo VOD.

  




Core chain 
-------------------------------

The core chain of online editing consists of the following parts: input, processing, and output.

* Input

  The material library is audioused for editing.

  Materials in the material library are classified into videos, audio, and images. The following table lists the formats supported for various materials.
  

  | Material |                                                                                                                  Format                                                                                                                  |
  |----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | Video    | Container format: 3GP, AVI, FLV, MP4, M3U8, MPG, ASF, WMV, MKV, MOV, TS, WebM, and MXF Encoding format: H.264/AVC, H.263, H.263+, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, Quicktime, RealVideo, and Windows Media Video |
  | Audio    | Container format: 3GP, AVI, FLV, MP4, M3U8, MPG, ASF, WMV, MKV, MOV, TS, WebM, and MXF Encoding format: AAC, AC-3, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, and Windows Media Audio                               |
  | Image    | JPG, JPEG, PNG, GIF, and APNG                                                                                                                                                                                                            |

  
  **Note**

  Materials in the material library are from the media library in ApsaraVideo VOD. Files in the media library are classified into mezzanine files and transcoded files. To ensure the best quality of finished resources, the online editing service uses the mezzanine files of ApsaraVideo VOD resources for editing and production.
  

* Processing

  **The core object in editing and production is the timeline.** A timeline consists of multiple tracks, which are also called layers. Each track consists of multiple clips. You can specify the start time, end time, and effect for each clip, and arrange the sequence of the clips.

  You can generate a timeline or directly submit a timeline:
  * Use the frontend components to edit media resources and save the editing data to generate a timeline.

    
  
  * Call the API operation or SDK of the media editing service to directly submit a timeline.

    
  

  

  The media editing service is **the core service of online editing** and generates the finished resources. The media editing service runs in asynchronous mode. After you call the [ProduceEditingProjectVideo](/intl.en-US/API Reference/Video editing/ProduceEditingProjectVideo.md) operation , the service returns the ID of the new resource synchronously and starts an asynchronous production task based on the specified parameters.
  * After the production is complete, you receive the [ProduceMediaComplete](/intl.en-US/Developer Guide/Event notification/Events/ProduceMediaComplete.md) callback event, which indicates that the new resource is produced based on the mezzanine files.

    
  
  * You can also query the status of the new resource based on the resource ID. If the new resource is in the uploaded state, the new resource is produced based on the mezzanine files.

    **Note**

    The efficiency of manual queries is low. To receive notifications, we recommend that you configure the callback mechanism after a production is complete.
    
  

  

  The online editing project management service allows you to create, modify, delete, and query online editing projects and configure materials for the projects. You can use this service to manage your online editing projects in depth.
  

* Output

  The finished resources. All finished resources from online editing are stored in the media library. The following output resource types are supported: video, audio, and GIF image.

  A finished resource is generated and saved as a media file which complies with the following process.

  The online editing service produces a new resource based on the mezzanine files of materials in the material library. Then, online editing stores the produced files as the mezzanine files of resources in the media library in ApsaraVideo VOD. A finished resource (media file) generated after online editing also complies with the following principles:
  * The resolution of the finished resource is determined by the maximum width and height in the mezzanine file resolutions of the materials used by the timeline. For example, assume that the timeline uses three materials whose mezzanine file resolutions are 1280 × 720 pixels, 1920 × 1080 pixels, and 720 × 1280 pixels. Then, the resolution of the finished resource is 1920 × 1280 pixels.

    
  
  * The bit rate of the finished resource is determined by the maximum bitrate of the mezzanine files of the materials used by the timeline.

    
  
  * The default type of the finished resource is video. The encoding format is H.264. The container format is MP4. You can also select a production template on the configuration page or specify a production template in the API call request. Then, you can specify the finished resource type such as audio or GIF, and detailed template parameters.

    
  

  

  The following table lists the formats supported for finished resources.
  

  | Material |                                                     Format                                                     |
  |----------|----------------------------------------------------------------------------------------------------------------|
  | Video    | Container format: FLV, MP4, TS, M3U8, GIF, and MPD Encoding format: H.264/AVC and H.265/HEVC   |
  | Audio    | Container format: FLV, MP4, TS, M3U8, GIF, and MPD Encoding format: MP3, AAC, VORBIS, and FLAC |
  | Image    | GIF                                                                                                            |

  

  After the production is complete, the mezzanine files of finished resources are generated. Then, the system automatically transcodes the mezzanine files and takes snapshots based on your requirements to facilitate fast distribution.
  * You can configure the `TemplateGroupId` parameter in `ProduceConfig` to specify the transcoding process to be started after the production is complete. If this parameter is not configured, the system starts a transcoding process based on the default template group after the production is complete. For more information about how to configure a transcoding template group, see [Transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).

    
  
  * Transcoding and snapshot taking are the post-processing operations of the media editing service. Transcoding and snapshot taking are initiated only after the mezzanine files are generated.

    
  

  




Methods to use the media editing service 
-------------------------------------------------------------

* Use the timeline

  You can directly specify the timeline parameters and call the ProduceEditingProjectVideo operation to perform video production as shown in the following figure. This method is applicable to most scenarios.![Production Service Interaction 1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2119301161/p178321.png)
  




<!-- -->

* Use the online editing project

  You can specify the ID of an online editing project and call the ProduceEditingProjectVideo operation to start media production. This method is applicable when you want to manage an online editing project in depth and submit a production task by using the project. This method can be further divided into the following two modes:
  * Mode 1

    1. Call the AddEditingProject operation to create an online editing project. When you call the operation, specify the timeline parameters for the project.

       
    
    2. Call the ProduceEditingProjectVideo operation by specifying the ID of the project.

       
    

    
  
  * Mode 2

    1. Call the AddEditingProject operation to create an online editing project. When you call the operation, specify a timeline for the project or leave the timeline empty.

       
    
    2. Call the UpdateEditingProject operation to update the timeline of the project.

       
    
    3. Call the ProduceEditingProjectVideo operation by specifying the ID of the project.

       
    

    
  

  




Examples 
-----------------------------

Various examples are provided to demonstrate how to use the video editing service such as how to perform media editing and production by using the timeline. The examples involve the following operations:

* [Cutting and merging](~~95483~~): Merge multiple videos, cut a video with the starting part, ending part, or middle part retained, and merge any parts of multiple videos.

  

* [Audio processing](~~95484~~): Implement various audio processing scenarios, which include muting, audio mixing, audio extraction, volume adjustment, and dubbing.

  

* [Image overlay](~~95485~~): Overlay an image on one or more videos from the start time to the end time of each entire video or in a specified time interval.

  

* [Text overlay](~~95486~~): Overlay text on a video from the start time to the end time of the entire video or in a specified time interval.

  



