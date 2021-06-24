Protocol for media asset search 
====================================================

This topic describes the syntax of the protocol for media asset search in ApsaraVideo VOD. You must use the protocol together with the SearchMedia operation. The protocol is a real-time search protocol that integrates the retrieval, filtering, sorting, and pagination features. You can use the protocol to query the information about media assets, such as videos, audio, and images, in ApsaraVideo VOD. 

Syntax 
---------------------------

Media asset fields are classified into the following categories based on syntax rules that are defined in the protocol for media asset search: fields used as returned fields, fields used for exact match, fields used for fuzzy match, fields used for a multi-value query, fields used for a range query, and fields used as sort fields. For more information about all media asset fields that are supported by ApsaraVideo VOD and applicable syntax rules, see the "[Media asset information](#title-sjk-ebd-dtb)" section of this topic. 
**Notice**

When you call the SearchMedia operation to query media asset information, you must perform URL encoding on the query statement. In addition, you must use single-byte punctuation marks, such as equal signs (=), double quotation marks ("), single quotation marks ('), and parentheses (), in the query statement. For more information about special characters that are defined in the protocol for media asset search, see the "[Special characters](#section-zar-pau-cmw)" section of this topic.

The following table describes the syntax that is defined in the protocol for media asset search and provides search examples.




|              Category               |                                                                                                                                                 Description                                                                                                                                                 |                     Syntax                      |                                                            Example                                                            |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Fields used as returned fields      | Specify the fields that are returned in the search results. By default, only the ID, creation time, and type of each media asset are returned.                                                                                                                                                              | field1,field2                                   | [Returned field](/intl.en-US/Developer Guide/Media asset management/Search for media asset information.md)    |
| Fields used for exact match         | Query the information about the media assets that exactly match the value of a specified field.                                                                                                                                                                                                             | field = value                                   | [Exact match](/intl.en-US/Developer Guide/Media asset management/Search for media asset information.md)       |
| Fields used for fuzzy match         | Query the information about the media assets whose value of a specified field contains the specified characters or strings.                                                                                                                                                                                 | field in ('value1','value2') or field = 'value' | [Fuzzy match](/intl.en-US/Developer Guide/Media asset management/Search for media asset information.md)       |
| Fields used for a multi-value query | Query the information about the media assets that match one of the values of a specified field.                                                                                                                                                                                                             | field in ('value1','value2')                    | [Multi-value query](/intl.en-US/Developer Guide/Media asset management/Search for media asset information.md) |
| Fields used for a range query       | Query the information about the media assets whose value of a specified field falls in a specified open or closed interval.                                                                                                                                                                                 | field = (value1,value2)                         | [Range query](/intl.en-US/Developer Guide/Media asset management/Search for media asset information.md)       |
| Fields used as sort fields          | Specify the fields based on which the search results are sorted and the order in which the search results are sorted based on each of the fields. The descending order and ascending order are supported. Multiple sort fields are listed from left to right based on their priorities in descending order. | SortBy=field:Desc                               | [Sort field](/intl.en-US/Developer Guide/Media asset management/Search for media asset information.md)        |



Special characters 
---------------------------------------




| Character |                                                                                                           Description                                                                                                            |                  Syntax                  |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------|
| and       | Connects two filter conditions to query the information about the media assets that meet both the filter conditions.                                                                                                             | field1 = 'value' and field2 = 'value'    |
| or        | Connects two filter conditions to query the information about the media assets that meet one of the filter conditions. If you use or in the query statement, you must enclose the filter conditions in a pair of parentheses (). | (field1 = 'value1' or field2 = 'value2') |
| ( )       | The parentheses, which are used to enclose a specified open or closed interval for a range query.                                                                                                                                | field = ('value1','value2')              |
| ( )       | The parentheses, which are used to enclose multiple filter conditions in the OR relationship.                                                                                                                                    | (field1 = 'value1' or field2 = 'value2') |
| ' '       | The single quotation marks, which are used to enclose field values of the STRING type.                                                                                                                                           | field = 'value'                          |
| ,         | The comma, which is used for a multi-value query. You can separate multiple field values with commas (,).                                                                                                                        | field in ('value1','value2')             |
| ( ) \[ \] | Specifies an open or closed interval for a range query. You can specify whether to include or exclude the left and right endpoints of the interval.                                                                              | field = \['value1','value2'\]            |
| in        | Specifies multiple values for a field in a multi-value query to query the information about the media assets that match one of the values of the specified field.                                                                | field in ('value1','value2')             |



Media asset information 
--------------------------------------------

ApsaraVideo VOD allows you to query the information about specified videos, audio, images, and auxiliary media assets. The following tables describe the syntax rules that are applicable to various media asset fields.

### Video: specifies the information about a video 

**Notice**

You can use the VideoId field to specify a maximum of 100 video IDs in a multi-value query.




|      Field       |    Type    |                                            Description                                             | Used as a returned field | Used for exact match | Used for fuzzy match | Used for a multi-value query | Used for a range query | Used as a sort field |
|------------------|------------|----------------------------------------------------------------------------------------------------|--------------------------|----------------------|----------------------|------------------------------|------------------------|----------------------|
| VideoId          | String     | The ID of the video.                                                                               | √                        | √                    |                      | √                            |                        |                      |
| AppId            | String     | The ID of the application.                                                                         | √                        |                      |                      | √                            |                        |                      |
| CateId           | Long       | The ID of the category to which the video belongs.                                                 | √                        | √                    |                      |                              |                        |                      |
| CateName         | String     | The name of the category to which the video belongs.                                               | √                        |                      |                      |                              |                        |                      |
| StorageLocation  | String     | The region where the video is stored.                                                              | √                        | √                    |                      | √                            |                        |                      |
| Title            | String     | The title of the video.                                                                            | √                        |                      | √                    | √                            |                        |                      |
| Tags             | String     | The tag of the video.                                                                              | √                        |                      | √                    | √                            |                        |                      |
| Description      | String     | The description of the video.                                                                      | √                        |                      | √                    | √                            |                        |                      |
| Status           | String     | [The status of the video.](/intl.en-US/API Reference/Appendix/Basic data types.md) | √                        |                      |                      | √                            |                        |                      |
| MediaSource      | String     | [The source of the video.](#title-ut5-mgi-270)                                     | √                        |                      |                      | √                            |                        |                      |
| PreprocessStatus | String     | [The preprocessing status of the video.](#title-l2i-vpg-gh6)                       | √                        |                      |                      | √                            |                        |                      |
| Size             | Long       | The size of the video.                                                                             | √                        |                      |                      |                              | √                      |                      |
| Duration         | Float      | The duration of the video.                                                                         | √                        |                      |                      |                              | √                      |                      |
| CreationTime     | String     | The time when the video was created.                                                               | √                        |                      |                      |                              | √                      | √                    |
| ModificationTime | String     | The time when the video was last updated.                                                          | √                        |                      |                      |                              | √                      | √                    |
| CoverURL         | String     | The URL of the thumbnail.                                                                          | √                        |                      |                      |                              |                        |                      |
| Snapshots        | String\[\] | The list of automatic snapshots.                                                                   | √                        |                      |                      |                              |                        |                      |
| SpriteSnapshots  | String\[\] | The list of image sprites.                                                                         | √                        |                      |                      |                              |                        |                      |
| DownloadSwitch   | String     | [Specifies whether offline download is enabled.](#title-1gq-v4e-t67)               | √                        |                      |                      |                              |                        |                      |
| TranscodeMode    | String     | [The transcoding mode.](#title-fuw-8fo-vn0)                                        | √                        |                      |                      |                              |                        |                      |



### Audio: specifies the information about an audio file 



|      Field       |    Type    |                                            Description                                             | Used as a returned field | Used for exact match | Used for fuzzy match | Used for a multi-value query | Used for a range query | Used as a sort field |
|------------------|------------|----------------------------------------------------------------------------------------------------|--------------------------|----------------------|----------------------|------------------------------|------------------------|----------------------|
| AudioId          | String     | The ID of the audio.                                                                               | √                        | √                    |                      |                              |                        |                      |
| AppId            | String     | The ID of the application.                                                                         | √                        |                      |                      | √                            |                        |                      |
| CateId           | Long       | The ID of the category to which the audio belongs.                                                 | √                        | √                    |                      |                              |                        |                      |
| CateName         | String     | The name of the category to which the audio belongs.                                               | √                        |                      |                      |                              |                        |                      |
| StorageLocation  | String     | The region where the audio is stored.                                                              | √                        |                      |                      | √                            |                        |                      |
| Title            | String     | The title of the audio.                                                                            | √                        |                      | √                    | √                            |                        |                      |
| Tags             | String     | The tag of the audio.                                                                              | √                        |                      | √                    | √                            |                        |                      |
| Description      | String     | The description of the audio.                                                                      | √                        |                      | √                    | √                            |                        |                      |
| Status           | String     | [The status of the audio.](/intl.en-US/API Reference/Appendix/Basic data types.md) | √                        |                      |                      | √                            |                        |                      |
| MediaSource      | String     | [The source of the audio.](#title-ut5-mgi-270)                                     | √                        |                      |                      | √                            |                        |                      |
| PreprocessStatus | String     | [The preprocessing status of the audio.](#title-l2i-vpg-gh6)                       | √                        |                      |                      | √                            |                        |                      |
| Size             | Long       | The size of the audio.                                                                             | √                        |                      |                      |                              | √                      |                      |
| Duration         | Float      | The duration of the audio.                                                                         | √                        |                      |                      |                              | √                      |                      |
| CreationTime     | String     | The time when the audio was created.                                                               | √                        |                      |                      |                              | √                      | √                    |
| ModificationTime | String     | The time when the audio was last updated.                                                          | √                        |                      |                      |                              | √                      | √                    |
| CoverURL         | String     | The URL of the thumbnail.                                                                          | √                        |                      |                      |                              |                        |                      |
| Snapshots        | String\[\] | The list of automatic snapshots.                                                                   | √                        |                      |                      |                              |                        |                      |
| SpriteSnapshots  | String\[\] | The list of image sprites.                                                                         | √                        |                      |                      |                              |                        |                      |
| DownloadSwitch   | String     | [Specifies whether offline download is enabled.](#title-1gq-v4e-t67)               | √                        |                      |                      |                              |                        |                      |
| TranscodeMode    | String     | [The transcoding mode.](#title-fuw-8fo-vn0)                                        | √                        |                      |                      |                              |                        |                      |



### Image: specifies the information about an image 



|      Field       |  Type  |                                            Description                                             | Used as a returned field | Used for exact match | Used for fuzzy match | Used for a multi-value query | Used for a range query | Used as a sort field |
|------------------|--------|----------------------------------------------------------------------------------------------------|--------------------------|----------------------|----------------------|------------------------------|------------------------|----------------------|
| ImageId          | String | The ID of the image.                                                                               | √                        | √                    |                      |                              |                        |                      |
| AppId            | String | The ID of the application.                                                                         | √                        |                      |                      | √                            |                        |                      |
| CateId           | Long   | The ID of the category to which the image belongs.                                                 | √                        | √                    |                      |                              |                        |                      |
| CateName         | String | The name of the category to which the image belongs.                                               | √                        |                      |                      |                              |                        |                      |
| StorageLocation  | String | The region where the image is stored.                                                              | √                        | √                    |                      | √                            |                        |                      |
| FileName         | String | The file name of the image.                                                                        | √                        |                      | √                    | √                            |                        |                      |
| Title            | String | The title of the image.                                                                            | √                        |                      | √                    | √                            |                        |                      |
| Tags             | String | The tag of the image.                                                                              | √                        |                      | √                    | √                            |                        |                      |
| Description      | String | The description of the image.                                                                      | √                        |                      | √                    | √                            |                        |                      |
| Status           | String | [The status of the image.](/intl.en-US/API Reference/Appendix/Basic data types.md) | √                        |                      |                      | √                            |                        |                      |
| CreationTime     | String | The time when the image was created.                                                               | √                        |                      |                      |                              | √                      | √                    |
| ModificationTime | String | The time when the image was last updated.                                                          | √                        |                      |                      |                              | √                      | √                    |
| URL              | String | The URL of the image.                                                                              | √                        |                      |                      |                              |                        |                      |



### AttachedMedia: specifies the information about an auxiliary media asset 



|      Field       |                                          Type                                          |                                                    Description                                                     | Used as a returned field | Used for exact match | Used for fuzzy match | Used for a multi-value query | Used for a range query | Used as a sort field |
|------------------|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|--------------------------|----------------------|----------------------|------------------------------|------------------------|----------------------|
| MediaId          | String                                                                                 | The ID of the auxiliary media asset.                                                                               | √                        | √                    |                      |                              |                        |                      |
| AppIdString      | String                                                                                 | The ID of the application.                                                                                         | √                        |                      |                      | √                            |                        |                      |
| CateId           | Long                                                                                   | The ID of the category to which the auxiliary media asset belongs.                                                 |                          | √                    |                      |                              |                        |                      |
| Categories       | [Category](/intl.en-US/API Reference/Appendix/Basic data types.md)\[\] | The list of category IDs.                                                                                          | √                        |                      |                      |                              |                        |                      |
| StorageLocation  | String                                                                                 | The region where the auxiliary media asset is stored.                                                              | √                        | √                    |                      | √                            |                        |                      |
| FileName         | String                                                                                 | The file name of the auxiliary media asset.                                                                        | √                        |                      | √                    | √                            |                        |                      |
| Title            | String                                                                                 | The title of the auxiliary media asset.                                                                            | √                        |                      | √                    | √                            |                        |                      |
| Tags             | String                                                                                 | The tag of the auxiliary media asset.                                                                              | √                        |                      | √                    | √                            |                        |                      |
| Description      | String                                                                                 | The description of the auxiliary media asset.                                                                      | √                        |                      | √                    | √                            |                        |                      |
| Status           | String                                                                                 | [The status of the auxiliary media asset.](/intl.en-US/API Reference/Appendix/Basic data types.md) | √                        |                      |                      | √                            |                        |                      |
| CreationTime     | String                                                                                 | The time when the auxiliary media asset was created.                                                               | √                        |                      |                      |                              | √                      | √                    |
| ModificationTime | String                                                                                 | The time when the auxiliary media asset was last updated.                                                          | √                        |                      |                      |                              | √                      | √                    |
| URL              | String                                                                                 | The URL of the auxiliary media asset.                                                                              | √                        |                      |                      |                              |                        |                      |
| BusinessType     | String                                                                                 | The type of the business.                                                                                          | √                        | √                    |                      |                              |                        |                      |



AttachedMedia: specifies the information about an auxiliary media asset 
--------------------------------------------------------------------------------------------

### PreprocessStatus: specifies the preprocessing status of a media asset 

Only preprocessed media assets can be used for live streaming in the streaming panel. 


|       Value       |                Description                 |      Remarks       |
|-------------------|--------------------------------------------|--------------------|
| UnPreprocess      | The media asset has not been preprocessed. | The initial state. |
| Preprocessing     | The media asset is being preprocessed.     | -                  |
| PreprocessSucceed | The preprocessing is complete.             | -                  |
| PreprocessFailed  | The preprocessing failed.                  | -                  |



### DownloadSwitch: specifies whether offline download is enabled for a media asset 

A media asset can be downloaded in offline mode only when offline download is enabled. 


| Value |          Description          |                                        Remarks                                         |
|-------|-------------------------------|----------------------------------------------------------------------------------------|
| on    | Offline download is enabled.  | The initial state, in which the media asset can be downloaded in offline mode.         |
| off   | Offline download is disabled. | If offline download is disabled, the media asset cannot be downloaded in offline mode. |



### MediaSource: specifies the source of a media asset 



|    Value    |                                   Description                                    |                                                                     Remarks                                                                     |
|-------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| general     | The media asset is uploaded to ApsaraVideo VOD in the console.                   | The simple upload mode.                                                                                                                         |
| short_video | The media asset is uploaded to ApsaraVideo VOD by using a short video SDK.       | For more information, see [Overview](/intl.en-US/New Player SDK/Overview.md).                                                   |
| editing     | The media asset is uploaded to ApsaraVideo VOD by using a video production task. | For more information, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). |
| live        | The media asset is uploaded to ApsaraVideo VOD by using live stream recording.   | N/A                                                                                                                                             |



### TranscodeMode: specifies the transcoding mode 

After a media asset is uploaded to ApsaraVideo VOD, it can be played only after a specific processing method is performed on it. Processing methods vary with transcoding modes. 


|     Value      |                                  Description                                  |                                                                                 Remarks                                                                                 |
|----------------|-------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FastTranscode  | The common transcoding.                                                       | The default mode in which the media asset is immediately transcoded after it is uploaded to ApsaraVideo VOD. The media asset can be played only after it is transcoded. |
| NoTranscode    | The media asset is delivered without transcoding.                             | The media assert is not transcoded after it is uploaded to ApsaraVideo VOD and can be immediately played without transcoding.                                           |
| AsyncTranscode | The media asset is immediately delivered and transcoded after it is uploaded. | The media asset can be immediately played and asynchronously transcoded after it is uploaded to ApsaraVideo VOD.                                                        |



