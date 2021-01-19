Video snapshots 
====================================

ApsaraVideo VOD allows you to take video snapshots by using snapshot templates configured in advance. You can manage snapshot templates by using the ApsaraVideo VOD console or by calling API operations. This topic describes the video snapshot feature, including snapshot types, usage notes, snapshot templates, snapshot parameters, and management of snapshot templates.

Overview 
-----------------------------

You can take video snapshots at specific time points in a video to generate image files. To make the feature easier to use, ApsaraVideo VOD provides snapshot templates that you can create by specifying related parameters. You can take snapshots by specifying the ID of a snapshot template.
**Notice**

* A snapshot may fail to be created if a media file is an audio file without any image information, if the mezzanine file is damaged, or if the mezzanine file encapsulation is abnormal.

  

* Snapshots are taken in an asynchronous manner. When a screenshot request is sent and a result is returned by using the API, the task may still be queued and not completed. You can obtain the results of a snapshot request by receiving the SnapshotComplete event notification. For more information, see [SnapshotComplete](/intl.en-US/Developer Guide/Event notification/Events/SnapshotComplete.md).

  

* The time required to create a snapshot depends on the file size, duration, and frame type used to take the snapshot.

  




Snapshot types 
-----------------------------------

* **Thumbnail snapshot (CoverSnapshot)** 

  ApsaraVideo VOD takes snapshots of each video mezzanine file. These snapshots are called thumbnail snapshots. By default, ApsaraVideo VOD takes a maximum of eight snapshots based on the keyframes of the video. The first snapshot is taken at the first keyframe after the fifth millisecond of a video. You can view thumbnail snapshots on the video details page of the ApsaraVideo VOD console and select one as the video thumbnail.
  



**Note**

* If a video contains less than eight keyframes, the number of thumbnail snapshots is less than eight.

  

* If you do not specify a snapshot as the thumbnail, ApsaraVideo VOD selects one of the thumbnail snapshots as the thumbnail.

  




* **Normal snapshot (NormalSnapshot)** 

  You can call API operations to take snapshots of a specific video. You can set the start time and interval for taking snapshots, the total number of snapshots, and the width and height of the snapshots. If you take snapshots of a video repeatedly by calling API operations, ApsaraVideo VOD retains only the snapshot data returned by the last operation. For more information, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitSnapshotJob.md).
  




<!-- -->

* **Sprite snapshot (SpriteSnapshot)** 

  To take sprite snapshots of a video, ApsaraVideo VOD takes normal snapshots and then combines them based on certain arrangement rules. These normal snapshots are called **sprite source snapshots** . Sprite snapshots can reduce the number of snapshot requests so that the information of multiple snapshots can be obtained by a single sprite snapshot request. This improves client performance.

  For example, if you arrange normal snapshots by 10 rows and 10 columns in a sprite snapshot, you can obtain up to 100 normal snapshots from the sprite snapshot. If the number of normal snapshots is less than 100, a sprite snapshot that contains less than 100 normal snapshots is generated. If the number of normal snapshots exceeds 100, a second sprite snapshot is generated to accommodate the excess normal snapshots. This process repeats until all snapshots have been obtained. The following figures show an example of sprite snapshots.![Sprite snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8668301161/p180514.png)

  
  **Note**

  In the preceding figures, the total number of normal snapshots is 50. The normal snapshots are arranged by 10 rows and 3 columns in a sprite snapshot. The first sprite snapshot contains 30 normal snapshots, and the second sprite snapshot contains 20 normal snapshots.
  




<!-- -->

* **Sprite source snapshot (SpriteOriginSnapshot)** 

  Sprite source snapshots are the normal snapshots used to compose sprite snapshots. You can delete or retain sprite source snapshots. If sprite source snapshots are retained, you can query them by calling an API operation. For more information, see [ListSnapshots](/intl.en-US/API Reference/Media management/Image Management/ListSnapshots.md).
  




<!-- -->

* **WebVTT screenshots** 

  WebVTT screenshots are VTT files that contain basic information of all screenshots, such as time and URLs. The information in the VTT files can be obtained and parsed for using preview thumbnails on the progress bar.
  




**WebVTT** snapshot storage method 
-------------------------------------------------------

* **Separate storage** 

  Snapshots are stored separately and their **relative** locations and time are stored in a VTT file, as shown in the following figure.![vtt-single](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8668301161/p178305.png)
  

* **Collective storage** 

  All snapshots are stored as a single image. When the system accesses a specific snapshot, it locates the snapshot based on content of the VTT file, as shown in the following figure.![vtt-big](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8668301161/p178306.png)
  




Usage notes 
--------------------------------

* **Thumbnail snapshots** 

  After a video is uploaded, ApsaraVideo VOD takes **thumbnail snapshots** of the video mezzanine file as the recommended video thumbnails. You are not charged during this process.
  




<!-- -->

* **Snapshots taken by calling an API operation** 

  You can take normal snapshots and sprite snapshots of a specific video by calling an API operation. For more information, see [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitSnapshotJob.md). You can use this method to take **normal snapshots** and **sprite snapshots** .
  




<!-- -->

* **How to query snapshots** 

  ApsaraVideo VOD allows you to query video snapshots by using the following methods:
  * You can obtain snapshot information by receiving the SnapshotComplete event notification. For more information, see [SnapshotComplete](/intl.en-US/Developer Guide/Event notification/Events/SnapshotComplete.md).

    
  
  * You can obtain the default snapshot information by calling the GetVideoInfo operation. For more information, see [GetVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfo.md).

    
  
  * You can query snapshots by calling the ListSnapshots operation. For more information, see [ListSnapshots](/intl.en-US/API Reference/Media management/Image Management/ListSnapshots.md).

    
  

  




<!-- -->

* **How to delete snapshots** 

  ApsaraVideo VOD does not allow you to manage snapshots separately. You must manage them together with videos. When you delete a video, all its snapshots are deleted and cannot be recovered.
  




Management of snapshot templates 
-----------------------------------------------------

Many parameters are involved when snapshots are taken. It is inefficient to specify all these parameters when you submit a snapshot taking task. Therefore, ApsaraVideo VOD provides snapshot templates that you can create by specifying related parameters. You can take snapshots by specifying the ID of a snapshot template.

You can manage snapshot templates by using the ApsaraVideo VOD console or by calling API operations.

* **Manage snapshot templates by using the console** 

  You can create, modify, and delete snapshot templates in the ApsaraVideo VOD console.![Snapshot template management](../images/p178307.png)
  

* **Manage snapshot templates by calling an API operation** 

  For more information, see [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/AddVodTemplate.md)
  




Snapshot parameters 
----------------------------------------

* **Parameters for normal snapshots** 

  **Note**

  The following table lists only some of the parameters for normal snapshots. For more information, see the SnapshotConfig section of [Media processing parameters](/intl.en-US/API Reference/Appendix/Media processing parameters.md).
  

  |    API parameter    | Console parameter |                                                                                                                                                                                                                                                                                                                                                                              Description                                                                                                                                                                                                                                                                                                                                                                               |
  |---------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | FrameType           | Frame Type        | The frame type of the snapshots. Valid values: intra and normal. intra indicates keyframes and normal indicates frames. It is faster to capture keyframes than frames when the same snapshot rules are applied.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
  | SpecifiedOffsetTime | Start Time        | The start time for taking snapshots. The value is a positive integer. Unit: milliseconds. If only one snapshot is taken, `SpecifiedOffsetTime` specifies the time that the snapshot is taken.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
  | Count               | Snapshot Count    | The total number of snapshots to take.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
  | Interval            | Snapshot Interval | The interval between snapshots when multiple snapshots are taken. * If the Count value is greater than 1 and the Interval value is not 0, the system takes the specified number of snapshots at the specified interval.   * If the Count value is greater than 1 and the Interval value is 0, the system takes the specified number of snapshots within the video duration. If the FrameType parameter is set to intra and the number of keyframes is smaller than the Count value, the number of snapshots that are taken is smaller than the value of Count.   * If the Count value is 1, the system takes a single snapshot.    |
  | Width               | Width             | The width of the snapshots. Unit: pixels. Valid values: 8 to 4096. **Note** Description of the Width and Height parameters: * If neither of the Width or Height parameters is specified, the snapshot width and height are the same as those of the video mezzanine file.   * If only one of the Width and Height parameters is specified, the other parameter is automatically set based on the aspect ratio of the input video to ensure that the snapshots are not distorted.                                                                                                                                                                    |
  | Height              | Height            | The height of the snapshots. Unit: pixels. Valid values: 8 to 4096.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

  




<!-- -->

* **Parameters for WebVTT snapshots** 

  When you take WebVTT snapshots, you must specify the `Format` and `SubOut` parameters as listed in the following table in addition to those for normal snapshots.
  

  | API parameter | Console parameter |                                                                                                                                                                                                     Description                                                                                                                                                                                                     |
  |---------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | Format        | Format            | The format in which to collect the index information for snapshots. Set the value to VTT. **Note** This parameter is required only when you take WebVTT snapshots.                                                                                                                                                                                                                                  |
  | SubOut        |                   | Specifies the storage method of WebVTT snapshots. Valid values:  * false: stores snapshots separately.   * true: stores snapshots as a single image.    This parameter is required only when you take WebVTT snapshots. Example: { "IsSptFrag":"true" }  |

  

* **Parameters for sprite snapshots** 

  **Note**

  The following table lists only some of the parameters that must be specified when you take sprite snapshots. For more information, see the SpriteSnapshotConfig section of [Media processing parameters](/intl.en-US/API Reference/Appendix/Media processing parameters.md).
  

  | API parameter | Console parameter |                                                                                                                                                                                                             Description                                                                                                                                                                                                             |
  |---------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | CellWidth     | Width             | The width and height of small images in the sprite snapshot. If neither of the CellWidth or CellHeight parameters is specified, the width and height of small images are the same as those of normal snapshots. If only one of the CellWidth and CellHeight parameters is specified, the other parameter is automatically set based the aspect ratio of the input video.                                                            |
  | CellHeight    | Height            | The width and height of small images in the sprite snapshot. If neither of the CellWidth or CellHeight parameters is specified, the width and height of small images are the same as those of normal snapshots. If only one of the CellWidth and CellHeight parameters is specified, the other parameter is automatically set based the aspect ratio of the input video.                                                            |
  | KeepCellPic   | Retain Snapshots  | Specifies whether to retain the sprite source snapshots after the sprite snapshot is generated. Valid values: delete and keep. **Note** We recommend that you delete sprite source snapshots unless otherwise required.                                                                                                                                                                                             |
  | Color         | Background Color  | The background color of the sprite snapshot. For more information, see [Color setting parameters](/intl.en-US/API Reference/Appendix/Color setting parameters.md). **Note** RGB values are not supported. The following figure provides a schematic diagram of sprite snapshot parameters.![p178308](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8668301161/p181525.png) |

  

  




