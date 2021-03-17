# Basic data types

## Video

Specifies the information about a video.

|Parameter|Type|Description|
|---------|----|-----------|
|VideoId|String|The ID of the video.|
|Title|String|The title of the video.|
|Description|String|The description of the video.|
|Duration|Float|The duration of the video. Unit: seconds.|
|CoverURL|String|The URL of the video thumbnail.|
|Status|String|[The status of the video](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#VideoStatus).|
|CreationTime|String|The time when the video was created. The time is displayed in UTC.|
|Size|Long|The size of the video mezzanine file. Unit: byte.|
|Snapshots|String\[\]|The URLs of video snapshots. The value is an array.|
|CateId|Long|The ID of the video category.|
|CateName|String|The name of the video category.|
|Tags|String|The tag of the video. Separate multiple tags with commas \(,\).|
|TemplateGroupId|String|The ID of the template group that was used to transcode the video.|
|StorageLocation|String|The Object Storage Service \(OSS\) bucket where the video file is stored.|
|AppId|String|[The ID of the application](https://help.aliyun.com/document_detail/113600.html#AppId).|

## VideoBase

Specifies the basic information about a video.

|Parameter|Type|Description|
|VideoId|String|The ID of the video.|
|Title|String|The title of the video.|
|Duration|String|The duration of the video. Unit: seconds.|
|CoverURL|String|The URL of the video thumbnail.|
|Status|String|[The status of the video](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#VideoStatus).|
|CreationTime|String|The time when the video was created. The time is displayed in UTC.|
|MediaType|String|The type of the media file. Valid values: -   video: video
-   audio: audio only |

**Note:** By default, the GetPlayInfo operation returns a Content Delivery Network \(CDN\) URL. If no domain name is specified, the GetPlayInfo operation returns an OSS URL. In this case, only the URL of the .mp4 video is available for playback.

## Media

Specifies the information about a media file.

|Parameter|Type|Description|
|MediaId|String|The ID of the media file.|
|CreationTime|String|The time when the media file was created. The time is displayed in UTC.|
|MediaType|String|The type of the media file. Valid values: -   video: video
-   audio: audio only
-   image: image
-   attached: auxiliary media asset |
|Video|[Video](https://help.aliyun.com/document_detail/86991.html#Video)|[The information about the video](https://help.aliyun.com/document_detail/86991.html#Video).|
|Audio|Audio|[The information about the audio](https://help.aliyun.com/document_detail/86991.html#Audio).|
|Image|Image|[The information about the image](https://help.aliyun.com/document_detail/86991.html#Image).|
|AttachedMedia|AttachedMedia|[The information about the auxiliary media asset](https://help.aliyun.com/document_detail/86991.html#AttachedMedia).|

## PlayInfo

Specifies the playback information about a video stream.

|Parameter|Type|Description|
|Bitrate|String|The bitrate of the video stream. Unit: Kbit/s.|
|Definition|String|The definition of the video stream. Valid values: -   FD: low definition
-   LD: standard definition
-   SD: high definition
-   HD: ultra high definition
-   OD: original quality
-   2K: 2K resolution
-   4K: 4K resolution |
|Specification|String|The specifications of a transcoded audio or video stream. For more information about the value range, see [Specification](https://help.aliyun.com/document_detail/124671.html#Specification).|
|Duration|String|The length of the video stream. Unit: seconds.|
|Encrypt|Long|Indicates whether the video stream is encrypted. Valid values: -   0: no
-   1: yes |
|EncryptType|String|The type of encryption that was performed on the video stream. Valid values: -   AliyunVoDEncryption: Alibaba Cloud proprietary cryptography
-   HLSEncryption: HTTP-Live-Streaming \(HLS\) encryption |
|PlayURL|String|The streaming URL of the video stream.|
|Format|String|The format of the video stream. If the media file is a video file, the following valid values are included: -   mp4
-   m3u8

 If the media file is an audio-only file, the value is -   mp3 |
|Fps|String|The frame rate of the video stream. Unit: frames per second|
|Size|Long|The size of the video stream. Unit: byte.|
|Width|Long|The width of the video stream. Unit: pixel.|
|Height|Long|The height of the video stream. Unit: pixel.|
|StreamType|String|The type of the media stream. If the media stream is a video stream, the value is -   video

 If the media stream is an audio-only stream, the value is -   audio |
|JobId|String|The ID of the job that was used to transcode the media stream. This ID uniquely identifies a media stream.|
|WatermarkId|String|The ID of the watermark that is associated with the media stream.|
|Status|String|The status of the video stream. Valid values: -   Normal: The video stream can be played
-   Invisible: The video stream is blocked. |
|NarrowBandType|String|The type of Narrowband HD™. Valid values: -   0: normal transcoding
-   1.0: Narrowband HD™ 1.0
-   2.0: Narrowband HD™ 2.0

 This parameter takes effect only when the definition of the built-in Narrowband HD™ 1.0 transcoding template is specified. For more information, see the Definition parameter in the [TranscodeTemplate](https://help.aliyun.com/document_detail/52839.html#h2--transcodetemplate-div-id-transcodetemplate-div-37) table.|
|CreationTime|String|The time when the media stream was created. The time is displayed in UTC.|
|ModificationTime|String|The time when the media stream was last updated. The time is displayed in UTC.|

## VideoMeta

Specifies the metadata of a video.

|Parameter|Type|Description|
|---------|----|-----------|
|VideoId|String|The ID of the video.|
|Title|String|The title of the video.|
|Duration|Float|The duration of the video. Unit: seconds.|
|CoverURL|String|The URL of the video thumbnail.|
|Status|String|[The status of the video](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#VideoStatus).|

## Status

The following table describes the valid values of the Status parameter for a video.

|Value|Description|Remarks|
|-----|-----------|-------|
|Uploading|Indicates that the video is being uploaded.|The initial status, which indicates that the video is being uploaded.|
|UploadFail|Indicates that the video fails to be uploaded.|This value is temporarily not used because the video is uploaded in resumable mode and ApsaraVideo VOD cannot determine whether the resumable upload fails.|
|UploadSucc|Indicates that the video is uploaded.|-|
|Transcoding|Indicates that the video is being transcoded.|-|
|TranscodeFail|Indicates that the video fails to be transcoded.|A transcoding failure is usually caused by an error in the video mezzanine file. To troubleshoot a transcoding failure, you can obtain the error message from the [TranscodeComplete](https://help.aliyun.com/document_detail/55638.html) event notification or submit a ticket.|
|Checking|Indicates that the video is being reviewed.|Log on to the [ApsaraVideo VOD console](https://www.aliyun.com/product/vod?spm=5176.8142029.388261.421.78de76f4IhQkZa). In the left-side navigation pane, choose **Review** \> **Settings**. If the Process parameter is set to **Review Before Publish**, the video status changes to **Under Review** after the video is transcoded. In this case, the video can be played only in the console.|
|Blocked|Indicates that the video is blocked.|The video is blocked when it is being reviewed.|
|Normal|Indicates that the video can be played.|The video can be played.|
|ProduceFail|Indicates that the video fails to be produced.|-|

## Status

The following table describes valid values of the Status parameter for an image.

|Value|Description|Remarks|
|-----|-----------|-------|
|Uploading|Indicates that the image is being uploaded.|The initial status, which indicates that the image is being uploaded.|
|Normal|Indicates that the image is uploaded.|The image is uploaded.|
|UploadFail|Indicates that the image fails to be uploaded.|The image fails to be uploaded.|

## Category

|Parameter|Type|Description|
|---------|----|-----------|
|CateId|Long|The ID of the video category.|
|CateName|String|The name of the category. The value can be up to 64 bytes in length. The string must be encoded in the UTF-8 format.|
|ParentId|Long|The ID of the parent category. The parent category ID of a level 1 category is -1.|
|Level|Long|The level of the category. A value of 0 indicates a level 1 category.|

## Mezzanine

|Parameter|Type|Description|
|---------|----|-----------|
|VideoId|String|The ID of the video.|
|FileName|String|The name of the mezzanine file.|
|Duration|String|The duration of the mezzanine file. Unit: seconds.|
|Status|String|The status of the mezzanine file.|
|CreationTime|String|The time when the mezzanine file was created. The time is displayed in UTC.|
|Height|Long|The height of the mezzanine file. Unit: pixel.|
|Width|Long|The width of the mezzanine file. Unit: pixel.|
|Fps|String|The frame rate of the mezzanine file. Unit: frames per second.|
|FileURL|String|The URL of the mezzanine file.|
|Bitrate|String|The bitrate of the mezzanine file. Unit: Kbit/s.|
|Size|Long|The size of the mezzanine file. Unit: byte.|
|OutputType|String|The type of the playback URL for the output file. Valid values: oss and cdn. A value of oss indicates an OSS URL and a value of cdn indicates an Alibaba Cloud CDN URL.|
|VideoStreamList|[VideoStreamList](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#VideoStream)\[\]|The information about video streams.|
|AudioStreamList|[AudioStreamList](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#AudioStream)\[\]|The information about audio streams.|

## VideoStream

Specifies the information about a video stream.

|Parameter|Type|Description|
|---------|----|-----------|
|Index|String|The sequence number of the video stream. The value identifies the position of the video stream in all video streams.|
|CodecName|String|The short name of the codec format.|
|CodecLongName|String|The full name of the codec format.|
|Profile|String|The codec profile.|
|CodecTimeBase|String|The codec time base.|
|CodecTagString|String|The tag string of the codec format.|
|CodecTag|String|The tag of the codec format.|
|Width|Long|The width of the video resolution.|
|Height|Long|The height of the video resolution.|
|HasBFrames|String|Indicates whether the video stream contains bidirectional frames \(B-frames\).|
|Sar|String|The sample aspect ratio \(SAR\).|
|Dar|String|The display aspect ratio \(DAR\).|
|PixFmt|String|The pixel format.|
|Level|String|The codec level.|
|Fps|String|The frame rate of the output file.|
|AvgFPS|String|The average frame rate.|
|Timebase|String|The time base.|
|StartTime|String|The start time of the video playback.|
|Duration|String|The duration of the video playback.|
|NumFrames|String|The total number of frames.|
|Lang|String|The language.|
|Rotate|String|The rotation angle of the video. Valid values: \[0, 360\).|

## AudioStream

Specifies the information about an audio stream.

|Parameter|Type|Description|
|---------|----|-----------|
|Index|String|The sequence number of the audio stream. The value identifies the position of the audio stream in all audio streams.|
|CodecName|String|The short name of the codec format.|
|CodecLongName|String|The full name of the codec format.|
|CodecTimeBase|String|The codec time base.|
|CodecTagString|String|The tag string of the codec format.|
|CodecTag|String|The tag of the codec format.|
|SampleFmt|String|The sampling format.|
|SampleRate|String|The sample rate.|
|Channels|String|The number of sound channels.|
|ChannelLayout|String|The output layout of sound channels.|
|Timebase|String|The time base.|
|StartTime|String|The start time of the audio playback.|
|Duration|String|The duration of the audio playback.|
|Bitrate|String|The bitrate.|
|NumFrames|String|The total number of frames.|
|Lang|String|The language.|

## Status

The following table describes the valid values of the Status parameter for a mezzanine file.

|Value|Description|Remarks|
|-----|-----------|-------|
|Uploading|Indicates that the file is being uploaded.|The initial status, which indicates that the file is being uploaded.|
|Normal|Indicates that the file is uploaded.|The file is uploaded.|
|UploadFail|Indicates that the file fails to be uploaded.|The file fails to be uploaded.|
|Deleted|Indicates that the file is deleted.|The file is deleted.|

## LiveRecordVideo

Specifies the information about video-on-demand \(VOD\) files that are created from a live stream.

|Parameter|Type|Description|
|---------|----|-----------|
|StreamName|String|The name of the live stream.|
|DomainName|String|The domain name of the live stream.|
|AppName|String|The name of the application.|
|PlaylistId|String|The ID of the playlist.|
|RecordStartTime|String|The start time of recording.|
|RecordEndTime|String|The end time of recording.|
|Video|Video|The information about the video.|

## TopPlayVideoStatis

Specifies the daily playback statistics on top videos.

|Parameter|Type|Description|
|---------|----|-----------|
|VideoId|String|The ID of the video.|
|PlayDuration|String|The playback duration of the video. Unit: milliseconds.|
|Title|String|The name of the video.|
|VV|String|The number of video views.|
|UV|String|The number of unique visitors.|

## VideoPlayStatisDetail

Specifies the daily playback statistics on a specific video.

|Parameter|Type|Description|
|---------|----|-----------|
|Date|String|The date in the yyyyMMdd format. Example: 20170120.|
|PlayDuration|String|The playback duration of the video. Unit: milliseconds.|
|Title|String|The name of the video.|
|VV|String|The number of video views.|
|UV|String|The number of unique visitors.|
|PlayRange|String|The distribution of the playback duration.|

## UserPlayStatisTotals

Specifies the statistics on total playback each day.

|Parameter|Type|Description|
|---------|----|-----------|
|Date|String|The date in the yyyyMMdd format. Example: 20170120.|
|PlayDuration|String|The playback duration of the video. Unit: milliseconds.|
|PlayRange|String|The distribution of the playback duration.|
|VV|VV|The total number of video views.|
|UV|UV|The total number of unique visitors.|

## UserPlayStatisAvgs

The statistics on average playback each day.

|Parameter|Type|Description|
|---------|----|-----------|
|Date|String|The date in the yyyyMMdd format. Example: 20170120.|
|AvgPlayDuration|String|The average playback duration of the video. Unit: milliseconds.|
|AvgPlayCount|String|The average number of video views.|

## VV

Specifies the video view statistics on playbacks that use ApsaraVideo Player SDKs.

|Parameter|Type|Description|
|---------|----|-----------|
|Android|String|The total number of video views that is collected by using ApsaraVideo Player SDK for Android.|
|iOS|String|The total number of video views that is collected by using ApsaraVideo Player SDK for iOS.|
|Flash|String|The total number of video views that is collected by using ApsaraVideo Player SDK for Flash.|
|HTML5|String|The total number of video views that is collected by using ApsaraVideo Player SDK for HTML5.|

## UV

Specifies the unique visitor statistics on playbacks that use ApsaraVideo Player SDKs.

|Parameter|Type|Description|
|---------|----|-----------|
|Android|String|The total number of unique visitors who use ApsaraVideo Player SDK for Android.|
|iOS|String|The total number of unique visitors who use ApsaraVideo Player SDK for iOS.|
|Flash|String|The total number of unique visitors who use ApsaraVideo Player SDK for Flash.|
|HTML5|String|The total number of unique visitors who use ApsaraVideo Player SDK for HTML5.|

## EditingProject

|Parameter|Type|Description|
|---------|----|-----------|
|ProjectId|String|The ID of the online editing project.|
|Title|String|The title of the online editing project.|
|CreationTime|String|The time when the online editing project was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. For example, a value of 2017-01-11T12:00:00Z indicates 20:00:00 \(UTC+8\) on January 11, 2017.|
|ModifiedTime|String|The time when the online editing project was last modified. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. For example, a value of 2017-01-11T12:00:00Z indicates 20:00:00 \(UTC+8\) on January 11, 2017.|
|Status|String|The status of the online editing project.|
|Description|String|The description of the online editing project.|
|Timeline|String|The timeline of the online editing project, in the JSON format.|
|Duration|String|The duration of the online editing project. The duration must be the same as that of the timeline.|
|CoverURL|String|The thumbnail URL of the online editing project.|

## Timeline

|Parameter|Type|Description|
|---------|----|-----------|
|Id|String|The ID of the online editing project.|
|Title|String|The title of the online editing project.|
|CreationTime|String|The time when the timeline was created.|
|ModifiedTime|String|The time when the timeline was last modified.|
|Duration|Float|The total duration of the timeline. Unit: seconds. The value is rounded to four decimal places.|
|CurrentRuler|Float|The current ruler of the timeline. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|CurrentPosition|Float|The current position of the playhead for the online editing project. Unit: seconds. The value is rounded to four decimal places. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|VideoTracks|VideoTrack\[\]|The list of video tracks.|

## VideoTrack

|Parameter|Type|Description|
|---------|----|-----------|
|Count|Int|The total number of video track clips.|
|Duration|String|The duration of the video track.|
|VideoTrackClips|VideoTrackClip\[\]|The list of video track clips.|

## VideoTrackClip

|Parameter|Type|Description|
|---------|----|-----------|
|Id|String|The ID of the video track clip. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing. If the timeline is used to edit data, you must set this parameter to a unique value within the timeline.|
|VideoId|String|The video ID of the video track clip.|
|Type|String|The type of the video track clip. Valid values: Video and Image. Default value: Video.|
|Title|String|The title of the video track clip. The title must be the same as that of the video.|
|Index|Int|The sequence number of the video track clip in the timeline, which starts from zero.|
|CutFlag|Boolean|Indicates whether the video track clip is cropped. Valid values: true and false. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|TextFlag|Boolean|Indicates whether banner text is added to the video track clip. Valid values: true and false. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|DeWatermarkFlag|Boolean|Indicates whether a part of the video track clip has been masked. Valid values: true and false. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|URL|String|The streaming URL of the stream that is used to edit the video track clip. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|CoverURL|String|The thumbnail URL of the video track clip. By default, this thumbnail URL is the same as that of the video. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|SpriteURLs|String|The sprite snapshot URL of the video track clip. Separate multiple URLs with commas \(,\). You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|Width|Int|The width of the stream that is used to edit the video track clip. Unit: pixel. You do not need to set this parameter if the timeline is used only for video production instead of data storage and no effect, such as banner text or masking, is added.|
|Height|Int|The height of the stream that is used to edit the video track clip. Unit: pixel. You do not need to set this parameter if the timeline is used only for video production instead of data storage and no effect, such as banner text or masking, is added.|
|Fps|Float|The frame rate of the video track clip. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|Bitrate|Float|The bitrate of the stream that is used to edit the video track clip. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|In|Float|The start time of the video track clip in the video. Unit: seconds. The value is rounded to four decimal places.|
|Out|Float|The end time of the video track clip in the video. Unit: seconds. The value is rounded to four decimal places.|
|Duration|Float|The duration of the video track clip. Unit: seconds. The value is rounded to four decimal places.|
|VirginDuration|Float|The total duration of the video to which the video track clip belongs. Unit: seconds. The value is rounded to four decimal places. You do not need to set this parameter if the timeline is used only for video production, but not for data storage during editing.|
|TimelineIn|Float|The start time of the video track clip in the timeline. Unit: seconds. The value is rounded to four decimal places.|
|TimelineOut|Float|The end time of the video track clip in the timeline. Unit: seconds. The value is rounded to four decimal places.|
|Effects|Effect\[\]|The effects that are added to the video track clip.|

## Effect

|Parameter|Type|Description|
|---------|----|-----------|
|Type|String|The type of the effect. Valid values: Text and DeWatermark. A value of Text indicates that banner text is added to the video track clip. A value of DeWatermark indicates that a part of the video track clip is masked.|
|Name|String|The name of the effect.|
|SubType|String|The subtype of the effect. If the Type parameter is set to DeWatermark, set this parameter to Delogo\_Blur.|
|In|Float|The start time of the effect that is added to the video track clip. Unit: seconds. The value is rounded to four decimal places.|
|Out|Float|The end time of the effect that is added to the video track clip. Unit: seconds. The value is rounded to four decimal places.|
|TimelineIn|Float|The start time of the effect in the timeline. Unit: seconds. The value is rounded to four decimal places.|
|TimelineOut|Float|The end time of the effect in the timeline. Unit: seconds. The value is rounded to four decimal places.|
|X|String|The X coordinate of the effect. The coordinate origin is the upper-left corner of the video image. The value is an integer from 8 to 4096 or a decimal number between 0 and 1. If the value is an integer, the value indicates a pixel value and the unit is pixel. If the value is a decimal number, the value indicates the ratio of the pixel value to the width in pixels of the resolution of the output video image. The decimal number has four decimal places, for example, 0.9999. Excessive digits are automatically deleted.|
|Y|String|The Y coordinate of the effect. The coordinate origin is the upper-left corner of the video image. The value is an integer from 8 to 4096 or a decimal number between 0 and 1. If the value is an integer, the value indicates a pixel value and the unit is pixel. If the value is a decimal number, the value indicates the ratio of the pixel value to the height in pixels of the resolution of the output video image. The decimal number has four decimal places, for example, 0.9999. Excessive digits are automatically deleted.|
|Width|Int|The width of the area where the effect is added. The value is an integer from 8 to 4096 or a decimal number between 0 and 1. If the value is an integer, the value indicates a pixel value and the unit is pixel. If the value is a decimal number, the value indicates the ratio of the pixel value to the width in pixels of the resolution of the output video image. The decimal number has four decimal places, for example, 0.9999. Excessive digits are automatically deleted.|
|Height|Int|The height of the area where the effect is added. The value is an integer from 8 to 4096 or a decimal number between 0 and 1. If the value is an integer, the value indicates a pixel value and the unit is pixel. If the value is a decimal number, the value indicates the ratio of the pixel value to the height in pixels of the resolution of the output video image. The decimal number has four decimal places, for example, 0.9999. Excessive digits are automatically deleted.|
|FEWidth|Float|The actually displayed width of the video image during editing. Unit: pixel.|
|FEHeight|Float|The actually displayed height of the video image during editing. Unit: pixel.|
|Font|String|The font. Set the value to SimSun.|
|FontFace|FontFace|The appearance of the font. For more information, see \[FontFace\]\(\#FontFace\).|
|FontColor|String|The color of the font, in hexadecimal format. The value starts with a number sign \(\#\). Example: \#ffffff.|
|FontSize|Int|The size of the font.|
|FontColorOpacity|Float|The transparency of the font. Valid values: \[0, 1\]. A value of 1 indicates that the font is not transparent. A value of 0 indicates that the font is completely transparent.|
|Content|String|The content of banner text.|

## FontFace

|Parameter|Type|Description|
|---------|----|-----------|
|Bold|Boolean|Indicates whether the font is bold.|
|Italic|Boolean|Indicates whether the font is italic.|
|Underline|Boolean|Indicates whether the font is underlined.|

## MediaMetadata

|Parameter|Type|Description|
|---------|----|-----------|
|Title|String|The title of the produced video. The value can be up to 128 bytes in length. The string must be encoded in the UTF-8 format.|
|Description|String|The description of the produced video. The value can be up to 1,024 bytes in length. The string must be encoded in the UTF-8 format.|
|CoverURL|String|The URL of the custom thumbnail for the produced video.|
|CateId|String|The category ID of the produced video. To view the category ID, log on to the ApsaraVideo VOD console. In the left-side navigation pane, choose Configuration Management \> Media Management \> Categories.|
|Tags|String|The tags of the produced video. Each tag name can be up to 32 bytes in length. You can specify a maximum of 16 tags. Separate multiple tags with commas \(,\). The string must be encoded in the UTF-8 format.|

## ProduceConfig

|Parameter|Type|Description|
|---------|----|-----------|
|TemplateGroupId|String|The ID of the transcoding template group that is used to transcode produced videos. The produced video files are used as the mezzanine files for transcoding. This transcoding process is similar to that is performed after a file is uploaded. This parameter is optional. If you do not set this parameter, ApsaraVideo VOD uses the default template group for transcoding. If you set this parameter, ApsaraVideo VOD uses the specified template group for transcoding. To view the template group ID, go to the Transcode page in the ApsaraVideo VOD console.|
|TemplateId|String|The ID of the template that is used for video production. The produced media file is used as the mezzanine file of the media resources. This parameter is optional. -   If you do not set this parameter, ApsaraVideo VOD uses the built-in template of the online editing service for video production.
    -   If a video file is produced, the codec format is H.264 and the container format is MP4.
    -   If an audio-only file is produced, the container format is MP3.
-   Assume that you set this parameter to meet your business requirements. For example, you want to produce animated stickers, intelligently produce subtitles, edit videos based on the M3U8 playlists, or use custom production parameters. In such cases, submit a ticket to apply for the specified template. |
|Width|Integer|The width of the output resolution of the produced video. Unit: pixel. This parameter is optional. The default value equals to the maximum resolution width of the mezzanine files of the video track clips that are used in the timeline. Assume that three video track clips are used in the timeline. The resolutions of their mezzanine files are 1280 × 720 pixels, 1920 × 1080 pixels, and 720 × 1280 pixels. In this case, the output resolution of the produced video is 1920 × 1280 pixels.|
|Height|Integer|The height of the output resolution of the produced video. Unit: pixel. This parameter is optional. The default value equals to the maximum resolution height of the mezzanine files of the video track clips that are used in the timeline. Assume that three video track clips are used in the timeline. The resolutions of their mezzanine files are 1280 × 720 pixels, 1920 × 1080 pixels, and 720 × 1280 pixels. In this case, the output resolution of the produced video is 1920 × 1280 pixels.|
|StorageLocation|String|The storage location of the produced file. This parameter is required if the produced file is stored in a region outside China.|

## Material

Note: Materials for an online editing project can be materials from media assets or videos in the media library.

|Parameter|Type|Description|
|---------|----|-----------|
|MaterialId|String|The ID of the material.|
|Title|String|The title of the material.|
|Description|String|The description of the material.|
|Duration|Float|The duration of the material. Unit: seconds. The value is rounded to four decimal places.|
|CoverURL|String|The thumbnail URL of the material.|
|Status|String|The status of the material.|
|CreationTime|String|The time when the material was created. The time is displayed in UTC.|
|Size|Long|The size of the material mezzanine file. Unit: byte.|
|CateId|Long|The category ID of the material.|
|CateName|String|The category name of the material.|
|Tags|String|The tag of the material. Separate multiple tags with commas \(,\).|
|Snapshots|String\[\]|The URLs of material snapshots. The value is an array.|
|Sprites|String\[\]|The URLs of material sprite snapshots. The value is an array.|

## ProjectStatus

|Value|Description|Remarks|
|-----|-----------|-------|
|Normal|Indicates that the online editing project is being edited.|The initial status.|
|Producing|Indicates that video production is being performed.|-|
|Produced|Indicates that video production is successful.|-|
|ProduceFailed|Indicates that video production fails.|-|

## TranscodeJob

The information about the transcoding job.

|Parameter|Type|Description|
|---------|----|-----------|
|JobId|String|The ID of the job.|

## SnapshotJob

Specifies the information about a snapshot job.

|Parameter|Type|Description|
|---------|----|-----------|
|JobId|String|The ID of the job.|

## MediaSnapshot

Specifies the media snapshot data.

|Parameter|Type|Description|
|---------|----|-----------|
|JobId|String|The ID of the snapshot job.|
|CreationTime|String|The time when the snapshot job was created. The time is displayed in UTC.|
|Total|Long|The total number of snapshots.|
|Regular|String|The rule used to generate snapshot URLs.|
|Snapshots|Snapshot\[\]|The snapshot data.|

## Snapshot

Specifies the information about a snapshot.

|Parameter|Type|Description|
|---------|----|-----------|
|Index|String|The index of the snapshot.|
|Url|String|The URL of the snapshot.|

## WatermarkInfo

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|CreationTime|String|Yes|The time when the watermark was created.|
|Name|String|Yes|The name of the watermark.|
|IsDefault|String|Yes|Indicates whether the default watermark is used. A value of Default indicates the default watermark. A value of NotDefault indicates a non-default watermark.|
|Type|String|Yes|The type of the watermark. Valid values: Image and Text.|
|WatermarkId|String|Yes|The ID of the watermark.|
|FileUrl|String|No|The OSS URL or CDN URL of the watermark file. A text watermark has no file URL.|
|WatermarkConfig|[WatermarkConfig](https://help.aliyun.com/document_detail/98618.html?spm=a2c4g.11186623.6.748.10314a0987DLZ6#h2--watermarkconfig4)|Yes|The configuration information of the watermark, such as the position and effects. The value is a JSON string. For more information, see [Text watermark](https://help.aliyun.com/document_detail/98618.html?spm=a2c4g.11186623.6.748.10314a0987DLZ6#h2--watermarkconfig4) and [Image watermark](https://help.aliyun.com/document_detail/98618.html?spm=a2c4g.11186623.6.748.10314a0987DLZ6#h2--watermarkconfig4).|

## VodTemplateInfo

|Parameter|Type|Description|
|---------|----|-----------|
|Name|String|The name of the template.|
|VodTemplateId|String|The ID of the template.|
|TemplateType|String|The type of the template. -   Snapshot
-   DynamicImage |
|IsDefault|String|Indicates whether the default template is used. Valid values: Default and NotDefault.|
|TemplateConfig|JSON|The detailed configurations of the template. The value is a JSON string. -   For more information about snapshot configurations, see [SnapshotTemplateConfig](https://help.aliyun.com/document_detail/98618.html?spm=a2c4g.11186623.2.103.141f2b8b0lUOvv#h2--snapshottemplateconfig-span-id-snapshottemplateconfig-span-6).
-   For more information about the configurations of animated stickers, see [DynamicImageTemplateConfig](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.2090789fNGUu9B#DynamicImageTemplateConfig). |
|CreationTime|String|The time when the template was created. The time is displayed in UTC.|
|ModifyTime|String|The time when the template was last modified. The time is displayed in UTC.|

## DynamicImageTemplateConfig

|Parameter|Type|Description|
|---------|----|-----------|
|Name|String|The name of the template.|
|Video|[Video](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#DynamicImageVideo)|The image configurations of the animated sticker.|
|Container|[Container](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#DynamicImageContainer)|The format of the animated sticker.|
|Clip|[TimeSpan](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#DynamicImageTimeSpan)|The configurations used to crop the animated sticker.|
|SetDefaultCover|String|Indicates whether the animated sticker is used as the thumbnail. -   A value of true indicates that the animated sticker is used as the thumbnail.
-   A value of false indicates that the animated sticker is not used as the thumbnail. |

## Video

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Width|String|Yes|The width of the animated sticker. Valid values: \[128, 4096\].|
|Height|String|Yes|The height of the animated sticker. Valid values: \[128, 4096\].|
|Fps|String|Yes|The frame rate of the animated sticker. Valid values: \(0,60\]|

## Container

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Format|String|Yes|The format of the animated sticker. Valid values: webp and gif.|

## Clip

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|TimeSpan|[TimeSpan](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#DynamicImageTimeSpan)|Yes|The configurations related to the time span used to generate an animated sticker by cropping a video.|

## TimeSpan

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Seek|String|Yes|The start time of the captured part of the video. Format 1:

-   sssss\[.SSS\]
-   Valid values: \[0.000, 86399.999\].
-   Example: 12000.556.

 Format 2:

-   hh:mm:ss\[.SSS\]
-   Valid values: \[00:00:00.000, 23:59:59.999\].
-   Example: 00:00:05.003. |
|Duration|String|Yes|The duration of the captured part of the video. Format 1:

-   sssss\[.SSS\]
-   Valid values: \[0.000, 86399.999\].
-   Example: 12000.556.

 Format 2:

-   hh:mm:ss\[.SSS\]
-   Valid values: \[00:00:00.000, 23:59:59.999\].
-   Example: 00:00:05.003. |
|End|String|Yes|The duration of the remaining part of the video after animation capture. Format 1:

-   sssss\[.SSS\]
-   Valid values: \[0.000, 86399.999\].
-   Example: 12000.556.

 Format 2:

-   hh:mm:ss\[.SSS\]
-   Valid values: \[00:00:00.000, 23:59:59.999\].
-   Example: 00:00:05.003. |

## TranscodeTemplateGroup

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Name|String|Yes|The name of the transcoding template group.|
|TranscodeTemplateGroupId|String|Yes|The ID of the transcoding template group.|
|IsDefault|String|Yes|Indicates whether the transcoding template group is the default one. -   Default: The transcoding template group is the default one.
-   NotDefault: The transcoding template group is not the default one. |
|CreationTime|String|Yes|The time when the transcoding template group was created.|
|ModifyTime|String|Yes|The time when the transcoding template group was last modified.|
|TranscodeTemplateList|[TranscodeTemplate](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#TranscodeTemplate)\[\]|Yes|The information about the transcoding templates.|

## TranscodeTemplate

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Type|String|No|The type of the transcoding template. Valid values: -   **Normal**: This template is a common transcoding template. This value is the default value. If this type of template is used, you cannot set the [PackageSetting](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#PackageSetting) parameter.
-   VideoPackage: This template is a video stream package template. If this type of template is used, ApsaraVideo VOD transcodes a video into video streams in different bitrates and packages these video streams with a file. The [PackageSetting](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#PackageSetting) parameter must be set for this type of template.
-   **SubtitlePackage**: This template is a subtitle package template. If this type of template is used, ApsaraVideo VOD adds the subtitle information to the output file that is generated by packaging the multi-bitrate video streams of the specific video. You must set the [PackageSetting](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#PackageSetting) parameter for a subtitle package template and associate the subtitle package template with a video stream package template. You can configure only one subtitle package template in a template group.******** |
|Video|[Video](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#VideoTranscode)|Yes|The transcoding configurations of the video stream. The value is a JSON string.|
|Audio|[Audio](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#Audio)|Yes|The transcoding configurations of the audio stream. The value is a JSON string.|
|Definition|String|Yes|The definition of the transcoding template.

 -   This parameter specifies the definition that is configured for the transcoding template and does not specify the actual resolution range of a transcoded video. For more information about the mappings between template definitions and output video resolutions, see [Specification](https://help.aliyun.com/document_detail/124671.html).
-   The template definition does not affect transcoding fees. For more information about transcoding fees, see the "Transcoding service" section of the [Billing method](https://www.aliyun.com/price/product?spm=a2c4g.11186623.2.12.3274600bq3oF00#/vod/detail) topic.

 Valid values for the definition of a common transcoding template:

 -   LD: low definition.
-   SD: standard definition.
-   HD: high definition.
-   FHD: ultra high definition.
-   OD: original quality. This value is used for [container format conversion](https://help.aliyun.com/document_detail/99380.html).
-   2K
-   4K
-   SQ: standard sound quality.
-   HQ: high sound quality.

 Valid values for the definition of a Narrowband HD™ 1.0 transcoding template:

 -   LD-NBV1: low definition
-   SD-NBV1: standard definition
-   HD-NBV1: high definition
-   FHD-NBV1: ultra high definition
-   2K-NBV1
-   4K-NBV1

 Note:

 -   1. You are not allowed to change the definition of a transcoding template.
-   2. You are not allowed to modify the system parameters of Narrowband HD™ 1.0 transcoding templates, such as the video resolution, audio resolution, and bitrate. For more information about the parameters, see [Narrowband HD™](https://help.aliyun.com/document_detail/99719.html#narrowband).
-   3. You can create only Narrowband HD™ 1.0 transcoding templates that support the FLV, M3U8 \(HLS\), and MP4 output formats. |
|Container|[Container](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#Container)|Yes|The format of the container that is used to encapsulate audio and video streams. The value is a JSON string.|
|MuxConfig|[MuxConfig](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#MuxConfig)|No|The transcoding segment configuration. You must set this parameter if the Format parameter in the Container table is set to HLS. The value is a JSON string.|
|TransConfig|[TransConfig](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#TransConfig)|No|The conditional transcoding configuration. You can set this parameter if you need to determine the basic logic based on the bitrate and resolution of the mezzanine file before the transcoded video is generated. The value is a JSON string.|
|TranscodeFileRegular|String|No|The custom path used to store the output files. Note:

 -   The following wildcards are supported: \{MediaId\}, \{JobId\}, and \{PlayDefinition\}. The MediaId parameter indicates the video ID. The JobId parameter indicates the transcoding job ID. The PlayDefinition parameter indicates the definition that is returned after the [GetPlayInfo](https://help.aliyun.com/document_detail/56124.html) operation is called.
-   The value can contain only digits, characters, braces \{\}, slashes \(/\), hyphens \(-\), and underscores \(\_\). The value can be up to 128 characters in length.
-   The value must start with \{MediaId\}.

 -   Configuration example: **\{MediaId\}/watermark-\{PlayDefinition\}**. During transcoding, ApsaraVideo VOD replaces \{MediaId\} with the video ID and \{PlayDefinition\} with the definition. For example, the video ID can be **8ff5cc93f6da4079a47a77bf71d** and the definition can be **fd**.

 -   Output path example: **8ff5cc93f6da4079a47a77bf71d/watermark-fd.mp4**. ApsaraVideo VOD automatically adds the file name extension, such as .mp4, .m3u8, or .flv. |
|Clip|[Clip](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#Clip)|No|The video cropping configuration. The value is a JSON string. For example, you can set this parameter to extract 5 seconds from a video to generate a new video.|
|Rotate|String|No|The rotation angle of the video. For example, if you set this parameter to 180, the video image is turned upside down. -   Valid values: \[0, 360\]. |
|EncryptSetting|[EncryptSetting](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#EncryptSetting)|No|The encryption configuration for transcoding.|
|PackageSetting|[PackageSetting](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#PackageSetting)|No|The packaging configurations. Only HLS packaging and Dynamic Adaptive Streaming over HTTP \(DASH\) packaging are supported. The value is a JSON string.|
|SubtitleList|[SubtitleConfig](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#SubtitleConfig)|No|The subtitle configuration. The value is a JSON string.|
|WatermarkIds|String\[\]|No|The ID of the associated watermark. -   A maximum of four watermark IDs are supported.
-   **USER\_DEFAULT\_WATERMARK** indicates the ID of the default watermark. |
|TranscodeTemplateId|String|No|The ID of the transcoding template. You must set this parameter when you modify a transcoding template.|
|TemplateName|String|No|The name of the transcoding template. You must set this parameter when you create a transcoding template.|

## Examples of the TranscodeTemplate parameter

```
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
	"WatermarkIds":["USER_DEFAULT_WATERMARK","ddddddddd"],
	"Definition":"SD",
	"TemplateName":"test"
}
			
```

## Video

**Note:**

-   Unless otherwise required, you need only to set the Codec, Bitrate, Height, and Width parameters and set the Remove parameter to false.
-   We recommend that you set only one of the Width and Height parameters for the output video file. This ensures that the aspect ratio of the output video file is the same as that of the mezzanine file.

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Codec|String|Yes|The codec format of the video. Valid values: H.264 and H.265.|
|Remove|String|Yes|Indicates whether the video stream is deleted. Valid values: true and false. -   A value of true indicates that the video stream is deleted from the transcoded video file.
-   A value of false indicates that the video stream is retained for the transcoded video file.
-   Default value: false. |
|Bitrate|String|No|The bitrate of the output video file. If you do not set this parameter, the bitrate is generated based on the value of the Crf parameter. -   Valid values: \[10, 50000\].
-   Unit: Kbit/s. |
|Height|String|No|The image height of the output video file. The value must be a multiple of 2. If you do not set this parameter, the image height of the mezzanine file is used. -   Valid values: \[128, 4096\].
-   Unit: pixel. |
|Width|String|No|The image width of the output video file. The value must be a multiple of 2. If you do not set this parameter, the image width of the mezzanine file is used. -   Valid values: \[128, 4096\].
-   Unit: pixel. |
|Fps|String|No|The frame rate of the output video file. If you do not set this parameter, the frame rate of the mezzanine file is used. -   Valid values: \(0, 60\].
-   Unit: frames per second. |
|Gop|String|No|The size of a group of pictures \(GOP\). -   Valid values: \[1, 100000\].
-   Unit: frame. |
|LongShortMode|String|No|Indicates whether to enable auto-rotate screen, that is, the long-short side mode. The image width of the output video file corresponds to the long side of the mezzanine file or the image height of the mezzanine file in portrait mode. The image height of the output video file corresponds to the short side of the mezzanine file or the image width of the mezzanine file in portrait mode. -   Valid values: true and false.
-   true: The auto-rotate screen is enabled.
-   false: The auto-rotate screen is disabled.
-   Default value: true.
-   This feature is applicable to videos in portrait mode.

 We recommend that you enable this feature.|
|Crf|String|No|The bitrate quality control factor. If you set this parameter, the Bitrate parameter is invalid. A greater value indicates the poorer image quality of the output video file and a smaller file size. A smaller value indicates the better image quality of the output video file, a larger file size, and a longer transcoding duration. -   Valid values: \[0, 51\].
-   Default value: 26.

 We recommend that you do not modify this parameter.|
|Profile|String|No|The codec profile. -   Valid values: baseline, main, and high.
-   Default value: high.
-   baseline: applicable to mobile devices.
-   main: applicable to standard-definition devices.
-   high: applicable to high-definition devices.
-   This parameter is valid only when H.264 encoding is performed.

 If multiple definitions exist, we recommend that you set this parameter to baseline for the lowest definition to ensure normal playback on low-end devices. Set this parameter to main or high for other definitions.|
|Preset|String|No|The preset video algorithm. -   Valid values: veryfast, fast, medium, slow, and slower.
-   Default value: medium.
-   This parameter is valid only when H.264 encoding is performed.

 We recommend that you do not modify this parameter.|
|ScanMode|String|No|The scan mode. -   interlaced
-   progressive |
|Bufsize|String|No|The size of the buffer. -   Valid values: \[1000, 128000\].
-   Default value: 6000.
-   Unit: KB. |
|Maxrate|String|No|The maximum video bitrate. -   Valid values: \[1000,50000\].
-   Unit: Kbit/s. |
|PixFmt|String|No|The pixel format for video color encoding. -   Valid values: standard pixel formats such as yuv420p and yuvj420p
-   Default value: yuv420p or the original color format |

## Examples of the Video parameter

```
{
	"Codec":"H.264",
	"Bitrate":"128",
	"Remove":"false",
	"Width":"640",
	"Fps":"30"
}
			
```

## Audio

**Note:** Unless otherwise required, you need only to set the Codec and Bitrate parameters and set the Remove parameter to false.

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Codec|String|Yes|The codec format of the audio file. Valid values: AAC and MP3.|
|Bitrate|String|Yes|The bitrate of the output audio file. -   Valid values: \[8,1000\].
-   Unit: Kbit/s. |
|Remove|String|Yes|Indicates whether the audio stream is deleted. Valid values: true and false. -   A value of true indicates that the audio stream is deleted from the output audio file.
-   A value of false indicates that the audio stream is retained for the output audio file.
-   Default value: false. |
|Samplerate|String|Yes|The sample rate. -   Valid values: 22050, 32000, 44100, 48000, and 96000.
-   Default value: 44100.
-   Unit: Hz.
-   If the container format for the video files is FLV and the codec format for the audio files is MP3, this parameter cannot be set to 32000, 48000, or 96000.
-   If the codec format for the audio files is MP3, this parameter cannot be set to 96000. |
|Channels|String|No|The number of sound channels. -   Default value: 2.
-   If the Codec parameter is set to MP3, this parameter can be set only to 1 or 2.
-   If the Codec parameter is set to AAC, this parameter can be set only to 1, 2, 4, 5, 6, or 8. |
|Profile|String|No|The codec profile of the audio file. -   If the Codec parameter is set to AAC, the following valid values are included: aac\_low, aac\_he, aac\_he\_v2, aac\_ld, and aac\_eld. |
|Volume|[Volume](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#Volume)|No|The volume.|

## Example of the Audio parameter

```
{
	"Codec":"AAC",
	"Bitrate":"128",
	"Remove":"false",
	"Samplerate":"44100"
}
			
```

## Container

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Format|String|Yes|The container format. -   For video transcoding, this parameter can be set to flv, mp4, or HLS \(m3u8+ts\).
-   For audio transcoding, this parameter can be set to mp3 or mp4
-   If this parameter is set to flv, the Codec parameter in the Video table cannot be set to H.265. |

## Example of the Container parameter

```
{
	"Format":"mp4"
}
			
```

## MuxConfig

**Note:** You must set this parameter if the container format is M3U8.

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Segment|[Segment](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#Segment)|Yes|The segment configurations. The value is a JSON object.|

## Segment

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Duration|String|Yes|The duration of the TS segment. The value is an integer. -   Valid values: \[1, 60\].
-   Unit: seconds.
-   Example: \{"Duration":"10"\}. |

## Example of the MuxConfig parameter

```
{
	"Segment":{
		"Duration":"10"
	}
}
			
```

## TransConfig

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|TransMode|String|No|The transcoding mode. -   Valid values: onepass, twopass, and CBR.
-   Default value: onepass. |
|IsCheckReso|String|No|Indicates whether the resolution of the mezzanine file is checked. Then, ApsaraVideo VOD determines whether to use the resolution of the mezzanine file for transcoding based on the check result. -   true: indicates that the resolution of the mezzanine file is checked. If ApsaraVideo VOD determines that the resolution of the output file is higher than the resolution of the mezzanine file based on the width or height, the resolution of the mezzanine file is retained after transcoding.
-   false: indicates that the resolution of the mezzanine file is not checked.
-   Default value: false. |
|IsCheckResoFail|String|No|Indicates whether the resolution of the mezzanine file is checked to determine a transcoding failure. -   true: indicates that the resolution of the mezzanine file is checked. If ApsaraVideo VOD determines that the resolution of the output file is higher than the resolution of the mezzanine file based on the width or height, an error that indicates a transcoding failure is returned.
-   false: indicates that the resolution of the mezzanine file is not checked.
-   Default value: false. |
|IsCheckVideoBitrate|String|No|Indicates whether the video stream bitrate of the mezzanine file is checked. Then, ApsaraVideo VOD determines whether to use the video stream bitrate of the mezzanine file for transcoding based on the check result. -   true: indicates that the video stream bitrate of the mezzanine file is checked. If ApsaraVideo VOD determines that the video stream bitrate of the output file is greater than the video stream bitrate of the mezzanine file, the video stream bitrate of the mezzanine file is retained after transcoding.
-   false: indicates that the video stream bitrate of the mezzanine file is not checked.
-   Default value: false. |
|IsCheckVideoBitrateFail|String|No|Indicates whether the video stream bitrate of the mezzanine file is checked to determine a transcoding failure. -   true: indicates that the video stream bitrate of the mezzanine file is checked. If ApsaraVideo VOD determines that the video stream bitrate of the output file is greater than the video stream bitrate of the mezzanine file, no transcoding is performed.
-   false: indicates that the video stream bitrate of the mezzanine file is not checked.
-   Default value: false.
-   This parameter has a greater priority than the IsCheckVideoBitrate parameter. |
|IsCheckAudioBitrate|String|No|Indicates whether the audio stream bitrate of the mezzanine file is checked. Then, ApsaraVideo VOD determines whether to use the audio stream bitrate of the mezzanine file for transcoding based on the check result. -   true: indicates that the audio stream bitrate of the mezzanine file is checked. If ApsaraVideo VOD determines that the audio stream bitrate of the output file is greater than the audio stream bitrate of the mezzanine file, the audio stream bitrate of the mezzanine file is retained after transcoding.
-   false: indicates that the audio stream bitrate of the mezzanine file is not checked.
-   Default value: false. |
|IsCheckAudioBitrateFail|String|No|Indicates whether the audio stream bitrate of the mezzanine file is checked to determine a transcoding failure. -   true: indicates that the audio stream bitrate of the mezzanine file is checked. If ApsaraVideo VOD determines that the audio stream bitrate of the output file is greater than the audio stream bitrate of the mezzanine file, no transcoding is performed.
-   false: indicates that the audio stream bitrate of the mezzanine file is not checked.
-   Default value: false.
-   This parameter has a greater priority than the IsCheckAudioBitrate parameter. |

## Example of the TransConfig parameter

```
{
	"IsCheckReso":"true",
	"IsCheckResoFail":"false",
	"IsCheckVideoBitrate":"false",
	"IsCheckVideoBitrateFail":"false",
	"IsCheckAudioBitrate":"false",
	"IsCheckAudioBitrateFail":"false"
}
			
```

## Clip

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|TimeSpan|[TimeSpan](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#Timespan)|Yes|The configurations related to the time span used to crop a video.|

## TimeSpan

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Seek|String|Yes|The start time of the captured part of the video. Format 1 \(**recommended**\):

 -   sssss\[.SSS\]
-   Valid values: \[0.000, 86399.999\].
-   Example: 12000.556.

 Format 2:

 -   hh:mm:ss\[.SSS\]
-   Valid values: \[00:00:00.000, 23:59:59.999\].
-   Example: 00:00:05.003. |
|Duration|String|No|The duration of the captured part of the video. Format 1 \(**recommended**\):

 -   sssss\[.SSS\]
-   Valid values: \[0.000, 86399.999\].
-   Example: 12000.556.

 Format 2:

 -   hh:mm:ss\[.SSS\]
-   Valid values: \[00:00:00.000, 23:59:59.999\].
-   Example: 00:00:05.003. |
|End|String|No|The duration of the remaining part of the video after video cropping. Format 1 \(**recommended**\):

 -   sssss\[.SSS\]
-   Valid values: \[0.000, 86399.999\].
-   Example: 12000.556.

 Format 2:

 -   hh:mm:ss\[.SSS\]
-   Valid values: \[00:00:00.000, 23:59:59.999\].
-   Example: 00:00:05.003.

 Note:

 -   If you set this parameter, the Duration parameter is invalid.
-   The sum of the Seek and End parameter values cannot be greater than the total video duration. |

**Note:** Note: Set only one of the Duration and End parameters.

## EncryptSetting

**Note:** You must set the EncryptType parameter to AliyunVoDEncryption and call the [SubmitTranscodeJobs](https://help.aliyun.com/document_detail/68570.html) operation to start the HLS encryption.

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|EncryptType|String|Yes|The encryption type. -   Set the value to AliyunVoDEncryption. This parameter is valid only for the M3U8 \(HLS\) format. |

## Example of the EncryptSetting parameter

```
{
	"EncryptType":"AliyunVoDEncryption"
}
			
```

## PackageSetting

**Note:**

-   You cannot package video and audio streams after you extract them from files.
-   Only HLS packaging is supported.

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|PackageType|String|Yes|The packaging type. -   Set the value to **HLSPackage**. |
|PackageConfig|[PackageConfig](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#packageconfig)|No|The packaging configurations. You must set this parameter if a video stream package template is used for transcoding.****|
|SubtitleExtractConfigList|[SubtitleExtractConfig\[\]](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#SubtitleExtractConfig)|No|The subtitle packaging configurations. You must set this parameter only when a subtitle package template is used for transcoding.****|

## PackageConfig

**Note:** You must set this parameter only when the PackageType parameter is set to HLSPackage.

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|BandWidth|String|Yes|The maximum bandwidth. You must set this parameter for HLS packaging. -   You must set this parameter only when a video stream package template is used for transcoding.****
-   Unit: bit/s. |

## SubtitleExtractConfig

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|SubtitleUrlList|String\[\]|Yes|The OSS URL of subtitle files. The OSS URLs must be HTTP URLs. CDN URLs and HTTPS URLs are not supported. -   Note: You can specify only one HTTP URL.
-   You can store subtitle files only in the buckets that are allocated by ApsaraVideo VOD. |
|Language|String|Yes|The tag of the subtitle language, such as en-US. For more information, see RFC 5646.|
|Format|String|Yes|The format of subtitle files. Only .vtt files are supported. Example: subtitle.vtt.|
|Name|String|Yes|The display name of the subtitle in the player, such as Chinese and English.|

## Examples of the PackageSetting parameter

```
Sample code for configuring a video stream package template:
{
	"PackageType":"HLSPackage",
	"PackageConfig":{
		"BandWidth":"400000"
	}
}
			
```

```
Sample code for configuring a subtitle package template:
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
			
```

## SubtitleConfig

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|SubtitleUrl|String|Yes|The OSS URL of the subtitle file. **HTTPS URLs and CDN URLs are not supported.** Note:

 -   The subtitle file and video mezzanine file must be stored in the same bucket in the same region, for example, the China \(Shanghai\) region.****
-   Subtitle formats: **srt and ass**. |
|CharEnc|String|Yes|The encoding format of the subtitle file. -   Valid values: auto, UTF-8, GBK, and BIG5. A value of auto indicates that the system automatically identifies the encoding format.
-   Default value: UTF-8 |

**Note:** For more information about how to upload a subtitle file, see [CreateUploadAttachedMedia](https://help.aliyun.com/document_detail/98467.html) and [Upload OSS objects](https://help.aliyun.com/document_detail/55538.html).

## Example of the SubtitleConfig parameter

```
{
	"SubtitleUrl": "http://outin-40564284ef058b2d300163e1403e7.oss-cn-shanghai.aliyuncs.com/subtitles/c737f-14f1-4364-b107-d5f7f8edde0e.ass",
	"CharEncode": "UTF-8"
}
			
```

## Example of the SubtitleList parameter

```
[
	{
		"SubtitleUrl": "http://outin-40564284ef058b2163e1403e7.oss-cn-shanghai.aliyuncs.com/subtitles/c737f-14f1-4364-b107-d5f7f8edde0e-cn.ass",
		"CharEncode": "UTF-8"
	},
	{
		"SubtitleUrl": "http://outin-40564284ef058b2d3001403e7.oss-cn-shanghai.aliyuncs.com/subtitles/rrrr-14f1-4364-b107-d5f7f8edde0e-en.srt",
		"CharEncode": "auto"
	}
]

			
```

## Volume

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Method|String|No|The volume adjustment method. Valid values: auto, dynamic, and linear.|
|IntegratedLoudnessTarget|String|No|The new volume. Valid values: \[-70, -5\]. Default value: -6. This parameter is valid only when the Method parameter is set to dynamic.|
|TruePeak|String|No|The peak volume. Valid values: \[-9, 0\]. This parameter is valid only when the Method parameter is set to dynamic. Default value: -1.|
|LoudnessRangeTarget|String|No|The range of the volume. Valid values: \[1, 20\]. This parameter is valid only when the Method parameter is set to dynamic. Default value: 8.|

## Example of the Volume parameter

```
{
	"Method":"dynamic",
	"IntegratedLoudnessTarget":"auto",
	"TruePeak":"-1",
	"LoudnessRangeTarget":"8"
}
			
```

## Supported combinations of container formats and audio codec formats

|Container|Audio Codecs|
|---------|------------|
|mp3|MP3|
|mp4|AAC|
|ogg|VORBIS and FLAC|
|flac|FLAC|

## Supported combinations of audio codec formats and video codec formats

|Container|Video Codecs|Audio Codecs|
|---------|------------|------------|
|flv|H.264|AAC and MP3|
|mp4|H.264 and H.265|AAC and MP3|
|ts|H.264 and H.265|AAC and MP3|
|m3u8|H.264 and H.265|AAC and MP3|
|gif|GIF|Not supported|

## Supported combinations of video codec formats and video stream parameters

|Video Codecs|H.264|H.265|GIF|
|------------|-----|-----|---|
|Profile|√|×|×|
|Bitrate|√|√|×|
|Crf|√|√|×|
|Width|√|√|√|
|Height|√|√|√|
|Fps|√|√|√|
|Gop|√|√|×|
|Preset|√|×|×|
|ScanMode|√|√|√|
|Bufsize|√|√|×|
|Maxrate|√|√|×|
|PixFmt|√|√|bgr8|

## TranscodeSummary

|Parameter|Type|Description|
|---------|----|-----------|
|VideoId|String|The ID of the video.|
|TranscodeTemplateGroupId|String|The ID of the transcoding template group.|
|TranscodeStatus|String|The transcoding status. -   Processing: The transcoding is in progress.
-   Partial: The video was partially transcoded.
-   CompleteAllSucc: All the transcoding jobs are complete and the video is fully transcoded.
-   CompleteAllFail: All the transcoding jobs are complete but the video fails to be transcoded. If an exception occurs in the mezzanine file, no transcoding job is initiated and the transcoding task fails.
-   CompletePartialSucc: All the transcoding jobs are complete but the video is partially transcoded. |
|TranscodeJobInfoSummaryList|[TranscodeJobInfoSummary](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#TranscodeJobInfoSummary)\[\]|The summaries of transcoding jobs.|
|CreationTime|String|The time when the transcoding task was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.|
|CompleteTime|String|The time when the transcoding task was complete. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.|

## TranscodeJobInfoSummary

|Parameter|Type|Description|
|---------|----|-----------|
|TranscodeTemplateId|String|The ID of the transcoding template.|
|Width|String|The image width of the output video. Unit: pixel.|
|Height|String|The image height of the output video. Unit: pixel.|
|Duration|String|The duration of the output video. Unit: seconds.|
|Filesize|String|The size of the output video file. Unit: byte.|
|Bitrate|String|The average bitrate of the output video. Unit: Kbit/s.|
|Fps|String|The frame rate of the output video. Unit: frames per second.|
|Format|String|The container format of the output video.|
|WatermarkIdList|String\[\]|The ID list of watermarks that are applied to the output video.|
|TranscodeProgress|Long|The transcoding progress. -   Valid values: \[0, 100\]. |
|TranscodeJobStatus|String|The status of the transcoding job. -   Transcoding: The transcoding job is running.
-   TranscodeSuccess: The transcoding job is successful.
-   TranscodeFail: The transcoding job fails. |
|CreationTime|String|The time when the transcoding job was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.|
|CompleteTime|String|The time when the transcoding job was complete. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.|
|ErrorCode|String|The error code that is returned when the transcoding job fails.|
|ErrorMessage|String|The error message that is returned when the transcoding job fails.|

## TranscodeTask

|Parameter|Type|Description|
|---------|----|-----------|
|TranscodeTaskId|String|The ID of the transcoding task.|
|TranscodeTemplateGroupId|String|The ID of the transcoding template group.|
|VideoId|String|The ID of the video.|
|TaskStatus|String|The status of the transcoding task. Valid values: -   Processing: The transcoding is in progress.
-   Partial: The video was partially transcoded.
-   CompleteAllSucc: All the transcoding jobs are complete and the video is fully transcoded.
-   CompleteAllFail: All the transcoding jobs are complete but the video fails to be transcoded. If an exception occurs in the mezzanine file, no transcoding job is initiated and the transcoding task fails.
-   CompletePartialSucc: All the transcoding jobs are complete but the video is partially transcoded. |
|CreationTime|String|The time when the transcoding task was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.|
|CompleteTime|String|The time when the transcoding task was complete. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC.|
|Trigger|String|The trigger type. Valid values: -   Auto: The transcoding is automatically triggered after a video is uploaded.
-   Manual: The transcoding is triggered by calling the [SubmitTranscodeJobs](https://help.aliyun.com/document_detail/68570.html?spm=a2c4g.11186623.2.136.4ff12b8bE3reaw) operation. |
|TranscodeJobInfoList|[TranscodeJobInfo](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#TranscodeJobInfo)|The information about transcoding jobs.|

## TranscodeJobInfo

|Parameter|Type|Description|
|---------|----|-----------|
|TranscodeTaskId|String|The ID of the transcoding task.|
|TranscodeJobId|String|The ID of the transcoding job.|
|VideoId|String|The ID of the video.|
|TranscodeProgress|Long|The progress of the transcoding job. -   Valid values: \[0, 100\]. |
|TranscodeJobStatus|String|The status of the transcoding job. -   Transcoding: The transcoding job is running.
-   TranscodeSuccess: The transcoding job is successful.
-   TranscodeFail: The transcoding job fails. |
|Priority|String|The priority of the transcoding task.|
|Definition|String|The definition. -   This parameter indicates the definition that is configured for the transcoding template and does not indicate the actual resolution range of the output video. |
|TranscodeTemplateId|String|The ID of the transcoding template.|
|CreationTime|String|The time when the transcoding job was created.|
|CompleteTime|String|The time when the transcoding job was complete.|
|InputFileUrl|String|The OSS URL of the mezzanine file.|
|OutputFile|[OutputFile](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#OutputFile)|The information about the output file.|
|ErrorCode|String|The error code that is returned when the transcoding job fails.|
|ErrorMessage|String|The error message that is returned when the transcoding job fails.|

## OutputFile

|Parameter|Type|Description|
|---------|----|-----------|
|OutputFileUrl|String|The OSS URL of the output file.|
|Format|String|The container format of the output file.|
|Width|String|The image width of the output file. Unit: pixel.|
|Height|String|The image height of the output file. Unit: pixel.|
|Duration|String|The duration of the output file. Unit: seconds.|
|Bitrate|String|The average bitrate of the output file. Unit: Kbit/s.|
|Fps|String|The frame rate of the output file. Unit: frames per second.|
|Filesize|Long|The size of the output file. Unit: byte.|
|EncryptType|String|The encryption type that is used for the output file. The value is a JSON string.|
|WatermarkIdList|String|The ID list of watermarks that are applied to the output file.|
|VideoStreamList|String|The list of video streams. For more information, see [VideoStream](https://help.aliyun.com/document_detail/52839.html#VideoStream).|
|AudioStreamList|String|The list of audio streams. For more information, see [AudioStreamList](https://help.aliyun.com/document_detail/52839.html#AudioStream).|

## ImageInfo

Specifies the information about an image.

|Parameter|Type|Description|
|---------|----|-----------|
|ImageId|String|The ID of the image.|
|URL|String|The URL of the image. If a CDN domain name was specified, a CDN URL was returned. Otherwise, an OSS URL was returned.|
|Title|String|The title of the image.|
|Tags|String|The tag of the image.|
|ImageType|String|The type of the image.|
|CateId|Long|The ID of the category.|
|CateName|String|The name of the category.|
|Description|String|The description of the image.|
|StorageLocation|String|The storage location.|
|Mezzanine|[Mezzanine](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#Mezzanine-image)|The information about the image mezzanine file.|
|CreationTime|String|The time when the image was created. The time is displayed in UTC.|
|Status|String|[The status of the image](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#ImageStatus).|
|AppId|String|[The ID of the application](https://help.aliyun.com/document_detail/113600.html#AppId).|

## Mezzanine

|Parameter|Type|Description|
|---------|----|-----------|
|FileURL|String|The OSS URL of the image mezzanine file.|
|OriginalFileName|String|The name of the image mezzanine file.|
|FileSize|Long|The size of the image mezzanine file. Unit: byte.|
|Width|Integer|The width of the image. Unit: pixel.|
|Height|Integer|The height of the image. Unit: pixel.|

## DyanmicImage

|Parameter|Type|Description|
|---------|----|-----------|
|VideoId|String|The ID of the video.|
|DynamicImageId|String|The ID of the animated sticker.|
|FileURL|String|The URL of the animated sticker file.|
|Width|String|The width of the animated sticker.|
|Height|String|The height of the animated sticker.|
|Duration|String|The duration of the animated sticker.|
|Format|String|The format of the animated sticker. Valid values: gif and webp.|
|FileSize|String|The size of the animated sticker file.|
|Fps|String|The frame rate of the animated sticker.|

## URLUploadInfo

Specifies the information about a URL-based upload job.

|Parameter|Type|Description|
|---------|----|-----------|
|JobId|String|The ID of the upload job.|
|UploadURL|String|The URL of the video to be uploaded.|
|MediaId|String|The ID of the video to be uploaded.|
|Status|String|[The status of the video](https://help.aliyun.com/document_detail/52839.html#h2--status-div-id-videostatus-div-6).|
|UploadStatus|String|[The status of the URL-based upload job](https://help.aliyun.com/document_detail/52839.html#h2-url-status-div-id-urluploadstatus-div-68).|
|CreationTime|String|The time when the upload job was created.|
|CompleteTime|Long|The time when the upload job was complete.|
|UserData|String|The custom configurations.|
|ErrorCode|String|The error code.|
|ErrorMessage|String|The error message.|

## Status

The following table describes the valid values of the Status parameter for a URL-based upload job.

|Value|Description|
|-----|-----------|
|PENDING|The job is submitted and is to be processed.|
|PROCESSING|The job is being processed.|
|DOWNLOADING|The file is being downloaded.|
|DOWNLOAD\_SUCCESS|The file is downloaded.|
|DOWNLOAD\_FAIL|The file fails to be downloaded.|
|UPLOADING|The file is being uploaded.|
|UPLOAD\_SUCCESS|The file is uploaded.|
|UPLOAD\_FAIL|The file fails to be uploaded.|
|SUCCESS|The upload job is successful and the callback is complete.|

## AttachedMediaInfo

Specifies the information about an auxiliary media asset.

|Parameter|Type|Description|
|---------|----|-----------|
|MediaId|String|The ID of the auxiliary media asset.|
|URL|String|The URL of the auxiliary media asset. If a CDN domain name was specified, a CDN URL was returned. Otherwise, an OSS URL was returned.|
|Title|String|The title of the auxiliary media asset.|
|Tags|String|The tag of the auxiliary media asset.|
|Type|String|The type of the auxiliary media asset.|
|Categories|[Category](https://help.aliyun.com/document_detail/52839.html#Category)\[\]|The list of categories.|
|Description|String|The description of the auxiliary media asset.|
|StorageLocation|String|The storage location.|
|CreationTime|String|The time when the auxiliary media asset was created. The time is displayed in UTC.|
|ModificationTime|String|The time when the auxiliary media asset was last modified. The time is displayed in UTC.|
|Status|String|[The status of the auxiliary media asset](https://help.aliyun.com/document_detail/52839.html?spm=a2c4g.11186623.6.896.4d383d45iZOVEG#AttachedMediaStatus).|
|AppId|String|[The ID of the application](https://help.aliyun.com/document_detail/113600.html#AppId).|

## Status

The following table describes the valid values of the Status parameter for an auxiliary media asset.

|Value|Description|Remarks|
|-----|-----------|-------|
|Uploading|Indicates that the auxiliary media asset is being uploaded.|The initial status, which indicates that the auxiliary media asset is being uploaded.|
|Normal|Indicates that the auxiliary media asset is uploaded.|The auxiliary media asset is uploaded.|
|UploadFail|Indicates that the auxiliary media asset fails to be uploaded.|The auxiliary media asset fails to be uploaded.|

## MessageCallback



Specifies the configuration of an event notification.

|Parameter|Type|Description|
|---------|----|-----------|
|CallbackType|String|The callback method. Valid values: HTTP and MNS.|
|CallbackURL|String|The callback URL. This parameter is returned only for HTTP callbacks.|
|MnsEndpoint|String|The public endpoint of Message Service \(MNS\). This parameter is returned only for MNS callbacks.|
|MnsQueueName|String|The name of the MNS queue. This parameter is returned only for MNS callbacks.|
|EventTypeList|String|The type of the callback event.|
|AuthSwitch|String|Indicates whether callback authentication is enabled. This parameter is returned only for HTTP callbacks. Valid values: on and off. A value of on indicates that callback authentication is enabled. A value of off indicates that callback authentication is disabled.|
|AuthKey|String|The cryptographic key. This parameter is returned only for HTTP callbacks.|

## AppInfo 

Specifies the information about an application.

|Parameter|Type|Description|
|---------|----|-----------|
|AppId|String|The ID of the application.|
|AppName|String|The name of the application.|
|Description|String|The description of the application.|
|Type|String|The type of the application. Valid values: System and Custom.|
|Status|String|The status of the application. Valid values: Normal and Disable.|
|CreationTime|String|The time when the application was created. The time is displayed in UTC.|
|ModificationTime|String|The time when the application was last modified. The time is displayed in UTC.|

## AppPolicy 

Specifies the information about an application policy.

|Parameter|Type|Description|
|---------|----|-----------|
|AppId|String|The ID of the application.|
|PolicyType|String|The type of the policy. Valid values: System and Custom.|
|PolicyName|String|The name of the policy.|
|CreationTime|String|The time when the policy was created. The time is displayed in UTC.|
|Description|String|The description of the policy.|

