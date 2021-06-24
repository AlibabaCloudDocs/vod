Parameters for media processing 
====================================================



EncryptConfig: specifies the configurations for HLS encryption 
-----------------------------------------------------------------------------------



| Parameter      | Type   | Required | Description                                                                                                                                                                             |
|:---------------|:-------|:---------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CipherText     | String | Yes      | The ciphertext key that is used to obtain the plaintext key.                                                                                                                            |
| DecryptKeyUri  | String | Yes      | The address that is used to obtain the decryption key based on the ciphertext key. Example: `http://decrypt.demo.com?CipherText=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMt`. |
| KeyServiceType | String | Yes      | The type of the key service. Default value: KMS, which indicates Key Management Service of Alibaba Cloud.                                                                               |



Example of the EncryptConfig parameter 
-----------------------------------------------------------

    {
      "CipherText":"ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMt",
      "DecryptKeyUri":"http://decrypt.demo.com?CipherText=ZjJmZGViNzUtZWY1Mi00Y2RlLTk3MTMt",
      "KeyServiceType":"KMS"
    }
                            



OverrideParams: specifies the configurations for a transcoding job 
---------------------------------------------------------------------------------------



| Parameter              | Type                                                                                               | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|:-----------------------|:---------------------------------------------------------------------------------------------------|:---------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Watermarks             | [Watermark](#section-ykp-h3o-oy6)\[\]                                           | No       | The watermark configurations. To replace a watermark, you must set this parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| SubtitleSetting        | [SubtitleSetting](#section-t9m-r4c-gci)                                         | No       | The subtitle configurations. To replace a subtitle file, you must set this parameter. 					 **Note** * Make sure that **subtitle parameters are set in advance** for the transcoding template that you use. Otherwise, you cannot modify the subtitle configurations. For more information about how to set subtitle parameters, see the "SubtitleConfig" section of the [Basic data types](/intl.en-US/API Reference/Appendix/Basic data types.md) topic.   * The new URL that is used to store subtitle files must be an **HTTP-based** Object Storage Service (OSS) URL, such as `http://out-ddawewsrrrw86223.cn-shanghai.aliyuncs.com/subtitle/subtitle.ass`. **CDN URLs and HTTPS-based OSS URLs** are not supported.    |
| PackageSubtitleSetting | [PackageSubtitleSetting](#section-9jw-gmr-4bu)\[\]                              | No       | The configurations of the subtitle package. To replace the URL that is used to store subtitle files for an adaptive bitrate streaming template, you must set this parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| TranscodeTemplateList  | [TranscodeTemplate](/intl.en-US/API Reference/Appendix/Basic data types.md)\[\] | No       | The configurations of the transcoding template. To modify the configurations of a transcoding template, you must set this parameter.  * You can modify the Video, Audio, Clip, Rotate, and TranscodeFileRegular parameters of a transcoding template.   * You cannot modify the parameters of an original quality template.   * To modify the configurations of a transcoding template, you must set the TranscodeTemplateId parameter.                                                                                                                                                                                                                                                                                                    |


**Note**

You can modify only the URL of an image watermark or the content of a text watermark.

Example of the TranscodeTemplateList parameter 
-------------------------------------------------------------------

            [
                    {
                      "TranscodeTemplateId":"9580424e49b28c952a46544e3e8f2268",
                      "Video":{
                              "Width":720,
                              "Height":480,
                              "Bitrate":"600"
                      },
                      "Audio":{
                              "Bitrate":128
                      }, 
                      "Clip":{
                              "TimeSpan":{
                                    "Seek":"1"
                                    "Duration":"5"
                            },
                      "Rotate":"270",
                      "TranscodeFileRegular":"{MediaId}/{JobId}/{PlayDefinition}"
                      }
                    }
            ]
                            



Watermark: specifies the watermark configurations 
----------------------------------------------------------------------



| Parameter   | Type   | Required | Description                                                                                                                                                                                                                                                                |
|:------------|:-------|:---------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WatermarkId | String | Yes      | The watermark ID that is associated with the transcoding template. You can query watermark IDs in the ApsaraVideo VOD console. For more information, see [Manage watermarks](/intl.en-US/User Guide/Global settings/Manage watermarks.md).                 |
| FileUrl     | String | No       | The OSS URL of the watermark file. To replace an image watermark, you must set this parameter. For more information about how to obtain OSS URLs, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md). |
| Content     | String | No       | The content of the text watermark. To replace a text watermark, you must set this parameter.                                                                                                                                                                               |


**Notice**

The OSS URL of the watermark file must belong to the same origin as the video resource.

SubtitleSetting: specifies the subtitle files 
------------------------------------------------------------------



| Parameter    | Type                                                | Required | Description         |
|:-------------|:----------------------------------------------------|:---------|:--------------------|
| SubtitleList | [Subtitle](#section-8th-hoc-yai) | Yes      | The subtitle files. |



Subtitle: specifies the subtitle configurations 
--------------------------------------------------------------------



| Parameter   | Type   | Required | Description                                                                                                                                                                                                                                                                                |
|:------------|:-------|:---------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubtitleUrl | String | Yes      | The OSS URL of the subtitle file. HTTPS-based OSS URLs are not supported.                                                                                                                                                                                                                  |
| CharEncode  | String | Yes      | The encoding format of the subtitle content. Valid values:  * auto: automatic detection   * UTF-8   * GBK   * BIG5    |



Note: We recommend that you set the CharEncode parameter to a valid encoding format based on your business requirements. If you set the parameter to auto, the detected encoding format may not be the actual encoding format.

PackageSubtitleSetting: specifies the subtitle package 
---------------------------------------------------------------------------



| Parameter           | Type                                                           | Required | Description                                                                            |
|:--------------------|:---------------------------------------------------------------|:---------|:---------------------------------------------------------------------------------------|
| PackageSubtitleList | [PackageSubtitle](#section-dyk-xxx-03o)\[\] | Yes      | The subtitle package. To replace multiple subtitle files, you must set this parameter. |



PackageSubtitleSetting: specifies the configurations for a subtitle package 
------------------------------------------------------------------------------------------------



| Parameter                 | Type   | Required | Description                                                                                                                                                                                                                                                                                               |
|:--------------------------|:-------|:---------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubtitlePackageTemplateId | String | Yes      | The ID of the subtitle package template.                                                                                                                                                                                                                                                                  |
| Language                  | String | Yes      | The tag of the subtitle language, such as en-US. For more information, see RFC 5646. 					 **Note** This parameter is used only to query the URLs of the subtitle files to be replaced and cannot be used to change the subtitle language.                                                |
| SubtitleUrl               | String | Yes      | The OSS URL of the subtitle file. The OSS URL must be an HTTP URL. CDN URLs and HTTPS-based OSS URLs are not supported. 								 **Note** You can specify only one HTTP URL.  You can store subtitle files only in the OSS buckets that are allocated by ApsaraVideo VOD. |


**Note**

The SubtitlePackageTemplateId and Language parameters are used only to query the URLs of the subtitle files to be replaced and cannot be used to change the subtitle language.

Example of the OverrideParams parameter 
------------------------------------------------------------

    {
      "Watermarks":[
        {
          "WatermarkId":"watermark1",
          "FileUrl":"http://test.bucket.aliyuncs.com/image/replace.png"
        },
        {
          "WatermarkId":"watermark2",
          "Content":"Watermark Test"
        }
      ],
      "SubtitleSetting":{
              "SubtitleList":[
                    {
                    "SubtitleUrl":"http://outin-40564284ef051100163e1403e7.oss-cn-shanghai.aliyuncs.com/subtitles/7b850b-724c-4011-b885-dd16cc112.ass",
                    "CharEncode":"UTF-8"
                    },
                    {
                    "SubtitleUrl":"http://outin-40564284ef0511e0163e1403e7.oss-cn-shanghai.aliyuncs.com/subtitles/7b86db-724c-4011-b885-dd161d1cyy.srt",
                    "CharEncode":"auto"
                    }
            ]
      },
      "PackageSubtitleSetting": {
        "PackageSubtitleList": [
          {
            "Language": "en-US",
            "SubtitlePackageTemplateId": "32d665807c08d25d4a5d513395ad6cd5", 
            "SubtitleUrl": "http://outin-4056428.oss-cn-shanghai.aliyuncs.com/789679188D1F36A00AEB7-3-3.vtt" 
          },
          {
            "Language": "ja",  
            "SubtitlePackageTemplateId": "32d665807c08d25d4a5d513395ad6cd5",
            "SubtitleUrl": "http://outin-4056428.oss-cn-shanghai.aliyuncs.com/F43FD90FF4B936A00AEB7-3-3.vtt"
          }
        ]
      }
    }
                            



WatermarkConfig: specifies the watermark configurations 
----------------------------------------------------------------------------

Parameters for image watermarks 
----------------------------------------------------



| Parameter | Type                                             | Required | Description                                                                                                                                                                                                                                                                |
|:----------|:-------------------------------------------------|:---------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Dx        | String                                           | Yes      | The horizontal offset of the watermark. The following types of values are supported:  * Pixel value: \[8,4096\]   * Image ratio: (0,1)                                  |
| Dy        | String                                           | Yes      | The vertical offset of the watermark. The following types of values are supported:  * Pixel value: \[8,4096\]   * Image ratio: (0,1)                                    |
| Width     | String                                           | Yes      | The width of the watermark. The following types of values are supported:  * Pixel value: \[8,4096\]   * Image ratio: (0,1)                                              |
| Height    | String                                           | Yes      | The height of the watermark. The following types of values are supported:  * Pixel value: \[8,4096\]   * Image ratio: (0,1)                                             |
| ReferPos  | String                                           | Yes      | The position of the watermark. Valid values: * BottomRight   * BottomLeft   * TopRight   * TopLeft    |
| Timeline  | [Timeline](#section-5xf-bk6-y12) | No       | The timeline for watermark display, including the start time and end time. The value is a JSON string.                                                                                                                                                                     |


**Notice**

This parameter is valid only for image watermarks.

Parameters for text watermarks 
---------------------------------------------------



| Parameter   | Type    | Required | Description                                                                                                           |
|:------------|:--------|:---------|:----------------------------------------------------------------------------------------------------------------------|
| Content     | String  | Yes      | The content of the text watermark. Example: "Text Watermark".                                                         |
| FontName    | String  | No       | [The name of the font.](#section-ejy-o5b-342)                                                      |
| FontColor   | String  | No       | [The color of the font.](/intl.en-US/API Reference/Appendix/Color setting parameters.md)           |
| FontAlpha   | String  | No       | The transparency of the font. Valid values: (0,1\]. Default value: 1.0.                                               |
| BorderColor | String  | No       | [The color of the font outline.](/intl.en-US/API Reference/Appendix/Color setting parameters.md)   |
| Top         | Integer | No       | The top margin of the text watermark. Only integer values are supported. Default value: 0. Valid values: \[0,4096\].  |
| Left        | Integer | No       | The left margin of the text watermark. Only integer values are supported. Default value: 0. Valid values: \[0,4096\]. |
| FontSize    | Integer | No       | The size of the font. Only integer values are supported. Default value: 16. Valid values: (4,120).                    |
| BorderWidth | Integer | No       | The width of the font outline. Only integer values are supported. Default value: 0. Valid values: \[0,4096\].         |



Timeline: specifies the configurations for a watermark timeline 
------------------------------------------------------------------------------------



| Parameter | Type   | Required | Description                                                                                                                                                                              |
|:----------|:-------|:---------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Start     | String | Yes      | The beginning of the time range in which the watermark is displayed. Unit: seconds. Valid values: positive numbers. Default value: 0.                                                    |
| Duration  | String | Yes      | The time range in which the watermark is displayed. Unit: seconds. Valid values: \[The value of the Start parameter,ToEND\]. Default value: ToEND, which indicates the end of the video. |


**Notice**

This parameter is valid only for image watermarks.

SnapshotTemplateConfig: specifies the configurations for a snapshot template 
-------------------------------------------------------------------------------------------------



| Parameter      | Type                                                      | Required | Description                                                                                                                                                                                                                                                          |
|:---------------|:----------------------------------------------------------|:---------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SnapshotType   | String                                                    | Yes      | * The snapshot type. Valid values: NormalSnapshot: normal snapshot   * SpriteSnapshot: image sprite   * WebVttSnapshot: WebVTT-based snapshot    |
| SnapshotConfig | [SnapshotConfig](#section-qol-rks-z3h) | Yes      | The snapshot configurations, which vary with the snapshot type. The value is a JSON string.                                                                                                                                                                          |



SnapshotConfig: specifies the configurations for normal snapshots 
--------------------------------------------------------------------------------------



| Parameter            | Type                                                            | Required | Description                                                                                                                                                                                                                           |
|:---------------------|:----------------------------------------------------------------|:---------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FrameType            | String                                                          | Yes      | The frame type of the snapshots. Valid values: * intra: keyframes   * normal: normal frames                                        |
| Count                | Long                                                            | Yes      | The number of snapshots to be captured.                                                                                                                                                                                               |
| Interval             | Long                                                            | Yes      | The snapshot interval. The value must be greater than or equal to 0. Unit: seconds. If you set this parameter to 0, snapshots are captured at even intervals based on the video duration divided by the value of the Count parameter. |
| SpecifiedOffsetTime  | Long                                                            | Yes      | The point in time when the first snapshot is captured. Unit: milliseconds.                                                                                                                                                            |
| Width                | Integer                                                         | No       | The width of each snapshot. Valid values: \[8,4096\]. By default, the width of the video resource file is used. Unit: pixel.                                                                                                          |
| Height               | Integer                                                         | No       | The height of each snapshot. Valid values: \[8,4096\]. By default, the height of the video resource file is used. Unit: pixel.                                                                                                        |
| SpriteSnapshotConfig | [SpriteSnapshotConfig](#section-lrx-0eq-7o7) | No       | The snapshot configurations for image sprites. To capture image sprites, you must set this parameter.                                                                                                                                 |
| Format               | String                                                          | No       | The file format. Set the value to vtt. This parameter only takes effect when the SnapshotType parameter is set to WebVttSnapshot.                                                                                                     |
| SubOut               | [SubOut](#section-9m6-ohc-eq8)               | No       | Specifies how snapshots are displayed. This parameter only takes effect when the SnapshotType parameter is set to WebVttSnapshot.                                                                                                     |


**Note**

An image sprite is composed of multiple normal snapshots. Therefore, the SnapshotConfig parameter is required for both image sprites and normal snapshots.

SubOut 
---------------------------



| Parameter | Type   | Required | Description                                                                                                                                                                                                                                                                                     |
|:----------|:-------|:---------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| IsSptFrag | String | Yes      | Specifies how snapshots are stored. Valid values: * false: separately stores each snapshot.   * true: combines multiple snapshots to produce an image sprite and stores the image sprite.    |



SpriteSnapshotConfig: specifies the configurations for capturing image sprites 
---------------------------------------------------------------------------------------------------



| Parameter   | Type   | Required | Description                                                                                                                                                                                                             |
|:------------|:-------|:---------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CellWidth   | String | No       | The width of the original snapshots that compose the image sprite. Default value: the width of a normal snapshot. Unit: pixel.                                                                                          |
| CellHeight  | String | No       | The height of the original snapshots that compose the image sprite. Default value: the height of a normal snapshot. Unit: pixel.                                                                                        |
| Padding     | String | Yes      | The padding of the original snapshots that compose the image sprite. Unit: pixel.                                                                                                                                       |
| Margin      | String | Yes      | The margin of the original snapshots that compose the image sprite. Unit: pixel.                                                                                                                                        |
| Color       | String | Yes      | The background color of the image sprite. For more information, see [Color setting parameters](/intl.en-US/API Reference/Appendix/Color setting parameters.md).                                      |
| Columns     | String | Yes      | The number of columns for the original snapshots that compose the image sprite. Valid values: \[1,10000\].                                                                                                              |
| Lines       | String | Yes      | The number of rows for the original snapshots that compose the image sprite. Valid values: \[1,10000\].                                                                                                                 |
| KeepCellPic | String | Yes      | Specifies whether to retain the original snapshots that compose the image sprite. Valid values: * keep   * delete    |



Note: You cannot set background colors by using RGB values.

Parameter values for font names 
----------------------------------------------------



| Font name               | Description             |
|:------------------------|:------------------------|
| SimSun                  | SimSum                  |
| WenQuanYi Zen Hei       | WenQuanYi Zen Hei       |
| WenQuanYi Zen Hei Mono  | WenQuanYi Zen Hei Mono  |
| WenQuanYi Zen Hei Sharp | WenQuanYi Zen Hei Sharp |
| Yuanti SC               | Yuanti SC               |


