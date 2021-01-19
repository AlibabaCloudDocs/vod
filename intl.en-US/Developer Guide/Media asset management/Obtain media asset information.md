Obtain media asset information 
===================================================

After media files are uploaded or processed, you can use the ApsaraVideo VOD console or call API operations to obtain media asset information. This topic describes how to obtain media asset information in the ApsaraVideo VOD console. This topic also describes how to call API operations or use SDKs to obtain media asset information.

Overview 
-----------------------------

The media asset information that can be obtained includes basic information and mezzanine file information of media files.

* For video files, you can also obtain playback information.

  

* For video files that are processed by the AI service, you can also obtain AI data.

  




Console management 
---------------------------------------

Log on to the ApsaraVideo VOD console and go to the **[Video and Audio](https://vod.console.aliyun.com/#/media/video/list)** page. You can click **Manage** in the Actions column that corresponds to a media asset and view the media asset details. You can also view the list of audios and videos and the list of images and videos. For more information, see [Media asset management](/intl.en-US/User Guide/Media library/Manage media assets.md).

API or SDK operations 
------------------------------------------

The following table describes the API operations that are used to obtain media asset information.


|      Information type      |                                                      Description                                                      |                                                                     Reference                                                                      |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Basic information          | Obtains the details of a single audio or video file.                                                                  | [Obtain video information](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfo.md)                      |
| Basic information          | Obtains the information about multiple audio and video files.                                                         | [Obtain the information about multiple videos](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfos.md) |
| Basic information          | Obtains image information.                                                                                            | [Obtain image information](/intl.en-US/API Reference/Media management/Image Management/GetImageInfo.md)                            |
| Mezzanine file information | Obtains the information about the mezzanine files of audios or videos.                                                | [Obtain mezzanine file information](/intl.en-US/API Reference/Media management/Audio&Video Management/GetMezzanineInfo.md)         |
| Playback information       | Obtains the playback information.                                                                                     | [Obtain the playback URL](/intl.en-US/Developer Guide/Video play/Use playback URLs.md)                                             |
| AI data                    | Obtains the summary of intelligent review results.                                                                    | [Obtain the summary of intelligent review results]()                                                                               |
| AI data                    | Obtains the details of intelligent review results.                                                                    | [Obtain the details of intelligent review results]()                                                                               |
| AI data                    | Obtains the AI results of speech recognition, text recognition, multimodal video recognition, and people recognition. | [Video AI]()                                                                                                                       |


**Note**

You can also call the [SearchMedia](/intl.en-US/Developer Guide/Media asset management/Search for media asset information.md) operation to obtain media asset information.

**Call methods:** 

* We recommend that you use a server SDK to obtain media asset information by calling the API operation. This method is simpler and more efficient. For more information about server SDKs, see [Usage notes](/intl.en-US/Server SDK Reference/Instructions.md). For more information about API details, see the "`SDK example`" section of API references.

  

* For more information about how to generate HTTP or HTTPS requests, see [Common parameters](/intl.en-US/API Reference/Calling methods/Common parameters.md) and [Examples](/intl.en-US/API Reference/Calling methods/Call Examples.md).

  



