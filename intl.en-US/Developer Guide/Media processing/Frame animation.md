Frame animation 
====================================

You can use the frame animation feature to transform a specific part of a video into a dynamic image file in the GIF or WEBP format. This topic provides an overview of the frame animation feature and describes how to use it, obtain a dynamic image file, and configure templates and parameters.

Overview 
-----------------------------

A dynamic image is a group of static images that switch at a specific frequency to create a dynamic effect. Most dynamic images are in the GIF format, while WEBP images are less commonly seen. You can choose a format based on your business needs. 

When you use the frame animation feature, ApsaraVideo VOD transforms a specific part of a video into a dynamic image file. Take note of the following items when you use this feature.
**Notice**

* A snapshot may fail to be created if a media file is an audio file without any image information, if the mezzanine file is damaged, or if the mezzanine file encapsulation is abnormal.

  

* Dynamic image files are generated in an asynchronous manner. You can obtain the status of a frame animation task by receiving the DynamicImageComplete event notification. For more information, see [DynamicImageComplete](https://help.aliyun.com/document_detail/143490.html).

  

* The time needed to generate a dynamic image depends on the file size, the duration of the video, and the length of the animation.

  

* For information about the billing methods of the frame animation feature, see [Billing Method](https://www.aliyun.com/price/product?spm=a2c4g.11186623.2.16.6ad476f3AVLuN7#/vod/detail).

  




Formats 
----------------------------

The GIF and WEBP formats are supported. The following section lists their features.

* GIF

  Dynamic images in the GIF format provide high compatibility and are often used to decorate websites.
  




<!-- -->

* WEBP

  WEBP images are smaller in size than images in the GIF format. However, WEBP images are not supported by some browsers, such as IE, Safari, iOS Safari 3.2 to 13.7, and KaiOS browser.
  




Usage 
--------------------------

* Capture dynamic images by calling API operations

  For more information, see [SubmitDynamicImageJob]().
  




<!-- -->

* Capture dynamic images by using the console

  You can generate dynamic images by using workflows. Log on to the **ApsaraVideo VOD console** . In the left-side navigation pane, choose **Configuration Management** \> **Media Processing** \> **Workflows** . On the Workflows page, you can add a Frame Animation workflow.
  




Obtain dynamic images 
------------------------------------------

You can obtain information about dynamic images by using the following methods:

* You can obtain information about dynamic images by receiving the DynamicImageComplete notification event. This is the recommended method. For more information, see [DynamicImageComplete](/intl.en-US/Developer Guide/Event notification/Events/DynamicImageComplete.md).

  

* After dynamic images are generated, you can obtain information about the images by calling the ListDynamicImage operation. For more information, see [ListDynamicImage]().

  



**Note**

If you set a dynamic image as the thumbnail of a video, you can call the GetVideoInfo operation to obtain the URL to the thumbnail. For more information, see [GetVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfo.md).

Templates 
------------------------------

A large number of parameters are involved when the system generates dynamic images. If you submit a frame animation request with all the parameters, it makes the feature difficult to use. Therefore, ApsaraVideo VOD provides frame animation templates. You can first specify relevant parameters in a template, and then specify the ID of the template when you submit a frame animation request.

* Manage frame animation templates by calling API operations

  For more information, see [AddVodTemplate](https://help.aliyun.com/document_detail/141406.html).
  




<!-- -->

* Manage frame animation templates by using the console

  




Parameters 
-------------------------------

This section describes only some of the parameters for frame animation templates. For information about additional parameters, see [Basic data types](/intl.en-US/API Reference/Appendix/Basic data types.md).

* Image parameters

  * Width: the width of the dynamic image. Unit: pixels. Value range: \[128, 4096\].

    
  
  * Height: the height of the dynamic image. Unit: pixels. Value range: \[128, 4096\].

    
  
  * Fps: the frame rate of the dynamic image. Value range: (0, 60\].

    
  

  




<!-- -->

* TimeSpan parameters

  * Seek: the start time of the captured part of the video.

    
  
  * Duration: the duration of the captured part of the video.

    
  
  * End: the duration of the remaining part of the video after animation capture.

    
  

  



**Note**



Specify the TimeSpan parameters in one of the following formats:

* Format 1: sssss\[.SSS\]. Value range: \[0.000, 86399.999\].
  Example: 12000.556.

  

* Format 2: hh:mm:ss\[.SSS\]. Value range: \[00:00:00.000, 23:59:59.999\].
  Example: 00:00:05.003.

  

* Seek is required. You need only to set one of the Duration and End parameters. If you set both, the End parameter prevails.

  




