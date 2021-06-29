Basic structures 
=====================================

This topic describes the basic structures of the ApsaraVideo VOD API. 

Video: the information about a video 
---------------------------------------------------------



|                                         Parameter                                          |    Type    |                                    Description                                     |
|--------------------------------------------------------------------------------------------|------------|------------------------------------------------------------------------------------|
| VideoId                                                                                    | String     | The ID of the video.                                                               |
| Title                                                                                      | String     | The title of the video.                                                            |
| Description                                                                                | String     | The description of the video.                                                      |
| Duration                                                                                   | Float      | The duration of the video. Unit: seconds.                                          |
| CoverURL                                                                                   | String     | The URL of the video thumbnail.                                                    |
| [Status](/intl.en-US/API Reference/Appendix/Basic structures.md)           | String     | The status of the video.                                                           |
| CreationTime                                                                               | String     | The time when the video was created. The time is displayed in UTC.                 |
| Size                                                                                       | Long       | The size of the mezzanine video file. Unit: byte.                                  |
| Snapshots                                                                                  | String\[\] | The URLs of video snapshots. The value is an array.                                |
| CateId                                                                                     | Long       | The category ID of the video.                                                      |
| CateName                                                                                   | String     | The category name of the video.                                                    |
| Tags                                                                                       | String     | The tags of the video. Multiple tags are separated by commas (,).                  |
| TemplateGroupId                                                                            | String     | The ID of the transcoding template group that was used to transcode the video.     |
| StorageLocation                                                                            | String     | The URL of the Object Storage Service (OSS) bucket where the video file is stored. |
| [AppId](/intl.en-US/Developer Guide/Multi-application service/Overview.md) | String     | The ID of the application.                                                         |



VideoBase: the basic information about a video 
-------------------------------------------------------------------



|                                    Parameter                                     |   Type    |                                                                                      Description                                                                                      |
|----------------------------------------------------------------------------------|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VideoId                                                                          | String    | The ID of the video.                                                                                                                                                                  |
| Title                                                                            | String    | The title of the video.                                                                                                                                                               |
| Duration                                                                         | String    | The duration of the video. Unit: seconds.                                                                                                                                             |
| CoverURL                                                                         | String    | The URL of the video thumbnail.                                                                                                                                                       |
| [Status](/intl.en-US/API Reference/Appendix/Basic structures.md) | String    | The status of the video.                                                                                                                                                              |
| CreationTime                                                                     | String    | The time when the video was created. The time is displayed in UTC.                                                                                                                    |
| MediaType                                                                        | MediaType | The type of the media asset. Valid values: * video: video   * audio: audio only    |


**Note**

By default, the GetPlayInfo operation returns a Content Delivery Network (CDN) URL. If no domain name is specified, the GetPlayInfo operation returns an OSS URL. In this case, only the URL of the .mp4 video file can be used for playbacks.

Media: the information about a media asset 
---------------------------------------------------------------



|                                               Parameter                                                |     Type      |                                                                                                                                                 Description                                                                                                                                                  |
|--------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MediaId                                                                                                | String        | The ID of the media asset.                                                                                                                                                                                                                                                                                   |
| CreationTime                                                                                           | String        | The time when the media asset was created. The time is displayed in UTC.                                                                                                                                                                                                                                     |
| MediaType                                                                                              | String        | The type of the media asset. Valid values: * video: video   * audio: audio only   * image: image   * attached: auxiliary media asset    |
| [Video](/intl.en-US/API Reference/Appendix/Protocol for media asset search.md)         | Video         | The information about the video.                                                                                                                                                                                                                                                                             |
| [Audio](/intl.en-US/API Reference/Appendix/Protocol for media asset search.md)         | Audio         | The information about the audio.                                                                                                                                                                                                                                                                             |
| [Image](/intl.en-US/API Reference/Appendix/Protocol for media asset search.md)         | Image         | The information about the image.                                                                                                                                                                                                                                                                             |
| [AttachedMedia](/intl.en-US/API Reference/Appendix/Protocol for media asset search.md) | AttachedMedia | The information about the auxiliary media asset.                                                                                                                                                                                                                                                             |



PlayInfo: the playback information about a video stream 
----------------------------------------------------------------------------



|    Parameter     |  Type  |                                                                                                                                                                                                                                                           Description                                                                                                                                                                                                                                                           |
|------------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Bitrate          | String | The bitrate of the video stream. Unit: Kbit/s.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Definition       | String | The definition of the video stream. Valid values: * FD: low definition   * LD: standard definition   * SD: high definition   * HD: ultra high definition   * OD: original quality   * 2K: 2K resolution   * 4K: 4K resolution                           |
| Specification    | String | The output specifications of a transcoded audio or video stream. For more information about this parameter, see the "Specification" section of the [Parameters for media assets](/intl.en-US/API Reference/Appendix/Parameters for media assets.md) topic.                                                                                                                                                                                                                                                      |
| Duration         | String | The duration of the video stream. Unit: seconds.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Encrypt          | Long   | Indicates whether the video stream is encrypted. Valid values: * 0: not encrypted   * 1: encrypted                                                                                                                                                                                                                                                                                                                           |
| EncryptType      | String | The type of encryption that was performed on the video stream. Valid values: * AliyunVoDEncryption: Alibaba Cloud proprietary cryptography   * HLSEncryption: HTTP-Live-Streaming (HLS) encryption                                                                                                                                                                                                                           |
| PlayURL          | String | The streaming URL of the video stream.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Format           | String | The format of the video stream.  If the media asset is a video file, the following valid values are included: * mp4   * m3u8    If the media asset is an audio-only file, the value is mp3.                                                                                                                                                                                                                  |
| Fps              | String | The frame rate of the video stream. Unit: frames per second.                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Size             | Long   | The size of the video. Unit: byte.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Width            | Long   | The width of the video. Unit: pixel.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Height           | Long   | The height of the video. Unit: pixel.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| StreamType       | String | The type of the media stream.  * If the media stream is a video stream, the value is video.    <!-- --> * If the media stream is an audio-only stream, the value is audio.                                                                                                                                                                                                                                  |
| JobId            | String | The ID of the job that was used to transcode the media stream. This ID uniquely identifies a media stream.                                                                                                                                                                                                                                                                                                                                                                                                                      |
| WatermarkId      | String | The ID of the watermark that is associated with the media stream.                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Status           | String | The status of the video stream. Valid values: * Normal: The video stream can be played.   * Invisible: The video stream is blocked.                                                                                                                                                                                                                                                                                          |
| NarrowBandType   | String | The type of Narrowband HD™. Valid values: * 0: regular transcoding   * 1.0: Narrowband HD™ 1.0   * 2.0: Narrowband HD™ 2.0    This parameter takes effect only when the definition of the built-in Narrowband HD™ 1.0 transcoding template is specified. For more information, see [TranscodeTemplate: the configurations of a transcoding template](#section-cme-uo6-1pk). |
| CreationTime     | String | The time when the media stream was created. The time is displayed in UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ModificationTime | String | The time when the media stream was last updated. The time is displayed in UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |



VideoMeta: the metadata of a video 
-------------------------------------------------------



|                                    Parameter                                     |  Type  |                Description                |
|----------------------------------------------------------------------------------|--------|-------------------------------------------|
| VideoId                                                                          | String | The ID of the video.                      |
| Title                                                                            | String | The title of the video.                   |
| Duration                                                                         | Float  | The duration of the video. Unit: seconds. |
| CoverURL                                                                         | String | The URL of the video thumbnail.           |
| [Status](/intl.en-US/API Reference/Appendix/Basic structures.md) | String | The status of the video.                  |



Status: the status of a video 
--------------------------------------------------



|     Value     |            Description            |                                                                                                                                                                                                                                                                    Remarks                                                                                                                                                                                                                                                                    |
|---------------|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Uploading     | The video is being uploaded.      | This is the initial status of a video. It indicates that the video is being uploaded.                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| UploadFail    | The video fails to be uploaded.   | This value is temporarily not used because videos are uploaded in resumable mode and ApsaraVideo VOD cannot determine whether a resumable upload fails.                                                                                                                                                                                                                                                                                                                                                                                       |
| UploadSucc    | The video is uploaded.            | N/A                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Transcoding   | The video is being transcoded.    | N/A                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| TranscodeFail | The video fails to be transcoded. | A transcoding failure is usually caused by an error in the mezzanine video file. To troubleshoot a transcoding failure, you can obtain the error message from the TranscodeComplete event notification. For more information, see [TranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/TranscodeComplete.md). If you have questions, submit a [ticket](https://account.alibabacloud.com/login/login.htm?oauth_callback=https%3A//ticket-intl.console.aliyun.com/%23/ticket/createIndex). |
| Checking      | The video is being reviewed.      | To specify that a video is reviewed before it is published, log on to the [ApsaraVideo VOD console](https://www.aliyun.com/product/vod?spm=5176.8142029.388261.421.78de76f4IhQkZa). In the left-side navigation pane, choose **Review** \> **Settings** . Set the Process parameter to **Review Before Publish** . Then, the status of a video changes to **Under Review** after the video is transcoded. In this case, the video can be played only in the ApsaraVideo VOD console.                                       |
| Blocked       | The video is blocked.             | A video that is being reviewed is blocked.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Normal        | The video can be played.          | A video in this state can be played.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ProduceFail   | The video fails to be produced.   | N/A                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |



Status: the status of an image 
---------------------------------------------------



|   Value    |           Description           |                                        Remarks                                         |
|------------|---------------------------------|----------------------------------------------------------------------------------------|
| Uploading  | The image is being uploaded.    | This is the initial status of an image. It indicates that the image is being uploaded. |
| Normal     | The image is uploaded.          | An image in this state is uploaded.                                                    |
| UploadFail | The image fails to be uploaded. | An image in this state fails to be uploaded.                                           |



Category: the information about a media asset category 
---------------------------------------------------------------------------



| Parameter |  Type  |                                               Description                                               |
|-----------|--------|---------------------------------------------------------------------------------------------------------|
| CateId    | Long   | The category ID of the video.                                                                           |
| CateName  | String | The name of the category. The value can be up to 64 bytes in length and is encoded in the UTF-8 format. |
| ParentId  | Long   | The ID of the parent category. The parent category ID of a level 1 category is -1.                      |
| Level     | Long   | The level of the category. A value of 0 indicates a level 1 category.                                   |



mezzanine: the information about a mezzanine file 
----------------------------------------------------------------------



|    Parameter    |                          Type                           |                                                                                              Description                                                                                               |
|-----------------|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VideoId         | String                                                  | The ID of the video.                                                                                                                                                                                   |
| FileName        | String                                                  | The name of the mezzanine file.                                                                                                                                                                        |
| Duration        | String                                                  | The duration of the mezzanine file. Unit: seconds.                                                                                                                                                     |
| Status          | String                                                  | The status of the mezzanine file.                                                                                                                                                                      |
| CreationTime    | String                                                  | The time when the mezzanine file was created. The time is displayed in UTC.                                                                                                                            |
| Height          | Long                                                    | The height of the mezzanine file. Unit: pixel.                                                                                                                                                         |
| Width           | Long                                                    | The width of the mezzanine file. Unit: pixel.                                                                                                                                                          |
| Fps             | String                                                  | The frame rate of the mezzanine file. Unit: frames per second.                                                                                                                                         |
| FileURL         | String                                                  | The URL of the mezzanine file.                                                                                                                                                                         |
| Bitrate         | String                                                  | The bitrate of the mezzanine file. Unit: Kbit/s.                                                                                                                                                       |
| Size            | Long                                                    | The size of the mezzanine file. Unit: byte.                                                                                                                                                            |
| OutputType      | String                                                  | The type of the streaming URL for the output file. Valid values: * oss: OSS URL   * cdn: CDN URL    |
| VideoStreamList | [VideoStream](#section-7n0-err-4h8)\[\] | The information about video streams.                                                                                                                                                                   |
| AudioStreamList | [AudioStream](#section-rxt-277-pec)\[\] | The information about audio streams.                                                                                                                                                                   |



VideoStream: the information about a video stream 
----------------------------------------------------------------------



| Parameter      | Type   | Description                                                                                                         |
|:---------------|:-------|:--------------------------------------------------------------------------------------------------------------------|
| Index          | String | The sequence number of the video stream. The value indicates the position of the video stream in all video streams. |
| CodecName      | String | The short name of the encoding format.                                                                              |
| CodecLongName  | String | The full name of the encoding format.                                                                               |
| Profile        | String | The codec profile.                                                                                                  |
| CodecTimeBase  | String | The codec time base.                                                                                                |
| CodecTagString | String | The tag string of the encoding format.                                                                              |
| CodecTag       | String | The tag of the encoding format.                                                                                     |
| Width          | Long   | The former number in the video resolution. The number indicates the video width.                                    |
| Height         | Long   | The latter number in the video resolution. The number indicates the video height.                                   |
| HasBFrames     | String | Indicates whether the video stream contains bidirectional frames (B-frames).                                        |
| Sar            | String | The sample aspect ratio (SAR).                                                                                      |
| Dar            | String | The display aspect ratio (DAR).                                                                                     |
| PixFmt         | String | The pixel format.                                                                                                   |
| Level          | String | The codec level.                                                                                                    |
| Fps            | String | The frame rate of the output file.                                                                                  |
| AvgFPS         | String | The average frame rate.                                                                                             |
| Timebase       | String | The time base.                                                                                                      |
| StartTime      | String | The start time of the video playback.                                                                               |
| Duration       | String | The duration of the video playback.                                                                                 |
| NumFrames      | String | The total number of frames.                                                                                         |
| Lang           | String | The language.                                                                                                       |
| Rotate         | String | The rotation angle of the video. Valid values: \[0,360).                                                            |



AudioStream: the information about an audio stream 
-----------------------------------------------------------------------



| Parameter      | Type   | Description                                                                                                         |
|:---------------|:-------|:--------------------------------------------------------------------------------------------------------------------|
| Index          | String | The sequence number of the audio stream. The value indicates the position of the audio stream in all audio streams. |
| CodecName      | String | The short name of the encoding format.                                                                              |
| CodecLongName  | String | The full name of the encoding format.                                                                               |
| CodecTimeBase  | String | The codec time base.                                                                                                |
| CodecTagString | String | The tag string of the encoding format.                                                                              |
| CodecTag       | String | The tag of the encoding format.                                                                                     |
| SampleFmt      | String | The sampling format.                                                                                                |
| SampleRate     | String | The sample rate.                                                                                                    |
| Channels       | String | The number of sound channels.                                                                                       |
| ChannelLayout  | String | The output layout of the sound channels.                                                                            |
| Timebase       | String | The time base.                                                                                                      |
| StartTime      | String | The start time of the audio playback.                                                                               |
| Duration       | String | The duration of the audio playback.                                                                                 |
| Bitrate        | String | The bitrate.                                                                                                        |
| NumFrames      | String | The total number of frames.                                                                                         |
| Lang           | String | The language.                                                                                                       |



Status: the status of a mezzanine file 
-----------------------------------------------------------



|   Value    |               Description                |                                            Remarks                                            |
|------------|------------------------------------------|-----------------------------------------------------------------------------------------------|
| Uploading  | The mezzanine file is being uploaded.    | This is the initial status of a mezzanine file. It indicates that the file is being uploaded. |
| Normal     | The mezzanine file is uploaded.          | A mezzanine file in this state is uploaded.                                                   |
| UploadFail | The mezzanine file fails to be uploaded. | A mezzanine file in this state fails to be uploaded.                                          |
| Deleted    | The mezzanine file is deleted.           | A mezzanine file in this state is deleted.                                                    |



LiveRecordVideo: the information about VOD files that are created from a live stream 
---------------------------------------------------------------------------------------------------------



| Parameter       | Type   | Description                         |
|:----------------|:-------|:------------------------------------|
| StreamName      | String | The name of the live stream.        |
| DomainName      | String | The domain name of the live stream. |
| AppName         | String | The name of the application.        |
| PlaylistId      | String | The ID of the playlist.             |
| RecordStartTime | String | The start time of the recording.    |
| RecordEndTime   | String | The end time of the recording.      |
| Video           | Video  | The information about the video.    |



TopPlayVideoStatis: the daily playback statistics on one of the top videos 
-----------------------------------------------------------------------------------------------



|  Parameter   |  Type  |                       Description                       |
|--------------|--------|---------------------------------------------------------|
| VideoId      | String | The ID of the video.                                    |
| PlayDuration | String | The playback duration of the video. Unit: milliseconds. |
| Title        | String | The title of the video.                                 |
| VV           | String | The number of video views.                              |
| UV           | String | The number of unique visitors.                          |



VideoPlayStatisDetail: the daily playback statistics on a specific video 
---------------------------------------------------------------------------------------------



|  Parameter   |  Type  |                             Description                              |
|--------------|--------|----------------------------------------------------------------------|
| Date         | String | The date in the yyyyMMdd format.  Example: 20170120. |
| PlayDuration | String | The playback duration of the video. Unit: milliseconds.              |
| Title        | String | The title of the video.                                              |
| VV           | String | The number of video views.                                           |
| UV           | String | The number of unique visitors.                                       |
| PlayRange    | String | The distribution of the playback duration.                           |



UserPlayStatisTotals: the statistics on total playbacks per day 
------------------------------------------------------------------------------------



|  Parameter   |  Type  |                             Description                              |
|--------------|--------|----------------------------------------------------------------------|
| Date         | String | The date in the yyyyMMdd format.  Example: 20170120. |
| PlayDuration | String | The playback duration of the video. Unit: milliseconds.              |
| PlayRange    | String | The distribution of the playback duration.                           |
| VV           | VV     | The total number of video views.                                     |
| UV           | UV     | The total number of unique visitors.                                 |



UserPlayStatisAvgs: the statistics on average playbacks per day 
------------------------------------------------------------------------------------



|    Parameter    |  Type  |                             Description                              |
|-----------------|--------|----------------------------------------------------------------------|
| Date            | String | The date in the yyyyMMdd format.  Example: 20170120. |
| AvgPlayDuration | String | The average playback duration of the video. Unit: milliseconds.      |
| AvgPlayCount    | String | The average number of video views.                                   |



VV 
-----------------------

Indicates the video view statistics on playbacks that use ApsaraVideo Player SDKs. 


| Parameter |  Type  |                                                        Description                                                        |
|-----------|--------|---------------------------------------------------------------------------------------------------------------------------|
| Android   | String | The total number of video views that is collected for videos that are played by using ApsaraVideo Player SDK for Android. |
| iOS       | String | The total number of video views that is collected for videos that are played by using ApsaraVideo Player SDK for iOS.     |
| Flash     | String | The total number of video views that is collected for videos that are played by using ApsaraVideo Player SDK for Flash.   |
| HTML5     | String | The total number of video views that is collected for videos that are played by using ApsaraVideo Player SDK for HTML5.   |



UV 
-----------------------

Indicates the unique visitor statistics on playbacks that use ApsaraVideo Player SDKs. 


| Parameter |  Type  |                                   Description                                   |
|-----------|--------|---------------------------------------------------------------------------------|
| Android   | String | The total number of unique visitors who use ApsaraVideo Player SDK for Android. |
| iOS       | String | The total number of unique visitors who use ApsaraVideo Player SDK for iOS.     |
| Flash     | String | The total number of unique visitors who use ApsaraVideo Player SDK for Flash.   |
| HTML5     | String | The total number of unique visitors who use ApsaraVideo Player SDK for HTML5.   |



EditingProject: the information about an online editing project 
------------------------------------------------------------------------------------



| Parameter    | Type   | Description                                                                                                                                                                                                                                                                        |
|:-------------|:-------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ProjectId    | String | The ID of the online editing project.                                                                                                                                                                                                                                              |
| Title        | String | The title of the online editing project.                                                                                                                                                                                                                                           |
| CreationTime | String | The time when the online editing project was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.  For example, a value of 2017-01-11T12:00:00Z indicates 20:00:00 (UTC+8) on January 11, 2017.       |
| ModifiedTime | String | The time when the online editing project was last modified. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.  For example, a value of 2017-01-11T12:00:00Z indicates 20:00:00 (UTC+8) on January 11, 2017. |
| Status       | String | The status of the online editing project.                                                                                                                                                                                                                                          |
| Description  | String | The description of the online editing project.                                                                                                                                                                                                                                     |
| Timeline     | String | The timeline of the online editing project, in the JSON format.                                                                                                                                                                                                                    |
| Duration     | String | The duration of the online editing project. The duration must be the same as that of the timeline.                                                                                                                                                                                 |
| CoverURL     | String | The thumbnail URL of the online editing project.                                                                                                                                                                                                                                   |



Timeline: the information about the timeline of an online editing project 
----------------------------------------------------------------------------------------------



| Parameter       | Type                                                   | Description                                                                                                                                                                                                                                                                             |
|:----------------|:-------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Id              | String                                                 | The ID of the online editing project.                                                                                                                                                                                                                                                   |
| Title           | String                                                 | The title of the online editing project.                                                                                                                                                                                                                                                |
| CreationTime    | String                                                 | The time when the timeline was created.                                                                                                                                                                                                                                                 |
| ModifiedTime    | String                                                 | The time when the timeline was last modified.                                                                                                                                                                                                                                           |
| Duration        | Float                                                  | The total duration of the timeline. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                     |
| CurrentRuler    | Float                                                  | The current ruler of the timeline.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                                                                                   |
| CurrentPosition | Float                                                  | The current position of the playhead for the online editing project. Unit: seconds. Specify a value accurate to four decimal places.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter. |
| VideoTracks     | [VideoTrack](#section-kea-b1n-9t4)\[\] | The video tracks.                                                                                                                                                                                                                                                                       |



VideoTrack: the information about a video track 
--------------------------------------------------------------------



|    Parameter    |                            Type                            |              Description               |
|-----------------|------------------------------------------------------------|----------------------------------------|
| Count           | Int                                                        | The total number of video track clips. |
| Duration        | String                                                     | The duration of the video track.       |
| VideoTrackClips | [VideoTrackClip](#section-48i-sdp-wqm)\[\] | The video track clips.                 |



VideoTrackClip: the information about a video track clip 
-----------------------------------------------------------------------------



| Parameter       | Type                                               | Description                                                                                                                                                                                                                                                                                                  |
|:----------------|:---------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Id              | String                                             | The ID of the video track clip.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.  If the timeline is used to edit data, you must set this parameter to a unique value within the timeline. |
| VideoId         | String                                             | The video ID of the video track clip.                                                                                                                                                                                                                                                                        |
| Type            | String                                             | The type of the video track clip. Valid values: * Video: video   * Image: image    Default value: Video.                                                                                                  |
| Title           | String                                             | The title of the video track clip. The title must be the same as that of the video.                                                                                                                                                                                                                          |
| Index           | Int                                                | The sequence number of the video track clip in the timeline. Sequence numbers start from zero.                                                                                                                                                                                                               |
| CutFlag         | Boolean                                            | Specifies whether the video track clip is cropped. Valid values: true and false.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                                                          |
| TextFlag        | Boolean                                            | Specifies whether banner text is added to the video track clip. Valid values: true and false.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                                             |
| DeWatermarkFlag | Boolean                                            | Specifies whether a part of the video track clip is masked. Valid values: true and false.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                                                 |
| URL             | String                                             | The streaming URL of the stream that is used to edit the video track clip.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                                                                |
| CoverURL        | String                                             | The thumbnail URL of the video track clip. By default, this thumbnail URL is the same as that of the video.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                               |
| SpriteURLs      | String                                             | The sprite snapshot URLs of the video track clip. Separate multiple URLs with commas (,).  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                                                 |
| Width           | Int                                                | The width of the stream that is used to edit the video track clip. Unit: pixel.  If the timeline is used only for video production, not for data storage during editing, and no effect, such as banner text or masking, is added, you do not need to set this parameter.                     |
| Height          | Int                                                | The height of the stream that is used to edit the video track clip. Unit: pixel.  If the timeline is used only for video production, not for data storage during editing, and no effect, such as banner text or masking, is added, you do not need to set this parameter.                    |
| Fps             | Float                                              | The frame rate of the video track clip.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                                                                                                   |
| Bitrate         | Float                                              | The bitrate of the stream that is used to edit the video track clip.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                                                                                      |
| In              | Float                                              | The start time of the video track clip in the video. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                         |
| Out             | Float                                              | The end time of the video track clip in the video. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                           |
| Duration        | Float                                              | The duration of the video track clip. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                                        |
| VirginDuration  | Float                                              | The total duration of the video to which the video track clip belongs. Unit: seconds. Specify a value accurate to four decimal places.  If the timeline is used only for video production and not for data storage during editing, you do not need to set this parameter.                    |
| TimelineIn      | Float                                              | The start time of the video track clip in the timeline. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                      |
| TimelineOut     | Float                                              | The end time of the video track clip in the timeline. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                        |
| Effects         | [Effect](#section-i3j-wna-gxo)\[\] | The effects to be added to the video track clip.                                                                                                                                                                                                                                                             |



Effect: the information about an effect 
------------------------------------------------------------



|    Parameter     |                       Type                       |                                                                                                                                                                                                                                                                                                                                       Description                                                                                                                                                                                                                                                                                                                                        |
|------------------|--------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type             | String                                           | The type of the effect. Valid values: * Text: Add banner text to the video track clip.   * DeWatermark: Mask a specific part of the video track clip.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Name             | String                                           | The name of the effect.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| SubType          | String                                           | The subtype of the effect.  If the Type parameter is set to DeWatermark, set this parameter to Delogo_Blur.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| In               | Float                                            | The start time of the effect to be added to the video track clip. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Out              | Float                                            | The end time of the effect to be added to the video track clip. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| TimelineIn       | Float                                            | The start time of the effect in the timeline. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| TimelineOut      | Float                                            | The end time of the effect in the timeline. Unit: seconds. Specify a value accurate to four decimal places.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| X                | String                                           | The X coordinate of the effect. The coordinate origin is the upper-left corner of the video image. The value can be an integer or a decimal number. * If the value is an integer, the value ranges from 8 to 4096 and indicates a pixel value, and the unit is pixel.   * If the value is a decimal number, the value ranges between 0 and 1 and indicates the ratio of the pixel value to the width in pixels in the resolution of the output video image. The decimal number can be accurate to four decimal places, such as 0.9999. Excessive digits are automatically deleted.    |
| Y                | String                                           | The Y coordinate of the effect. The coordinate origin is the upper-left corner of the video image. The value can be an integer or a decimal number. * If the value is an integer, the value ranges from 8 to 4096 and indicates a pixel value, and the unit is pixel.   * If the value is a decimal number, the value ranges between 0 and 1 and indicates the ratio of the pixel value to the width in pixels in the resolution of the output video image. The decimal number can be accurate to four decimal places, such as 0.9999. Excessive digits are automatically deleted.    |
| Width            | Int                                              | The width of the area where the effect is to be added. The value can be an integer or a decimal number. * If the value is an integer, the value ranges from 8 to 4096 and indicates a pixel value, and the unit is pixel.   * If the value is a decimal number, the value ranges between 0 and 1 and indicates the ratio of the pixel value to the width in pixels in the resolution of the output video image. The decimal number can be accurate to four decimal places, such as 0.9999. Excessive digits are automatically deleted.                                                |
| Height           | Int                                              | The height of the area where the effect is to be added. The value can be an integer or a decimal number. * If the value is an integer, the value ranges from 8 to 4096 and indicates a pixel value, and the unit is pixel.   * If the value is a decimal number, the value ranges between 0 and 1 and indicates the ratio of the pixel value to the width in pixels in the resolution of the output video image. The decimal number can be accurate to four decimal places, such as 0.9999. Excessive digits are automatically deleted.                                               |
| FEWidth          | Float                                            | The displayed width of the video image during editing. Unit: pixel.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| FEHeight         | Float                                            | The displayed height of the video image during editing. Unit: pixel.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Font             | String                                           | The font. Set the value to SimSun.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| FontFace         | [FontFace](#section-egk-sn7-e5w) | The appearance of the font.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| FontColor        | String                                           | The color of the font, in the hexadecimal format. The value must start with a number sign (#). Example: #ffffff.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| FontSize         | Int                                              | The size of the font.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| FontColorOpacity | Float                                            | The transparency of the font. Valid values: 0 to 1. A value of 1 indicates that the font is not transparent. A value of 0 indicates that the font is completely transparent.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Content          | String                                           | The content of the banner text.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |



FontFace: font style 
-----------------------------------------



| Parameter |  Type   |                Description                |
|-----------|---------|-------------------------------------------|
| Bold      | Boolean | Specifies whether the font is bold.       |
| Italic    | Boolean | Specifies whether the font is italic.     |
| Underline | Boolean | Specifies whether the font is underlined. |



MediaMetadata: the metadata of a media resource 
--------------------------------------------------------------------



| Parameter   | Type   | Description                                                                                                                                                                                                                                                                                                                  |
|:------------|:-------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Title       | String | The title of the produced video. The value can be up to 128 bytes in length and must be encoded in the UTF-8 format.                                                                                                                                                                                                         |
| Description | String | The description of the produced video. The value can be up to 1,024 bytes in length and must be encoded in the UTF-8 format.                                                                                                                                                                                                 |
| CoverURL    | String | The URL of the custom thumbnail for the produced video.                                                                                                                                                                                                                                                                      |
| CateId      | String | The category ID of the produced video. To view the category ID, log on to the [ApsaraVideo VOD console](https://www.aliyun.com/product/vod?spm=5176.8142029.388261.421.78de76f4IhQkZa). In the left-side navigation pane, choose **Configuration Management** \> **Media Management** \> **Categories** . |
| Tags        | String | The tags of the produced video. Each tag name can be up to 32 bytes in length. You can specify a maximum of 16 tags. Separate multiple tags with commas (,). The string must be encoded in the UTF-8 format.                                                                                                                 |



ProduceConfig: the configurations of video production 
--------------------------------------------------------------------------



| Parameter       | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|:----------------|:--------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TemplateGroupId | String  | The ID of the transcoding template group that is used to transcode produced videos. The produced video files are used as the mezzanine files for transcoding. This transcoding process is similar to that is performed after a file is uploaded.  This parameter is optional. If you do not set this parameter, ApsaraVideo VOD uses the default template group for transcoding. If you set this parameter, ApsaraVideo VOD uses the specified template group for transcoding. To view the template group ID, go to the Transcode page in the ApsaraVideo VOD console.                                                                                                                                                                                                                                                                                               |
| TemplateId      | String  | The ID of the template that is used for video production. The produced media file is used as the mezzanine file of the media resources. This parameter is optional. If you do not set this parameter, ApsaraVideo VOD uses the built-in template of the online editing service for video production.  If a video file is produced, the encoding format is H.264, and the container format is MP4.  If you want to set this parameter to meet your business requirements, for example, to produce animated stickers, implement intelligent subtitle production, edit videos based on the M3U8 playlists, or use custom production parameters, submit a [ticket](https://account.alibabacloud.com/login/login.htm?oauth_callback=https%3A//ticket-intl.console.aliyun.com/%23/ticket/createIndex) to apply for the specified template. |
| Width           | Integer | The width in the output resolution of the produced video. Unit: pixel.  This parameter is optional. The default width is the maximum resolution width of the mezzanine files of the video track clips that are used in the timeline.  For example, three video track clips are used in the timeline. The resolutions of their mezzanine files are 1280 × 720 pixels, 1920 × 1080 pixels, and 720 × 1280 pixels. In this case, the output resolution of the produced video is 1920 × 1280 pixels.                                                                                                                                                                                                                                                                                                                                                     |
| Height          | Integer | The height in the output resolution of the produced video. Unit: pixel.  This parameter is optional. The default height is the maximum resolution height of the mezzanine files of the video track clips that are used in the timeline.  For example, three video track clips are used in the timeline. The resolutions of their mezzanine files are 1280 × 720 pixels, 1920 × 1080 pixels, and 720 × 1280 pixels. In this case, the output resolution of the produced video is 1920 × 1280 pixels.                                                                                                                                                                                                                                                                                                                                                  |
| StorageLocation | String  | The storage location of the produced file. This parameter is required if the produced file is stored in a region other than the China (Shanghai) region.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |



Material: the information about a material for an online editing project 
---------------------------------------------------------------------------------------------

**Note**

Materials for an online editing project can be materials from media assets or videos in the media library.


|  Parameter   |    Type    |                                        Description                                         |
|--------------|------------|--------------------------------------------------------------------------------------------|
| MaterialId   | String     | The ID of the material.                                                                    |
| Title        | String     | The title of the material.                                                                 |
| Description  | String     | The description of the material.                                                           |
| Duration     | Float      | The duration of the material. Unit: seconds. The value is accurate to four decimal places. |
| CoverURL     | String     | The thumbnail URL of the material.                                                         |
| Status       | String     | The status of the material.                                                                |
| CreationTime | String     | The time when the material was created. The time is displayed in UTC.                      |
| Size         | Long       | The size of the mezzanine file. Unit: byte.                                                |
| CateId       | Long       | The category ID of the material.                                                           |
| CateName     | String     | The category name of the material.                                                         |
| Tags         | String     | The tags of the material. Multiple tags are separated by commas (,).                       |
| Snapshots    | String\[\] | The URLs of material snapshots. The value is an array.                                     |
| Sprites      | String\[\] | The URLs of material sprite snapshots. The value is an array.                              |



ProjectStatus: the status of an online editing project 
---------------------------------------------------------------------------



|    Value     |                 Description                 |                         Remarks                          |
|--------------|---------------------------------------------|----------------------------------------------------------|
| Normal       | The online editing project is being edited. | This is the initial status of an online editing project. |
| Producing    | Video production is being performed.        | N/A                                                      |
| Produced     | Video production is successful.             | N/A                                                      |
| ProduceFaile | Video production fails.                     | N/A                                                      |



TranscodeJob: the information about a transcoding job 
--------------------------------------------------------------------------



| Parameter |  Type  |    Description     |
|-----------|--------|--------------------|
| JobId     | String | The ID of the job. |



SnapshotJob: the information about a snapshot job 
----------------------------------------------------------------------



| Parameter |  Type  |    Description     |
|-----------|--------|--------------------|
| JobId     | String | The ID of the job. |



MediaSnapshot: media snapshot data 
-------------------------------------------------------



|  Parameter   |                         Type                         |                                Description                                |
|--------------|------------------------------------------------------|---------------------------------------------------------------------------|
| JobId        | String                                               | The ID of the snapshot job.                                               |
| CreationTime | String                                               | The time when the snapshot job was created. The time is displayed in UTC. |
| Total        | Long                                                 | The total number of snapshots.                                            |
| Regular      | String                                               | The rule used to generate snapshot URLs.                                  |
| Snapshots    | [Snapshot](#section-qx8-nsy-mkr)\[\] | The snapshot data.                                                        |



Snapshot: the information about a snapshot 
---------------------------------------------------------------



| Parameter |  Type  |        Description         |
|-----------|--------|----------------------------|
| Index     | String | The index of the snapshot. |
| Url       | String | The URL of the snapshot.   |



WatermarkInfo: the information about a watermark 
---------------------------------------------------------------------




| Parameter       | Type                                                                                                     | Required | Description                                                                                                                                                                                                                                                                |
|:----------------|:---------------------------------------------------------------------------------------------------------|:---------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CreationTime    | String                                                                                                   | Yes      | The time when the watermark was created.                                                                                                                                                                                                                                   |
| Name            | String                                                                                                   | Yes      | The name of the watermark.                                                                                                                                                                                                                                                 |
| IsDefault       | String                                                                                                   | Yes      | Indicates whether the watermark is the default one. Valid values: * Default: The watermark is the default one.   * NotDefault: The watermark is not the default one.    |
| Type            | String                                                                                                   | Yes      | The type of the watermark. Valid values: * Image: image   * Text: text                                                                                                  |
| WatermarkId     | String                                                                                                   | Yes      | The ID of the watermark.                                                                                                                                                                                                                                                   |
| FileUrl         | String                                                                                                   | No       | The OSS URL or CDN URL of the watermark file. This parameter does not apply to text watermarks.                                                                                                                                                                            |
| WatermarkConfig | [WatermarkConfig](/intl.en-US/API Reference/Appendix/Parameters for media processing.md) | Yes      | The configurations such as the position and effect of the text watermark or image watermark. The value must be a JSON string.                                                                                                                                              |



VodTemplateInfo: the information about a template 
----------------------------------------------------------------------



| Parameter      | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|:---------------|:-------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name           | String | The name of the template.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| VodTemplateId  | String | The ID of the template.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| TemplateType   | String | The type of the template. Valid values:						 * Snapshot: snapshot template   * DynamicImage: animated sticker template                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| IsDefault      | String | Indicates whether the template is the default one. Valid values: * Default: The template is the default one.   * NotDefault: The template is not the default one.                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| TemplateConfig | JSON   | The detailed configurations of the template. The value is a JSON string.						 * For more information about the configurations of a snapshot template, see the [SnapshotTemplateConfig: specifies the configurations for a snapshot template](/intl.en-US/API Reference/Appendix/Parameters for media processing.md) section of the Parameters for media processing topic.   * For more information about the configurations of an animated sticker template, see [DynamicImageTemplateConfig: the configurations of an animated sticker template](#section-k00-mpm-ejv).    |
| CreationTime   | String | The time when the template was created. The time is displayed in UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ModifyTime     | String | The time when the template was last modified. The time is displayed in UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |



DynamicImageTemplateConfig: the configurations of an animated sticker template 
---------------------------------------------------------------------------------------------------



| Parameter       | Type                                              | Description                                                                                                                                                                                                                                                                                                    |
|:----------------|:--------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name            | String                                            | The name of the template.                                                                                                                                                                                                                                                                                      |
| Video           | [Video](#section-n9u-4ke-rff)     | The image configurations of animated stickers.                                                                                                                                                                                                                                                                 |
| Container       | [Container](#section-czf-234-0cd) | The format of animated stickers.                                                                                                                                                                                                                                                                               |
| Clip            | [Clip](#section-9wk-d8w-mxb)      | The configurations used to generate an animated sticker by cropping a video.                                                                                                                                                                                                                                   |
| SetDefaultCover | String                                            | Indicates whether the animated sticker is used as the thumbnail. Valid values:					 * true: The animated sticker is used as the thumbnail.   * false: The animated sticker is not used as the thumbnail.    |



Video: the image configurations of an animated sticker 
---------------------------------------------------------------------------



| Parameter | Type   | Required | Description                                                     |
|:----------|:-------|:---------|:----------------------------------------------------------------|
| Width     | String | Yes      | The width of the animated sticker. Valid values: \[128,4096\].  |
| Height    | String | Yes      | The height of the animated sticker. Valid values: \[128,4096\]. |
| Fps       | String | Yes      | The frame rate of the animated sticker. Valid values: (0,60\]   |



Container: the format of an animated sticker 
-----------------------------------------------------------------



| Parameter | Type   | Required | Description                                                     |
|:----------|:-------|:---------|:----------------------------------------------------------------|
| Format    | String | Yes      | The format of the animated sticker. Valid values: webp and gif. |



Clip: the configurations used to generate an animated sticker by cropping a video 
------------------------------------------------------------------------------------------------------



| Parameter | Type                                             | Required | Description                                                                                    |
|:----------|:-------------------------------------------------|:---------|:-----------------------------------------------------------------------------------------------|
| TimeSpan  | [TimeSpan](#section-ci2-v8c-ehf) | Yes      | The configurations of the time span used to generate the animated sticker by cropping a video. |



TimeSpan: the configurations of the time span used to generate an animated sticker by cropping a video 
---------------------------------------------------------------------------------------------------------------------------



| Parameter | Type   | Required | Description                                                                                                                                                                                                                                                                                                                                                                      |
|:----------|:-------|:---------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Seek      | String | Yes      | The start time of the captured part of the video.  * Format 1: sssss\[.SSS\].Valid values: \[0.000,86399.999\].  Example: 12000.55.   * Format 2: hh:mm:ss\[.SSS\].Valid values: \[00:00:00.000,23:59:59.999\]. Example: 00:00:05.003.                        |
| Duration  | String | Yes      | The duration of the captured part of the video.  * Format 1: sssss\[.SSS\].Valid values: \[0.000,86399.999\].  Example: 12000.55.   * Format 2: hh:mm:ss\[.SSS\].Valid values: \[00:00:00.000,23:59:59.999\]. Example: 00:00:05.003.                          |
| End       | String | Yes      | The duration of the remaining part of the video after video cropping.  * Format 1: sssss\[.SSS\].Valid values: \[0.000,86399.999\].  Example: 12000.55.   * Format 2: hh:mm:ss\[.SSS\].Valid values: \[00:00:00.000,23:59:59.999\]. Example: 00:00:05.003.    |



TranscodeTemplateGroup: the information about a transcoding template group 
-----------------------------------------------------------------------------------------------



| Parameter                | Type                                                          | Required | Description                                                                                                                                                                                                                                                                                                           |
|:-------------------------|:--------------------------------------------------------------|:---------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name                     | String                                                        | Yes      | The name of the transcoding template group.                                                                                                                                                                                                                                                                           |
| TranscodeTemplateGroupId | String                                                        | Yes      | The ID of the transcoding template group.                                                                                                                                                                                                                                                                             |
| IsDefault                | String                                                        | Yes      | Indicates whether the transcoding template group is the default one.						 * Default: The transcoding template group is the default one.   * NotDefault: The transcoding template group is not the default one.    |
| CreationTime             | String                                                        | Yes      | The time when the transcoding template group was created.                                                                                                                                                                                                                                                             |
| ModifyTime               | String                                                        | Yes      | The time when the transcoding template group was last modified.                                                                                                                                                                                                                                                       |
| TranscodeTemplateList    | [TranscodeTemplate](#section-cme-uo6-1pk)\[\] | Yes      | The information about the transcoding templates.                                                                                                                                                                                                                                                                      |



TranscodeTemplate: the configurations of a transcoding template 
------------------------------------------------------------------------------------



| Parameter            | Type                                                   | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|:---------------------|:-------------------------------------------------------|:---------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type                 | String                                                 | No       | The type of the transcoding template. Valid values:							 * Normal: regular transcoding template  The [PackageSetting](#section-i06-ofo-f1o) parameter cannot be set for this type of template.   * VideoPackage: video stream packaging template  If this type of template is used, ApsaraVideo VOD transcodes a video into video streams in different bitrates and packages these video streams with a file. You must set the [PackageSetting](#section-i06-ofo-f1o) parameter for this type of template.   * SubtitlePackage: subtitle packaging template  If this type of template is used, ApsaraVideo VOD adds the subtitle information to the output file that is generated by packaging the multi-bitrate video streams of the corresponding video. You must set the [PackageSetting](#section-i06-ofo-f1o) parameter for a subtitle packaging template and associate the subtitle packaging template with a video stream packaging template. You can configure only one subtitle packaging template in a template group.    Default value: Normal.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Video                | [Video](#section-qkk-c5l-0x0)          | Yes      | The transcoding configurations of the video stream. The value must be a JSON string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Audio                | [Audio](#section-j4n-fid-3j1)          | Yes      | The transcoding configurations of the audio stream. The value must be a JSON string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Definition           | String                                                 | Yes      | The definition of the transcoding template. Valid values for the definition of a regular transcoding template: * LD: low definition.   * SD: standard definition.   * HD: high definition.   * FHD: ultra high definition.   * OD: original quality. This value is used for [container format conversion](/intl.en-US/Introduction/Terms.md).   * 2K   * 4K   * SQ: standard sound quality.   * HQ: high sound quality.    **Note** * This parameter specifies the definition that is configured for the transcoding template and does not specify the actual resolution range of a transcoded video. For more information about the mappings between template definitions and output video resolutions, see the "Specifications" section of the [Parameters for media assets](/intl.en-US/API Reference/Appendix/Parameters for media assets.md) topic.   * The template definition does not affect transcoding fees. For more information about transcoding fees, see the "Transcoding plans of ApsaraVideo VOD" section of the [Resource plans]() topic.    Valid values for the definition of a Narrowband HD™ 1.0 transcoding template: * LD-NBV1: low definition   * SD-NBV1: standard definition   * HD-NBV1: high definition   * FHD-NBV1: ultra high definition   * 2K-NBV1   * 4K-NBV    **Note** * You cannot change the definition of a transcoding template.   * You cannot modify the system parameters of Narrowband HD™ 1.0 transcoding templates, such as the video resolution, audio resolution, and bitrate. For more information about the parameters, see the "Narrowband HD" section of the [Audio and video transcoding](/intl.en-US/Developer Guide/Media processing/Audio and video transcoding.md) topic.   * You can create only Narrowband HD™ 1.0 transcoding templates that support the FLV, M3U8 (HLS), and MP4 output formats.    |
| Container            | [Container](#section-czf-234-0cd)      | Yes      | The format of the container that is used to encapsulate audio and video streams. The value must be a JSON string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| MuxConfig            | [MuxConfig](#section-djh-b25-ohr)      | No       | The transcoding segment configuration. You must set this parameter if the Format parameter is set to HLS. The value must be a JSON string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| TransConfig          | [TransConfig](#section-nym-24f-ogv)    | No       | The conditional transcoding configurations. You can set this parameter if you need to determine the basic logic based on the bitrate and resolution of the mezzanine file before the transcoded video is generated. The value must be a JSON string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| TranscodeFileRegular | String                                                 | No       | The custom path used to store the output files.  **Note** * The following wildcards are supported: {MediaId}, {JobId}, and {PlayDefinition}. The MediaId parameter indicates the video ID. The JobId parameter indicates the transcoding job ID. The PlayDefinition parameter indicates the definition that is returned after the [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md) operation is called.   * The value can contain only digits, characters, braces {}, slashes (/), hyphens (-), and underscores (_). The value can be up to 128 characters in length.   * The value must start with {MediaId}.    **Configuration example**  {MediaId}/watermark-{PlayDefinition}: During transcoding, ApsaraVideo VOD replaces {MediaId} with the video ID and {PlayDefinition} with the definition. For example, the video ID can be 8ff5cc93f6da4079a47a77bf71d, and the definition can be fd.  **Output path example** 8ff5cc93f6da4079a47a77bf71d/watermark-fd.mp4: ApsaraVideo VOD automatically adds the file name extension, such as .mp4, .m3u8, or .flv.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Clip                 | [Clip](#section-9wk-d8w-mxb)           | No       | The video cropping configurations. The value must be a JSON string.  For example, you can set this parameter to extract 5 seconds of content from a video to generate a new video.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Rotate               | String                                                 | No       | The rotation angle of the video. Valid values: \[0,360\].  For example, if you set this parameter to 180, the video image is turned upside down.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| EncryptSetting       | [EncryptSetting](#section-2kv-j9d-4p6) | No       | The encryption configuration for transcoding.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| PackageSetting       | [PackageSetting](#section-i06-ofo-f1o) | No       | The packaging configurations. Only HLS packaging and Dynamic Adaptive Streaming over HTTP (DASH) packaging are supported. The value must be a JSON string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| SubtitleList         | [SubtitleConfig](#section-44w-bgt-5v9) | No       | The subtitle configurations. The value must be a JSON string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| WatermarkIds         | String\[\]                                             | No       | The ID of the associated watermark. A maximum of four watermark IDs are supported. USER_DEFAULT_WATERMARK indicates the ID of the default watermark.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| TranscodeTemplateId  | String                                                 | No       | The ID of the transcoding template. You must set this parameter when you modify a transcoding template.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| TemplateName         | String                                                 | No       | The name of the transcoding template. You must set this parameter when you create a transcoding template.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |



**Example of the TranscodeTemplate parameter** 

    {
            "Type":"VideoPackage",
            "Video":{
                    "Codec":"H.264",
                    "Bitrate":"900",
                    "Width":"960",
                    "Remove":"false",
                    "Fps":"30"
            },
            "Audio":{
                    "Codec":"AAC",
                    "Bitrate":"128",
                    "Samplerate":"44100"
            },
            "Container":{
                    "Format":"m3u8"
            },
            "MuxConfig":{
                    "Segment":{
                            "Duration":"6"
                    }
            },
            "EncryptSetting":{
                    "EncryptType":"AliyunVoDEncryption"
            },
            "PackageSetting":{
                    "PackageType":"HLSPackage"
                    "PackageConfig":{
                            "BandWidth":"900000"
                    }
            },
           "SubtitleUrl": "http://outin-40564284ef058b2163e1403e7.oss-cn-shanghai.aliyuncs.com/subtitles/c737f-14f1-4364-b107-d5f7f8edde0e-cn.ass",
            "CharEncode": "UTF-8",
            "WatermarkIds":["USER_DEFAULT_WATERMARK","ddddddddd"],
            "Definition":"SD",
            "TemplateName":"test"
    }
                            



Video: the transcoding configurations of a video stream 
----------------------------------------------------------------------------

**Note**

* Unless otherwise required, you need only to set the Codec, Bitrate, Height, and Width parameters and set the Remove parameter to false.

  

* We recommend that you set only one of the Width and Height parameters for the output video file. This ensures that the aspect ratio of the output video file is the same as that of the mezzanine file.

  





| Parameter     | Type   | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|:--------------|:-------|:---------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Codec         | String | Yes      | The encoding format of the video. Valid values: H.264 and H.265.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Remove        | String | Yes      | Specifies whether to delete the video stream. Valid values: * true: Delete the video stream from the transcoded video file.   * false: Retain the video stream for the transcoded video file.    Default value: false.                                                                                                                                                                                                                                                                                                                                                                                                    |
| Bitrate       | String | No       | The bitrate of the output video file. If you do not set this parameter, the bitrate is specified based on the value of the Crf parameter. Unit: Kbit/s. 		Valid values: \[10,50000\].                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Height        | String | No       | The image height of the output video file. The value must be a multiple of 2. If you do not set this parameter, the image height of the mezzanine file is used. Unit: pixel. Valid values: \[128,4096\].                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Width         | String | No       | The image width of the output video file. The value must be a multiple of 2. If you do not set this parameter, the image width of the mezzanine file is used. Unit: pixel. Valid values: \[128,4096\].                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Fps           | String | No       | The frame rate of the output video file. If you do not set this parameter, the frame rate of the mezzanine file is used. Unit: frames per second. Valid values: (0,60\].                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Gop           | String | No       | The size of a group of pictures (GOP). Valid values: \[1,100000\].                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| LongShortMode | String | No       | Specifies whether to enable auto-rotate screen, namely, the long-short side mode. The image width of the output video file corresponds to the long side of the mezzanine file or the image height of the mezzanine file in portrait mode. The image height of the output video file corresponds to the short side of the mezzanine file or the image width of the mezzanine file in portrait mode. 					Valid values: * true: Enable auto-rotate screen.   * false: Disable auto-rotate screen.    Default value: true. This feature is applicable to videos in portrait mode. We recommend that you enable this feature. |
| Crf           | String | No       | The bitrate quality control factor. If you set this parameter, the Bitrate parameter is invalid. A greater value indicates the poorer image quality of the output video file and a smaller file size. A smaller value indicates the better image quality of the output video file, a larger file size, and a longer transcoding duration. Valid values: \[0,51\].  Default value: 26. We recommend that you do not modify this parameter.                                                                                                                                                                                                                                                                    |
| Profile       | String | No       | The codec profile. Valid values: * baseline: applicable to mobile devices.   * main: applicable to standard-definition devices.   * high: applicable to high-definition devices.    Default value: high. This parameter is valid only when H.264 encoding is performed.  **Best practices**  If multiple definitions exist, we recommend that you set this parameter to baseline for the lowest definition to ensure normal playback on low-end devices. Set this parameter to main or high for other definitions.                                       |
| Preset        | String | No       | The preset video algorithm. Valid values: veryfast, fast, medium, slow, and slower.  Default value: medium. This parameter is valid only when H.264 encoding is performed. We recommend that you do not modify this parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ScanMode      | String | No       | The scan mode. Valid values: * interlaced: interlaced scan   * progressive: progressive scan                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Bufsize       | String | No       | The size of the buffer. Unit: KB. Valid values: \[1000,128000\].  Default value: 6000.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Maxrate       | String | No       | The maximum video bitrate. Unit: Kbit/s. Valid values: \[1000,50000\].                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| PixFmt        | String | No       | The pixel format for video color encoding. Valid values: standard pixel formats such as yuv420p and yuvj420p.  Default value: yuv420p or the original color format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |



**Example of the Video parameter** 

    {
            "Codec":"H.264",
            "Bitrate":"128",
            "Remove":"false",
            "Width":"640",
            "Fps":"30"
    }



Audio: the transcoding configurations of an audio stream 
-----------------------------------------------------------------------------

**Note**

Unless otherwise required, you need only to set the Codec and Bitrate parameters and set the Remove parameter to false.


| Parameter  | Type                                           | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                       |
|:-----------|:-----------------------------------------------|:---------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Codec      | String                                         | Yes      | The encoding format of the audio file. Valid values: AAC and MP3.                                                                                                                                                                                                                                                                                                                                                 |
| Bitrate    | String                                         | Yes      | The bitrate of the output audio file. Unit: Kbit/s. Valid values: \[8,1000\].                                                                                                                                                                                                                                                                                                                                     |
| Remove     | String                                         | Yes      | Specifies whether to delete the audio stream. Valid values: * true: Delete the audio stream from the output audio file.   * false: Retain the audio stream for the output audio file.    Default value: false.                                                                                                 |
| Samplerate | String                                         | Yes      | The sample rate. Unit: Hz. Valid values: 22050, 32000, 44100, 48000, and 96000.  Default value: 44100.  If the container format for the video files is FLV and the encoding format for the audio files is MP3, this parameter cannot be set to 32000, 48000, or 96000.  If the encoding format for the audio files is MP3, this parameter cannot be set to 96000. |
| Channels   | String                                         | No       | The number of sound channels. Default value: 2.  * If the Codec parameter is set to MP3, this parameter can be set only to 1 or 2.   * If the Codec parameter is set to AAC, this parameter can be set only to 1, 2, 4, 5, 6, or 8.                                                                            |
| Profile    | String                                         | No       | The codec profile of the audio file. Valid values when the Codec parameter is set to AAC: aac_low, aac_he, aac_he_v2, aac_ld, and aac_eld.                                                                                                                                                                                                                                                                        |
| Volume     | [Volume](#section-zjs-nhv-ibt) | No       | The volume.                                                                                                                                                                                                                                                                                                                                                                                                       |



**Example of the Audio parameter** 

    {
            "Codec":"AAC",
            "Bitrate":"128",
            "Remove":"false",
            "Samplerate":"44100"
    }



Container: the container format 
----------------------------------------------------



| Parameter | Type   | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                 |
|:----------|:-------|:---------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Format    | String | Yes      | The container format. 			 * For video transcoding, this parameter can be set to flv, mp4, or HLS (m3u8 and ts).   * For audio transcoding, this parameter can be set to mp3 or mp4.   * If this parameter is set to flv, the Codec parameter cannot be set to H.265.    |



**Example of the Container parameter** 

    {
            "Format":"mp4"
    }



MuxConfig: the segment configuration for HLS 
-----------------------------------------------------------------

**Note**

You must set this parameter if the container format is M3U8.


| Parameter | Type                                            | Required | Description                                                 |
|:----------|:------------------------------------------------|:---------|:------------------------------------------------------------|
| Segment   | [Segment](#section-z45-c8n-w3q) | Yes      | The segment configuration. The value must be a JSON object. |



Segment: the configuration of a segment 
------------------------------------------------------------



| Parameter | Type   | Required | Description                                                                                                                                       |
|:----------|:-------|:---------|:--------------------------------------------------------------------------------------------------------------------------------------------------|
| Duration  | String | Yes      | The duration of the TS segment. The value must be an integer. Valid values: \[1,60\]. Unit: seconds.  Example: {"Duration":"10"}. |



**Example of the MuxConfig parameter** 

    {
            "Segment":{
                    "Duration":"10"
            }
    }



TransConfig: conditional transcoding configurations 
------------------------------------------------------------------------



| Parameter               | Type   | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|:------------------------|:-------|:---------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TransMode               | String | No       | The transcoding mode. Valid values: onepass, twopass, and CBR. Default value: onepass.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| IsCheckReso             | String | No       | Specifies whether to check the resolution of the mezzanine file. Then, ApsaraVideo VOD determines whether to use the resolution of the mezzanine file for transcoding based on the check result. Valid values: * true: Check the resolution of the mezzanine file. If ApsaraVideo VOD determines that the resolution of the output file is higher than the resolution of the mezzanine file based on the width or height, the resolution of the mezzanine file is retained after transcoding.   * false: Do not check the resolution of the mezzanine file.    Default value: false.                                           |
| IsCheckResoFail         | String | No       | Specifies whether to check the resolution of the mezzanine file for a transcoding failure. Valid values: * true: Check the resolution of the mezzanine file. If ApsaraVideo VOD determines that the resolution of the output file is higher than the resolution of the mezzanine file based on the width or height, an error that indicates a transcoding failure is returned.   * false: Do not check the resolution of the mezzanine file.    Default value: false.                                                                                                                                                          |
| IsCheckVideoBitrate     | String | No       | Specifies whether to check the video stream bitrate of the mezzanine file. Then, ApsaraVideo VOD determines whether to use the video stream bitrate of the mezzanine file for transcoding based on the check result. Valid values: * true: Check the video stream bitrate of the mezzanine file. If ApsaraVideo VOD determines that the video stream bitrate of the output file is greater than the video stream bitrate of the mezzanine file, the video stream bitrate of the mezzanine file is retained after transcoding.   * false: Do not check the video stream bitrate of the mezzanine file.    Default value: false. |
| IsCheckVideoBitrateFail | String | No       | Specifies whether to check the video stream bitrate of the mezzanine file for a transcoding failure. Valid values: * true: Check the video stream bitrate of the mezzanine file. If ApsaraVideo VOD determines that the video stream bitrate of the output file is greater than the video stream bitrate of the mezzanine file, no transcoding is performed.   * false: Do not check the video stream bitrate of the mezzanine file.    Default value: false. This parameter has a greater priority than the IsCheckVideoBitrate parameter.                                                                                    |
| IsCheckAudioBitrate     | String | No       | Specifies whether to check the audio stream bitrate of the mezzanine file. Then, ApsaraVideo VOD determines whether to use the audio stream bitrate of the mezzanine file for transcoding based on the check result. Valid values: * true: Check the audio stream bitrate of the mezzanine file. If ApsaraVideo VOD determines that the audio stream bitrate of the output file is greater than the audio stream bitrate of the mezzanine file, the audio stream bitrate of the mezzanine file is retained after transcoding.   * false: Do not check the audio stream bitrate of the mezzanine file.    Default value: false. |
| IsCheckAudioBitrateFail | String | No       | Specifies whether to check the audio stream bitrate of the mezzanine file for a transcoding failure. Valid values: * true: Check the audio stream bitrate of the mezzanine file. If ApsaraVideo VOD determines that the audio stream bitrate of the output file is greater than the audio stream bitrate of the mezzanine file, no transcoding is performed.   * false: Do not check the audio stream bitrate of the mezzanine file.    Default value: false. This parameter has a greater priority than the IsCheckAudioBitrate parameter.                                                                                    |



**Example of the TransConfig parameter** 

    {
            "IsCheckReso":"true",
            "IsCheckResoFail":"false",
            "IsCheckVideoBitrate":"false",
            "IsCheckVideoBitrateFail":"false",
            "IsCheckAudioBitrate":"false",
            "IsCheckAudioBitrateFail":"false"
    }



Clip: video cropping configurations 
--------------------------------------------------------



| Parameter | Type                                             | Required | Description                                               |
|:----------|:-------------------------------------------------|:---------|:----------------------------------------------------------|
| TimeSpan  | [TimeSpan](#section-ci2-v8c-ehf) | Yes      | The configurations of the time span used to crop a video. |



TimeSpan: the configurations of the time span used to crop a video 
---------------------------------------------------------------------------------------



| Parameter | Type   | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|:----------|:-------|:---------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Seek      | String | Yes      | The start time of the captured part of the video.  * Format 1: sssss\[.SSS\].Valid values: \[0.000,86399.999\].  Example: 12000.55.   * Format 2: hh:mm:ss\[.SSS\].Valid values: \[00:00:00.000,23:59:59.999\]. Example: 00:00:05.003.    We recommend that you use Format 1.                                                                                                                                                                                                                                                                                                                      |
| Duration  | String | No       | The duration of the captured part of the video.  * Format 1: sssss\[.SSS\].Valid values: \[0.000,86399.999\].  Example: 12000.55.   * Format 2: hh:mm:ss\[.SSS\].Valid values: \[00:00:00.000,23:59:59.999\]. Example: 00:00:05.003.    We recommend that you use Format 1.                                                                                                                                                                                                                                                                                                                        |
| End       | String | No       | The duration of the remaining part of the video after video cropping.  * Format 1: sssss\[.SSS\].Valid values: \[0.000,86399.999\].  Example: 12000.55.   * Format 2: hh:mm:ss\[.SSS\].Valid values: \[00:00:00.000,23:59:59.999\]. Example: 00:00:05.003.    We recommend that you use Format 1.  **Note** * If you set this parameter, the Duration parameter is invalid.   * The duration between the start time and the end time cannot be greater than the total duration of the video.    |


**Note**

Note: Set only one of the Duration and End parameters.

EncryptSetting: the encryption configuration for transcoding 
---------------------------------------------------------------------------------

**Note**

You must set the EncryptType parameter to AliyunVoDEncryption and call the [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md) operation to start the HLS encryption.


| Parameter   | Type   | Required | Description                                                                                                        |
|:------------|:-------|:---------|:-------------------------------------------------------------------------------------------------------------------|
| EncryptType | String | Yes      | The encryption type. Set the value to AliyunVoDEncryption. This parameter is valid only for the M3U8 (HLS) format. |



**Example of the EncryptSetting parameter** 

    {
            "EncryptType":"AliyunVoDEncryption"
    }



PackageSetting: packaging configurations for transcoding 
-----------------------------------------------------------------------------

**Note**

* You cannot package video and audio streams after you extract them from files.

  

* Only HLS packaging is supported.

  





| Parameter                 | Type                                                              | Required | Description                                                                                                                        |
|:--------------------------|:------------------------------------------------------------------|:---------|:-----------------------------------------------------------------------------------------------------------------------------------|
| PackageType               | String                                                            | Yes      | The packaging type. Set the value to HLSPackage.                                                                                   |
| PackageConfig             | [PackageConfig](#section-t96-x4j-8jq)             | No       | The packaging configurations. You must set this parameter if a video stream packaging template is used for transcoding.            |
| SubtitleExtractConfigList | [SubtitleExtractConfig\[\]](#section-e5l-mcn-k15) | No       | The subtitle packaging configurations. You can set this parameter only when a subtitle packaging template is used for transcoding. |



PackageConfig: video packaging configurations 
------------------------------------------------------------------

**Note**

You can set this parameter only when the PackageType parameter is set to HLSPackage.


| Parameter | Type   | Required | Description                                                                                                                                                                                         |
|:----------|:-------|:---------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BandWidth | String | Yes      | The maximum bandwidth. You must set this parameter for HLS packaging. Unit: bit/s.  You can set this parameter only when a video stream packaging template is used for transcoding. |



**Example of the PackageSetting parameter** 

    Sample code for configuring a video stream packaging template:
    {
            "PackageType":"HLSPackage",
            "PackageConfig":{
                    "BandWidth":"400000"
            }
    }
                            



SubtitleExtractConfig: subtitle packaging configurations 
-----------------------------------------------------------------------------



| Parameter       | Type       | Required | Description                                                                                                                                                                                                                                                                                                                                                                         |
|:----------------|:-----------|:---------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubtitleUrlList | String\[\] | Yes      | The OSS URLs of subtitle files. The OSS URLs must be HTTP URLs. CDN URLs and HTTPS URLs are not supported. 							  **Note** * You can specify only one HTTP URL.   * You can store subtitle files only in the buckets that are allocated by ApsaraVideo VOD.    |
| Language        | String     | Yes      | The tag of the subtitle language, such as en-US. For more information, see RFC 5646.                                                                                                                                                                                                                                                                                                |
| Format          | String     | Yes      | The format of subtitle files. Only .vtt files are supported. Sample file name: subtitle.vtt.                                                                                                                                                                                                                                                                                        |
| Name            | String     | Yes      | The display name of the subtitle in the player, such as Chinese and English.                                                                                                                                                                                                                                                                                                        |



**Example of the SubtitlePackage parameter** 

    Sample code for configuring a subtitle packaging template:
     {
          "PackageType": "HLSPackage",
          "SubtitleExtractConfigList": [
            {
              "SubtitleUrlList": [
                "http://outin-4051403e7.oss-cn-shanghai.aliyuncs.com/subtitles/4bff3675-79a5-40fa-8c86-1f98169d69ca-eng.vtt"
              ],
              "Language": "en-US",
              "Format": "vtt",
              "Name": "English"
            },
            {
              "SubtitleUrlList": [
                "http://outin-4051403e7.oss-cn-shanghai.aliyuncs.com/subtitles/a3f50b08-11c3-4511-94cf-7fd4f7a5e87e-jpn.vtt"
              ],
              "Language": "ja",
              "Format": "vtt",
              "Name": "Japanese"
            },
            {
              "SubtitleUrlList": [
                "http://outin-4051403e7.oss-cn-shanghai.aliyuncs.com/subtitles/4dba87c2-a787-42cd-8328-2369aeb8bff3-cn.vtt"
              ],
              "Language": "cn",
              "Format": "vtt",
              "Name": "Chinese"
            }
          ]
        }



SubtitleConfig: subtitle configurations 
------------------------------------------------------------



| Parameter   | Type   | Required | Description                                                                                                                                                                                                                                                                                                                                       |
|:------------|:-------|:---------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubtitleUrl | String | Yes      | The OSS URL of the subtitle file. HTTPS URLs and CDN URLs are not supported. Supported subtitle formats: srt and ass.  **Note** The subtitle file and mezzanine video file must be stored in the same bucket in the same region, such as the China (Shanghai) region.                                             |
| CharEnc     | String | Yes      | The encoding format of the subtitle file. Valid values: * auto: The system automatically identifies the encoding format.   * UTF-8   * GBK   * BIG5    Default value: UTF-8. |


**Note**

For more information about how to upload a subtitle file, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md) and [Upload OSS objects](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).

Example of the SubtitleConfig parameter

    {
            "SubtitleUrl": "http://outin-40564284ef058b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/subtitles/c737f-14f1-4364-b107-d5f7f8edde0e.ass",
            "CharEncode": "UTF-8"
    }



Volume: volume configurations 
--------------------------------------------------



| Parameter                | Type   | Required | Description                                                                                                                                                   |
|:-------------------------|:-------|:---------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Method                   | String | No       | The volume adjustment method. Valid values: auto, dynamic, and linear.                                                                                        |
| IntegratedLoudnessTarget | String | No       | The new volume. Valid values: \[-70,-5\]. This parameter is valid only when the Method parameter is set to dynamic.  Default value: -6.       |
| TruePeak                 | String | No       | The peak volume. Valid values: \[-9,0\]. This parameter is valid only when the Method parameter is set to dynamic.  Default value: -1.        |
| LoudnessRangeTarget      | String | No       | The range of the volume. Valid values: \[1,20\]. This parameter is valid only when the Method parameter is set to dynamic.  Default value: 8. |



**Example of the Volume parameter** 

    {
            "Method":"dynamic",
            "IntegratedLoudnessTarget":"auto",
            "TruePeak":"-1",
            "LoudnessRangeTarget":"8"
    }



Supported combinations of container formats and audio encoding formats 
-------------------------------------------------------------------------------------------



| Container | Audio Codecs    |
|:----------|:----------------|
| mp3       | MP3             |
| mp4       | AAC             |
| ogg       | VORBIS and FLAC |
| flac      | FLAC            |



Supported combinations of container formats, audio encoding formats, and video encoding formats 
--------------------------------------------------------------------------------------------------------------------



| Container | Video Codecs    | Audio Codecs  |
|:----------|:----------------|:--------------|
| flv       | H.264           | AAC and MP3   |
| mp4       | H.264 and H.265 | AAC and MP3   |
| ts        | H.264 and H.265 | AAC and MP3   |
| m3u8      | H.264 and H.265 | AAC and MP3   |
| gif       | GIF             | Not supported |



Supported combinations of video encoding formats and video stream parameters 
-------------------------------------------------------------------------------------------------



| Video Codecs | H.264 | H.265 | GIF  |
|:-------------|:------|:------|:-----|
| Profile      | √     | ×     | ×    |
| Bitrate      | √     | √     | ×    |
| Crf          | √     | √     | ×    |
| Width        | √     | √     | √    |
| Height       | √     | √     | √    |
| Fps          | √     | √     | √    |
| Gop          | √     | √     | ×    |
| Preset       | √     | ×     | ×    |
| ScanMode     | √     | √     | √    |
| Bufsize      | √     | √     | ×    |
| Maxrate      | √     | √     | ×    |
| PixFmt       | √     | √     | bgr8 |



TranscodeSummary: transcoding summaries 
------------------------------------------------------------



| Parameter                   | Type                                                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|:----------------------------|:--------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VideoId                     | String                                                              | The ID of the video.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| TranscodeTemplateGroupId    | String                                                              | The ID of the transcoding template group.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| TranscodeStatus             | String                                                              | The transcoding status. Valid values: * Processing: Transcoding is in progress.   * Partial: The video is partially transcoded.   * CompleteAllSucc: All the transcoding jobs are complete, and the video is fully transcoded.   * CompleteAllFail: All the transcoding jobs are complete but the video fails to be transcoded. If an exception occurs in the mezzanine file, no transcoding job is initiated, and the transcoding task fails.   * CompletePartialSucc: All the transcoding jobs are complete but the video is partially transcoded.    |
| TranscodeJobInfoSummaryList | [TranscodeJobInfoSummary](#section-gi9-03s-id5)\[\] | The summaries of transcoding jobs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| CreationTime                | String                                                              | The time when the transcoding task was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| CompleteTime                | String                                                              | The time when the transcoding task was complete. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |



TranscodeJobInfoSummary: the summary of a transcoding job 
------------------------------------------------------------------------------



| Parameter           | Type       | Description                                                                                                                                                                                                                                                                                                                                    |
|:--------------------|:-----------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TranscodeTemplateId | String     | The ID of the transcoding template.                                                                                                                                                                                                                                                                                                            |
| Width               | String     | The image width of the output video. Unit: pixel.                                                                                                                                                                                                                                                                                              |
| Height              | String     | The image height of the output video. Unit: pixel.                                                                                                                                                                                                                                                                                             |
| Duration            | String     | The duration of the output video. Unit: seconds.                                                                                                                                                                                                                                                                                               |
| Filesize            | String     | The size of the output video file. Unit: byte.                                                                                                                                                                                                                                                                                                 |
| Bitrate             | String     | The average bitrate of the output video. Unit: Kbit/s.                                                                                                                                                                                                                                                                                         |
| Fps                 | String     | The frame rate of the output video. Unit: frames per second.                                                                                                                                                                                                                                                                                   |
| Format              | String     | The container format of the output video.                                                                                                                                                                                                                                                                                                      |
| WatermarkIdList     | String\[\] | The IDs of the watermarks that are applied to the output video.                                                                                                                                                                                                                                                                                |
| TranscodeProgress   | Long       | The transcoding progress. Valid values: \[0,100\].                                                                                                                                                                                                                                                                                             |
| TranscodeJobStatus  | String     | The status of the transcoding job. Valid values: * Transcoding: The transcoding job is running.   * TranscodeSuccess: The transcoding job is successful.   * TranscodeFail: The transcoding job failed.    |
| CreationTime        | String     | The time when the transcoding job was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.                                                                                                                                                                                        |
| CompleteTime        | String     | The time when the transcoding job was complete. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.                                                                                                                                                                                       |
| ErrorCode           | String     | The error code returned when the transcoding job failed.                                                                                                                                                                                                                                                                                       |
| ErrorMessage        | String     | The error message returned when the transcoding job failed.                                                                                                                                                                                                                                                                                    |



TranscodeTask: the information about a transcoding task 
----------------------------------------------------------------------------



| Parameter                | Type                                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|:-------------------------|:---------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TranscodeTaskId          | String                                                   | The ID of the transcoding task.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| TranscodeTemplateGroupId | String                                                   | The ID of the transcoding template group.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| VideoId                  | String                                                   | The ID of the video.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| TaskStatus               | String                                                   | The status of the transcoding task. Valid values: * Processing: Transcoding is in progress.   * Partial: The video is partially transcoded.   * CompleteAllSucc: All the transcoding jobs are complete, and the video is fully transcoded.   * CompleteAllFail: All the transcoding jobs are complete but the video fails to be transcoded. If an exception occurs in the mezzanine file, no transcoding job is initiated, and the transcoding task fails.   * CompletePartialSucc: All the transcoding jobs are complete but the video is partially transcoded.    |
| CreationTime             | String                                                   | The time when the transcoding task was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| CompleteTime             | String                                                   | The time when the transcoding task was complete. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Trigger                  | String                                                   | The trigger type. Valid values:						 * Auto: Transcoding is automatically triggered after a video is uploaded.   * Manual: Transcoding is triggered by calling the [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md) operation.                                                                                                                                                                                                                                                                                                                                                             |
| TranscodeJobInfoList     | [TranscodeJobInfo](#section-8o0-79k-mjw) | The information about transcoding jobs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |



TranscodeJobInfo: the information about a transcoding job 
------------------------------------------------------------------------------



| Parameter           | Type                                               | Description                                                                                                                                                                                                                                                                                                                                    |
|:--------------------|:---------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TranscodeTaskId     | String                                             | The ID of the transcoding task.                                                                                                                                                                                                                                                                                                                |
| TranscodeJobId      | String                                             | The ID of the transcoding job.                                                                                                                                                                                                                                                                                                                 |
| VideoId             | String                                             | The ID of the video.                                                                                                                                                                                                                                                                                                                           |
| TranscodeProgress   | Long                                               | The progress of the transcoding job. Valid values: \[0,100\].                                                                                                                                                                                                                                                                                  |
| TranscodeJobStatus  | String                                             | The status of the transcoding job. Valid values: * Transcoding: The transcoding job is running.   * TranscodeSuccess: The transcoding job is successful.   * TranscodeFail: The transcoding job failed.    |
| Priority            | String                                             | The priority of the transcoding task.                                                                                                                                                                                                                                                                                                          |
| Definition          | String                                             | The definition.  **Note** This parameter indicates the definition that is configured for the transcoding template and does not indicate the actual resolution range of the output video.                                                                                                                                       |
| TranscodeTemplateId | String                                             | The ID of the transcoding template.                                                                                                                                                                                                                                                                                                            |
| CreationTime        | String                                             | The time when the transcoding job was created.                                                                                                                                                                                                                                                                                                 |
| CompleteTime        | String                                             | The time when the transcoding job was complete.                                                                                                                                                                                                                                                                                                |
| InputFileUrl        | String                                             | The OSS URL of the mezzanine file.                                                                                                                                                                                                                                                                                                             |
| OutputFile          | [OutputFile](#section-mwm-rx4-iox) | The information about the output file.                                                                                                                                                                                                                                                                                                         |
| ErrorCode           | String                                             | The error code returned when the transcoding job failed.                                                                                                                                                                                                                                                                                       |
| ErrorMessage        | String                                             | The error message returned when the transcoding job failed.                                                                                                                                                                                                                                                                                    |



OutputFile: the information about an output file after transcoding 
---------------------------------------------------------------------------------------



| Parameter       | Type   | Description                                                                                                                              |
|:----------------|:-------|:-----------------------------------------------------------------------------------------------------------------------------------------|
| OutputFileUrl   | String | The OSS URL of the output file.                                                                                                          |
| Format          | String | The container format of the output file.                                                                                                 |
| Width           | String | The image width of the output file. Unit: pixel.                                                                                         |
| Height          | String | The image height of the output file. Unit: pixel.                                                                                        |
| Duration        | String | The duration of the output file. Unit: seconds.                                                                                          |
| Bitrate         | String | The average bitrate of the output file. Unit: Kbit/s.                                                                                    |
| Fps             | String | The frame rate of the output file. Unit: frames per second.                                                                              |
| Filesize        | Long   | The size of the output file. Unit: byte.                                                                                                 |
| EncryptType     | String | The encryption type that is used for the output file. The value is a JSON string.                                                        |
| WatermarkIdList | String | The IDs of the watermarks that are applied to the output file.                                                                           |
| VideoStreamList | String | The video streams. For more information, see [VideoStream: the information about a video stream](#section-7n0-err-4h8).  |
| AudioStreamList | String | The audio streams. For more information, see [AudioStream: the information about an audio stream](#section-rxt-277-pec). |



ImageInfo: the information about an image 
--------------------------------------------------------------



|                                         Parameter                                          |                       Type                        |                                                      Description                                                       |
|--------------------------------------------------------------------------------------------|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| ImageId                                                                                    | String                                            | The ID of the image.                                                                                                   |
| URL                                                                                        | String                                            | The URL of the image. If a domain name for CDN is specified, a CDN URL is returned. Otherwise, an OSS URL is returned. |
| Title                                                                                      | String                                            | The title of the image.                                                                                                |
| Tags                                                                                       | String                                            | The tags of the image.                                                                                                 |
| ImageType                                                                                  | String                                            | The type of the image.                                                                                                 |
| CateId                                                                                     | Long                                              | The ID of the category.                                                                                                |
| CateName                                                                                   | String                                            | The name of the category.                                                                                              |
| Description                                                                                | String                                            | The description of the image.                                                                                          |
| StorageLocation                                                                            | String                                            | The storage location.                                                                                                  |
| Mezzanine                                                                                  | [Mezzanine](#section-kb3-2vt-8n1) | The information about the mezzanine image file.                                                                        |
| CreationTime                                                                               | String                                            | The time when the image was created. The time is displayed in UTC.                                                     |
| [Status](#section-szr-1uj-dxw)                                             | String                                            | The status of the image.                                                                                               |
| [AppId](/intl.en-US/Developer Guide/Multi-application service/Overview.md) | String                                            | The ID of the application.                                                                                             |



Mezzanine: the information about a mezzanine image file 
----------------------------------------------------------------------------



|    Parameter     |  Type   |                     Description                      |
|------------------|---------|------------------------------------------------------|
| FileURL          | String  | The OSS URL of the mezzanine image file.             |
| OriginalFileName | String  | The name of the mezzanine image file.                |
| FileSize         | Long    | The size of the mezzanine image file. Unit: byte.    |
| Width            | Integer | The width of the mezzanine image file. Unit: pixel.  |
| Height           | Integer | The height of the mezzanine image file. Unit: pixel. |



DynamicImage: the information about an animated sticker 
----------------------------------------------------------------------------




|   Parameter    |  Type  |                           Description                           |
|----------------|--------|-----------------------------------------------------------------|
| VideoId        | String | The ID of the video.                                            |
| DynamicImageId | String | The ID of the animated sticker.                                 |
| FileURL        | String | The URL of the animated sticker file.                           |
| Width          | String | The width of the animated sticker.                              |
| Height         | String | The height of the animated sticker.                             |
| Duration       | String | The duration of the animated sticker.                           |
| Format         | String | The format of the animated sticker. Valid values: gif and webp. |
| FileSize       | String | The size of the animated sticker file.                          |
| Fps            | String | The frame rate of the animated sticker.                         |



URLUploadInfo: the information about a URL-based upload job 
--------------------------------------------------------------------------------



|                                    Parameter                                     |  Type  |                Description                 |
|----------------------------------------------------------------------------------|--------|--------------------------------------------|
| JobId                                                                            | String | The ID of the upload job.                  |
| UploadURL                                                                        | String | The URL of the video to be uploaded.       |
| MediaId                                                                          | String | The ID of the video to be uploaded.        |
| [Status](/intl.en-US/API Reference/Appendix/Basic structures.md) | String | The status of the video.                   |
| [UploadStatus](#section-ehe-tmf-118)                             | String | The status of the URL-based upload job.    |
| CreationTime                                                                     | String | The time when the upload job was created.  |
| CompleteTime                                                                     | Long   | The time when the upload job was complete. |
| UserData                                                                         | String | The custom configurations.                 |
| ErrorCode                                                                        | String | The error code.                            |
| ErrorMessage                                                                     | String | The error message.                         |



Status: the status of a URL-based upload job 
-----------------------------------------------------------------



|      Value       |                         Description                         |
|------------------|-------------------------------------------------------------|
| PENDING          | The upload job is submitted and is to be processed.         |
| PROCESSING       | The upload job is being processed.                          |
| DOWNLOADING      | The file is being downloaded.                               |
| DOWNLOAD_SUCCESS | The file is downloaded.                                     |
| DOWNLOAD_FAIL    | The file fails to be downloaded.                            |
| UPLOADING        | The file is being uploaded.                                 |
| UPLOAD_SUCCESS   | The file is uploaded.                                       |
| UPLOAD_FAIL      | The file fails to be uploaded.                              |
| SUCCESS          | The upload job is successful, and the callback is complete. |



AttachedMediaInfo: the information about an auxiliary media asset 
--------------------------------------------------------------------------------------



|                   Parameter                    |                         Type                         |                                                              Description                                                               |
|------------------------------------------------|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| MediaId                                        | String                                               | The ID of the auxiliary media asset.                                                                                                   |
| URL                                            | String                                               | The URL of the auxiliary media asset. If a domain name for CDN is specified, a CDN URL is returned. Otherwise, an OSS URL is returned. |
| Title                                          | String                                               | The title of the auxiliary media asset.                                                                                                |
| Tags                                           | String                                               | The tags of the auxiliary media asset.                                                                                                 |
| Type                                           | String                                               | The type of the auxiliary media asset.                                                                                                 |
| Categories                                     | [Category](#section-ykq-jym-ngf)\[\] | The categories.                                                                                                                        |
| Description                                    | String                                               | The description of the auxiliary media asset.                                                                                          |
| StorageLocation                                | String                                               | The storage location.                                                                                                                  |
| CreationTime                                   | String                                               | The time when the auxiliary media asset was created. The time is displayed in UTC.                                                     |
| ModificationTime                               | String                                               | The time when the auxiliary media asset was last modified. The time is displayed in UTC.                                               |
| [Status](#section-c34-tip-46h) | String                                               | The status of the auxiliary media asset.                                                                                               |
| AppId                                          | String                                               | The ID of the application.                                                                                                             |



Status: the status of an auxiliary media asset 
-------------------------------------------------------------------



|   Value    |                   Description                   |                                                        Remarks                                                         |
|------------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Uploading  | The auxiliary media asset is being uploaded.    | This is the initial status of an auxiliary media asset. It indicates that the auxiliary media asset is being uploaded. |
| Normal     | The auxiliary media asset is uploaded.          | An auxiliary media asset in this state is uploaded.                                                                    |
| UploadFail | The auxiliary media asset fails to be uploaded. | An auxiliary media asset in this state fails to be uploaded.                                                           |



MessageCallback: the configurations of an event notification 
---------------------------------------------------------------------------------



| Parameter     | Type   | Description                                                                                                                                                                                                                                                                                                           |
|:--------------|:-------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CallbackType  | String | The callback method. Valid values: HTTP and MNS.                                                                                                                                                                                                                                                                      |
| CallbackURL   | String | The callback URL. This parameter is returned only for HTTP callbacks.                                                                                                                                                                                                                                                 |
| MnsEndpoint   | String | The public endpoint of Message Service (MNS). This parameter is returned only for MNS callbacks.                                                                                                                                                                                                                      |
| MnsQueueName  | String | The name of the MNS queue. This parameter is returned only for MNS callbacks.                                                                                                                                                                                                                                         |
| EventTypeList | String | The type of the callback event.                                                                                                                                                                                                                                                                                       |
| AuthSwitch    | String | Indicates whether callback authentication is enabled. This parameter is returned only for HTTP callbacks. Valid values: * on: Callback authentication is enabled.   * off: Callback authentication is disabled.    |
| AuthKey       | String | The cryptographic key. This parameter is returned only for HTTP callbacks.                                                                                                                                                                                                                                            |



AppInfo: the information about an application 
------------------------------------------------------------------



|    Parameter     |  Type  |                                  Description                                   |
|------------------|--------|--------------------------------------------------------------------------------|
| AppId            | String | The ID of the application.                                                     |
| AppName          | String | The name of the application.                                                   |
| Description      | String | The description of the application.                                            |
| Type             | String | The type of the application. Valid values: System and Custom.                  |
| Status           | String | The status of the application. Valid values: Normal and Disable.               |
| CreationTime     | String | The time when the application was created. The time is displayed in UTC.       |
| ModificationTime | String | The time when the application was last modified. The time is displayed in UTC. |



AppPolicy: the information about an application policy 
---------------------------------------------------------------------------



|  Parameter   |  Type  |                             Description                             |
|--------------|--------|---------------------------------------------------------------------|
| AppId        | String | The ID of the application.                                          |
| PolicyType   | String | The type of the policy. Valid values: System and Custom.            |
| PolicyName   | String | The name of the policy.                                             |
| CreationTime | String | The time when the policy was created. The time is displayed in UTC. |
| Description  | String | The description of the policy.                                      |


