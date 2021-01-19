Delete media files 
=======================================

ApsaraVideo VOD may generate multiple types of media files. ApsaraVideo VOD allows you to delete media files at different levels. You can delete media files in the console, by calling the API operation, or by using the SDK. This topic describes how to delete media files.

Features 
-----------------------------

* Delete audio or videos files and the associated files, which include uploaded mezzanine files, transcoded stream files, thumbnail snapshots, and image sprite snapshots.

  

* Delete audio or video streams in the transcoded stream files in a specified definition.

  

* Delete audio or video mezzanine files that are uploaded.

  

* Delete uploaded image files. After image files are deleted, image URLs that use audio and video thumbnails, snapshots, and watermarks cannot be accessed.

  



**Note**

* When you delete objects from OSS, only objects are deleted, but media asset information is not deleted. When you delete media files stored in ApsaraVideo VOD, both files and the media asset information created in ApsaraVideo VOD are deleted.

  

* Files deleted by delete operations cannot be recovered. We recommend that you use caution when you use delete operations.

  

* By default, audio or video mezzanine files that are uploaded without transcoding cannot be deleted. This is because they are also used as stream files for original-quality playback. If you want to delete these files, set Force to true when you call the delete operation.

  




Delete media files by using the console 
------------------------------------------------------------

On the **[Video and Audio](https://vod.console.aliyun.com/#/media/video/list)** page or the **[Image](https://vod.console.aliyun.com/#/media/image/list)** page in the ApsaraVideo VOD conslole, click **Deleted** to delete a media file. For more information, see [Media asset management](/intl.en-US/User Guide/Media library/Manage media assets.md).

Delete media files by calling API operations or by using SDKs 
----------------------------------------------------------------------------------

You can use the API or SDKs to delete audio and video, audio and video stream files, audio and video mezzanine files, and image files.

The following table lists APIs that are used to delete media files.


|      Deleted file      |                                                                         Description                                                                          |                                                                Reference                                                                 |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Audio and video        | Deletes a complete video, including their mezzanine files, transcoded media stream files, and thumbnail snapshots. You can delete multiple videos at a time. | [Delete a complete video](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteVideo.md)              |
| Audio and video stream | Deletes media streams such as video or audio streams and their physical storage files. You can delete multiple media streams at a time.                      | [Delete media streams](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteStream.md)                |
| Mezzanine file         | Deletes mezzanine file information and its storage.                                                                                                          | [Delete multiple mezzanine files](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteMezzanines.md) |
| Image file             | Deletes uploaded images and automatic snapshots of videos.                                                                                                   | [Delete images](/intl.en-US/API Reference/Media management/Image Management/DeleteImage.md)                              |



**Call methods:** 

* We recommend that you use a server SDK to obtain media asset information by calling the API operations. This method is simpler and more efficient. For more information, see [Usage notes](/intl.en-US/Server SDK Reference/Instructions.md). For more information about API operations, see `SDK examples` for each API operation.

  

* For more information about how to generate HTTP or HTTPS requests, see [Common parameters](/intl.en-US/API Reference/Calling methods/Common parameters.md) and [Examples](/intl.en-US/API Reference/Calling methods/Call Examples.md).

  



