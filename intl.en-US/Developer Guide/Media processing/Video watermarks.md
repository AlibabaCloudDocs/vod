Video watermarks 
=====================================

ApsaraVideo VOD allows you to add watermarks to videos. You can manage watermarks by using the ApsaraVideo VOD console or by calling API operations and can add watermarks to videos during transcoding. This topic describes the usage and management of watermarks, watermark types, position parameters, and usage scenarios.

Overview 
-----------------------------

During video transcoding, you can add images, videos, or text to video streams as watermarks and generate new video files that have the watermarks. You can add signature information such as enterprise logos, brand logos, TV station logos, user IDs, and nicknames as watermarks for video copyright declaration or brand promotion.

**Watermark types** 
----------------------------------------

ApsaraVideo VOD supports static image watermarks, dynamic image watermarks, and text watermarks.

* Static image watermarks

  Only images in the PNG format can be used as static image watermarks. A static image watermark can be displayed in a specific position throughout a video and within a specific time period based on the start and end time that you specify.

  You can use static image watermarks for video copyright declaration or brand promotion.
  




<!-- -->

* Dynamic image watermark

  Dynamic image watermarks support images in the GIF and APNG formats and videos in the MOV format. Dynamic image watermarks can be displayed in a specific position throughout a video and within a specific time period based on the start and end time that you specify.

  You can use dynamic image watermarks for video copyright declaration or brand promotion.

  
  **Note**

  
  * If you use the ApsaraVideo VOD console to add watermarks, you can add only GIF images as dynamic image watermarks. If you add watermarks by calling API operations, you can add GIF and APNG images as well as MOV videos.

    
  
  * If a file is used as a dynamic image watermark, the file name extension must be in lower case. File name extensions of files used as static image watermarks are not limited.

    
  
  * Files used as watermarks and videos to which the watermarks are added must be stored in the same origin. For example, videos stored in an origin in China (Shanghai) can use only watermarks stored in the same origin in China (Shanghai). Videos cannot use watermarks stored in another region or origin. For more information about storage origins, see [Manage VOD resources](/intl.en-US/User Guide/Global settings/Manage VOD resources.md).

    
  

  
  




<!-- -->

* Text watermarks

  You can add one or more pieces of text as watermarks to videos. You can set font configurations such as the font type, size, color, transparency, and border, and add different text content to different videos. For information about dynamic text watermarks, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md).

  You can use text watermarks for video copyright declaration or brand promotion. You can also dynamically replace text watermarks in short videos.

  
  **Note**

  You can manage dynamic image watermarks in the MOV and APNG formats and text watermarks only by calling API operations. For more information, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/AddWatermark.md).
  




Usage notes 
--------------------------------

Perform the following operations to add watermarks to a video:

1. Add and manage watermarks. For more information, see the "Watermark management" section in this topic.

   

2. Set a default watermark. For more information, see [Manage watermarks](/intl.en-US/User Guide/Global settings/Manage watermarks.md) when you add watermarks by using the console or [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/SetDefaultWatermark.md) when you add watermarks by calling API operations.

   

3. Create a transcoding template and set the watermark parameters. For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md) when you add watermarks by using the console or [AddTranscodeTemplateGroup]() when you add watermarks by calling API operations.

   

4. Upload a video by using the template created in Step 3. For more information, see [Upload media assets](/intl.en-US/User Guide/Media library/Upload media assets.md) or [Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md).

   



**Note**



* You must associate a transcoding template with multiple watermarks. For more information, see [AddTranscodeTemplateGroup]().

  

* If the definition is set to Original in a transcoding template, you cannot specify watermarks. The videos transcoded by using this template cannot have watermarks added.

  




Watermark management 
-----------------------------------------

You can manage watermarks by using the ApsaraVideo VOD console or by calling API operations.

* Manage watermarks by using the console

  For information about operations related to watermark management in the ApsaraVideo VOD console, see [Manage watermarks](/intl.en-US/User Guide/Global settings/Manage watermarks.md).
  **Note**

  You cannot upload dynamic image watermarks in the MOV and APNG formats or text watermarks in the ApsaraVideo VOD console. You can do this only by calling the AddWatermark operation. For more information, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/AddWatermark.md).
  




<!-- -->

* Manage watermarks by using API operations

  You can perform the following operations to add a watermark template:
  1. Call the CreateUploadAttachedMedia operation to obtain the directory to which watermarks are added and to obtain temporary permissions.

     
  
  2. Upload watermark files by using Object Storage Service (OSS). For more information, see [Upload OSS objects](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).

     
  
  3. Call the AddWatermark operation to add watermark information. For more information, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/AddWatermark.md).

     
  

  




Watermark position parameters 
--------------------------------------------------

Watermark position parameters are used to set the position and size of a watermark on the image of an output video. You can specify the watermark position by using the ApsaraVideo VOD console or by calling the AddWatermark operation. For more information, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/AddWatermark.md).
**Note**

The following section describes the parameters that are used to configure the position and size of a watermark. For more information, see [Media processing parameters](/intl.en-US/API Reference/Appendix/Media processing parameters.md).

* **Image watermarks** 

  You can use ReferPos, Dx, Dy, Width, and Height to set the position and size of an image watermark on an output video.
  

  |      API parameter       | Console parameter |                                                                                                                                                                                                                              Description                                                                                                                                                                                                                              |
  |--------------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | ReferPos | Location          | The approximate position of the watermark relative to the output video image. * Upper-left: the upper-left corner.   * Lower-left: the lower-left corner.   * Upper-right: the upper-right corner.   * Lower-right: the lower-right corner.                                                      |
  | Dx                       | Horizontal Shift  | The horizontal shift of the watermark on the output video image. You can set the parameter to a value of one of the following types: * Positive integer: Unit: pixels. Value range: \[8, 4096\].   * Image proportion: a proportion to the video image. Value range: (0, 1).                                                                                       |
  | Dy                       | Vertical Shift    | The vertical shift of the watermark on the output video image. You can set the parameter to a value of one of the following types: * Positive integer: Unit: pixels. Value range: \[8, 4096\].   * Image proportion: a proportion to the video image. Value range: (0, 1).                                                                                         |
  | Width                    | Width             | The width of the watermark on the output video image. You can set the parameter to a value of one of the following types: * Positive integer: Unit: pixels. Value range: \[8, 4096\].   * Image proportion: a proportion to the video image. Value range: (0, 1).                                                                                                  |
  | Height                   | Height            | The height of the watermark on the output video image. You can set the parameter to a value of one of the following types: * Positive integer: Unit: pixels. Value range: \[8, 4096\].   * Image proportion: a proportion to the video image. Value range: (0, 1).                                                                                                 |
  | Timeline                 | Timeline          | The watermark timeline is used to control the start time and duration of an image watermark on a video image. You can use multiple watermark configurations to control the dynamic display effect of an image watermark on a video image. For more information, see [Media processing parameters](/intl.en-US/API Reference/Appendix/Media processing parameters.md). **Notice** This parameter is not supported for text watermarks. |

  

  **Schematic diagram** 

  To center a watermark on the image of an output video, set both Dx and Dy to 0.5. A value of 0.5 indicates that the horizontal or vertical shift of the watermark is 50% of the video width or height.![Image watermark position](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6278301161/p178310.png)
  




<!-- -->

* **Text watermarks** 

  You can set the position of a text watermark on the image of an output video only by setting Top and Left. The two parameters indicate the offset of the watermark relative to the upper-left corner of the output video image. The two parameters can be set only to positive integers that indicate the number of pixels. You cannot set them to decimal fractions that indicate a proportion to the video width or height.
  

  | API parameter | Console parameter |                                                                    Description                                                                    |
  |---------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
  | Top           | Vertical Shift    | The distance between the upper-left corner of the watermark and the upper side of the output video image. Unit: pixels. Value range: \[8, 4096\]. |
  | Left          | Horizontal Shift  | The distance between the upper-left corner of the watermark and the left side of the output video image Unit: pixels. Value range: \[8, 4096\].   |

  

  **Schematic diagram** ![Text watermark](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6278301161/p178311.png)
  




<!-- -->

* **Calculation methods** 

  The Dx, Dy, Width, and Height parameters of an image watermark can be calculated based on the positive integers or image proportions that you specify. The Top and Left parameters of a text watermark can be calculated based only on positive integers. The following section describes the calculation methods.
  * Positive integer: Unit: pixels. Value range: \[8, 4096\].

    **Notice**

    If the parameter settings of an image or text watermark are greater than the size of the output video image, the watermark may be partially displayed or not displayed at all.

    For example, if the resolution of the output video is 640 × 360, and ReferPos is set to Upper-left, Dx is set to 4000, and Dy is set to 4000, the watermark is not displayed on the output video image.
    
  
  * Image proportion: the proportion of the width and height of the image watermark to those of the output video. Valid values: (0, 1). The value is accurate to four decimal places.

    **Notice**

    If the resolutions of your output videos frequently change, we recommend that you set the position and size parameters of the watermarks to image proportion values.

    Sample value: 0.9999. Example: Width/Video width = 0.1. Height/Video height = 0.06. Dx/Video width = 0.02. Dy/Video width = 0.03.
    
  

  

* **Default values** 

  * If you do not specify the Width and Height parameters for a watermark, the width of the watermark is calculated based on the following formula: Watermark width = Output video width × 0.12. The height of the watermark scales proportionally based on the aspect ratio of the source watermark image.

    
  
  * If you specify one of the Width and Height parameters for a watermark, the value of the other parameter is calculated based on the specified parameter and the aspect ratio of the source watermark image. For example, if Width is set to 44 and the aspect ratio of the source image is 2:1, the Height value is 22.

    
  
  * If you specify both the Width and Height parameters, the width and height of the output watermark are set to the specified values.

    
  
  * The default values of Dx and Dy are both 0.

    
  

  




Common scenarios 
-------------------------------------

**Dynamic text watermark replacement** 

When users of your business upload short videos, they may add image watermarks (typically product logos) and text watermarks such as the IDs or nicknames of the video creators to their short videos for copyright declaration.

Different users have different IDs and nicknames. Therefore, different text content must be added to different videos during transcoding. This can be implemented by submitting transcoding tasks with a transcoding template that is associated with multiple watermarks. For more information, see [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md).

**Effects** 

Both an image watermark and a text watermark are added to the following images of videos uploaded by different users. The image watermark is the same in both images, but the text watermarks are different and indicate the ID of the user.

![Text watermark effect](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6278301161/p178312.png)

#### **Implementation** 

See [SubmitTranscodeJobs](/intl.en-US/Server SDK Reference/SDK for Java/Media processing.md).
