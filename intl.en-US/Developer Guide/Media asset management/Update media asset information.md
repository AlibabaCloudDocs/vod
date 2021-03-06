Update media asset information 
===================================================

ApsaraVideo VOD allows you to configure part of media asset informationbefore you upload media files.ApsaraVideo VOD can also modify or update part of the media data that is uploaded. This topic describes how to update media asset information by using the ApsaraVideo VOD console or by using the API or SDK.

Overview 
-----------------------------

You can specify part of media asset information when you upload media files. You can also update existing media assets after the upload is complete.

* You can update the title, category, and description of a video.

  

* Part of mezzanine file information about the media file such as the file size, type, and storage region cannot be modified.

  




Console management 
---------------------------------------

Log on to the ApsaraVideo VOD console to go to the **[Video and Audio](https://vod.console.aliyun.com/#/media/video/list)** page. You can click **Manage** in the Actions column to view media asset details and edit video information. For more information, see [Media asset management](/intl.en-US/User Guide/Media library/Manage media assets.md).

API or SDK operations 
------------------------------------------

The following table lists the API operations that are used to upgrade the media asset information.


|            Type            |                                                                                                   Description                                                                                                   |                                                                            Reference                                                                            |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Basic information          | Modifies the information about a single video. You can modify the title, description, thumbnail, category ID, and tag of the video.                                                                             | [Modify video information](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfo.md)                      |
| Basic information          | This operation can also be used to modify the information of a single video. API operations are also apply to audio files. You can modify the title, description, thumbnail, category ID, and tag of the video. | [Modify the information about multiple videos](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfos.md) |
| Basic information          | This operation can also be used to modify the information of a single image. You can modify the title, description, thumbnail, category ID, and tag of the image.                                               | [Update the information about multiple images](/intl.en-US/API Reference/Media asset management/Image management/UpdateImageInfos.md)           |
| Mezzanine file information | Mezzanine file information is the metadata extracted from the media file. File attributes such as the size, type, width, height, status, and storage region cannot be modified.                                 | [GetMezzanineInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetMezzanineInfo.md)                             |
| Playback information       | Playback information such as the encoding format, definition, bitrate, and frame rate cannot be modified. However, you can transcode media files to generate new audio and video streams.                       | [Audio and video transcoding](/intl.en-US/Developer Guide/Media processing/Audio and video transcoding.md)                      |



**Call methods:** 

* We recommend that you use a server SDK to obtain media asset information by calling the API operations. This method is simpler and more efficient. For more information about server SDKs, see [Usage notes](/intl.en-US/Server SDK Reference/Usage notes.md). For more information about API operations, see the "`SDK example`" section of API references.

  

* For more information about how to generate HTTP or HTTPS requests, see [Common parameters](/intl.en-US/API Reference/Calling methods/Common parameters.md) and [Examples](/intl.en-US/API Reference/Calling methods/Call Examples.md).

  



