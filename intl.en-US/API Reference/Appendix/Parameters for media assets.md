Parameters for media assets 
================================================



Specification 
----------------------------------

This parameter specifies the output specifications of transcoded audio and videos. Transcoding fees vary with different output specifications. For more information about the billing rules, see [Billing of basic services](https://www.aliyun.com/price/product#/vod/detail). The following table describes the values of the Specification parameter. 
**Notice**

* The output resolutions are divided into several open or closed intervals.

  

* For more information about the parameter values that indicate different levels of video definition, see the "[Definition](#section-z5u-6by-yqi)" section of this topic.

  

* The specifications and definition of an output video are determined based on the `resolution` range where the long side and short side of the video image fall. If the long side or short side exceeds the specified resolution range, the output video has higher specifications and definition.

  





|         Value          | Encoding format |         Resolution         |      Transcoding type       |  Definition and audio quality  |
|------------------------|-----------------|----------------------------|-----------------------------|--------------------------------|
| Original               | -               | -                          | Mezzanine file              | Original quality               |
| Segmentation           | -               | -                          | Container format conversion | Original quality               |
| Audio                  | -               | -                          | Audio transcoding           | Standard or high sound quality |
| H264.LD                | H.264           | \[128 x 128,640 x 480\]    | Common transcoding          | Low definition                 |
| H264.SD                | H.264           | (640 x 480,1280 x 720\]    | Common transcoding          | Standard or high definition    |
| H264.HD                | H.264           | (1280 x 720,1920 x 1080\]  | Common transcoding          | Ultra high definition          |
| H264.2K                | H.264           | (1920 x 1080,2560 x 1440\] | Common transcoding          | 2K                             |
| H264.4K                | H.264           | (2560 x 1440,3840 x 2160\] | Common transcoding          | 4K                             |
| H264.LD.NarrowBandHDV1 | H.264           | \[128 x 128,640 x 480\]    | Narrowband HD™ 1.0          | Low definition                 |
| H264.SD.NarrowBandHDV1 | H.264           | (640 x 480,1280 x 720\]    | Narrowband HD™ 1.0          | Standard or high definition    |
| H264.HD.NarrowBandHDV1 | H.264           | (1280 x 720,1920 x 1080\]  | Narrowband HD™ 1.0          | Ultra high definition          |
| H264.2K.NarrowBandHDV1 | H.264           | (1920 x 1080,2560 x 1440\] | Narrowband HD™ 1.0          | 2K                             |
| H264.4K.NarrowBandHDV1 | H.264           | (2560 x 1440,3840 x 2160\] | Narrowband HD™ 1.0          | 4K                             |



Definition 
-------------------------------

This parameter specifies the video definition that is used when you call the [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md) operation, or use [ApsaraVideo Player SDK]() to play a video. The following table describes the values of the Definition parameter.
**Note**

The output resolutions are divided into several open or closed intervals.


| Value |                                                                                                                                                             Description                                                                                                                                                             |         Resolution         |
|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| FD    | Low definition                                                                                                                                                                                                                                                                                                                      | \[128 x 128,640 x 480\]    |
| LD    | Standard definition                                                                                                                                                                                                                                                                                                                 | (640 x 480,720 x 540\]     |
| SD    | High definition                                                                                                                                                                                                                                                                                                                     | (720 x 540,1280 x 720\]    |
| HD    | Ultra high definition                                                                                                                                                                                                                                                                                                               | (1280 x 720,1920 x 1080\]  |
| 2K    | 2K                                                                                                                                                                                                                                                                                                                                  | (1920 x 1080,2560 x 1440\] |
| 4K    | 4K                                                                                                                                                                                                                                                                                                                                  | (2560 x 1440,3840 x 2160\] |
| OD    | Original quality                                                                                                                                                                                                                                                                                                                    | Same as the mezzanine file |
| SQ    | Standard sound quality                                                                                                                                                                                                                                                                                                              | -                          |
| HQ    | High sound quality                                                                                                                                                                                                                                                                                                                  | -                          |
| AUTO  | Indicates an adaptive bitrate. Videos of the AUTO definition are generated only if the PackageSetting parameter is set in the transcoding template that you use. For more information, see the "PackageSetting" section of the [Basic data types](/intl.en-US/API Reference/Appendix/Basic data types.md) topic. | -                          |


