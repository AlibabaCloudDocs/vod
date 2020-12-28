# Manage transcoding settings

ApsaraVideo VOD provides the transcoding feature. You can select and configure a transcoding template to transcode videos based on your business requirements.

## Feature description

After you upload your videos, you must configure the transcoding settings. You can select a normal transcoding template or the No Transcoding template based on your business requirements.

-   Normal transcoding template: Video mezzanine files are transcoded to videos in required container formats and definitions for playback. Normal transcoding templates apply to long videos.

    The definition options include low definition \(LD\), standard definition \(SD\), high definition \(HD\), ultra high definition \(ultra HD\), original quality, 2K, 4K, high sound quality, and standard sound quality. You can customize bitrates, resolutions, and formats for videos in different definitions. You can also categorize and manage different transcoding templates in transcoding template groups.

    If you are a new customer, we recommend that you use the built-in template group **TranscodeTemplateGroup**. The built-in template group provides common parameters such as the definition, bitrate, and resolution. You can set the format, watermark template, and encryption method for transcoding.

-   No Transcoding template: Video mezzanine files are directly used as video streams. This template applies to videos that require special processing, such as short videos.

    If you select this template, ApsaraVideo VOD automatically distributes video mezzanine files and writes the file information to video stream information. This way, you can call the GetPlayInfo operation to obtain the video playback URLs. This template is often used in scenarios such as short video and live-to-VOD scenarios. You can directly play the video mezzanine files.

    By default, the built-in template group **No Transcoding** is used after you activate the ApsaraVideo VOD service.


**Note:**

-   You are charged for transcoding. For more information, see [Billing standards](https://www.aliyun.com/price/product?spm=5176.2020520107.0.0.719a83833KlNbP#/vod/detail).
-   If you set the Definition parameter to **Original**, the original definition and bitrate of videos are retained. You can modify only the container format of videos. This mode applies to scenarios where you do not need to adjust the size or bitrate of videos. In addition, if you select the **No Transcoding** template group, the CDN URL of your video points to the video in the original quality.
-   Transcoding fees are calculated based on the width and height of the video resolution, which may be different from the definition that is specified in the transcoding template.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **Media Processing** \> **Transcode**. The Transcode page appears.

    By default, the **No Transcoding** template group is used after you activate the ApsaraVideo VOD service. The system also provides the **TranscodeTemplateGroup** built-in template group.

    ![Transcode](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6056348061/p172491.png)

4.  Click **Create Template**. The Added Transcoding Template Group page appears.

    Add a transcoding template group as needed on this page if the **No Transcoding** and **TranscodeTemplateGroup** template groups cannot meet your requirements.

    ![Transcode](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7056348061/p174476.png)

5.  Click **Set as Default** to set the template group as the default one.

    ![Set as Default](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7056348061/p174513.png)

    You can click **View** to view the configuration of the template group, and click **Edit** to modify the configuration. You can click **Delete** to delete the template group that is no longer needed.


## Add a transcoding template group

After you click Set as Default for the TranscodeTemplateGroup template group, this template group is used by default. The TranscodeTemplateGroup template group contains only two templates, which support LD videos in the HTTP Live Streaming \(HLS\) and MP4 formats.

**Note:** When you add a template to the built-in template group, you cannot modify the resolution or bitrate of the template. By default, the following definitions are accordingly set: LD \(640 × 360\), SD \(960 × 540\), HD \(1280 × 720\), ultra HD \(1920 × 1080\), or original quality.

You can customize the template group by adding a normal transcoding template.

![Transcoding template](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7056348061/p182466.png)

The following table describes the transcoding template parameters.

|No.|Type|Parameter|Description|
|---|----|---------|-----------|
|①|Basic parameters|Encapsulation Format|-   Valid values for videos: hls, mp4, and flv.
-   Valid value for audio: mp3.

For more information about each container format, see [t1959239.md\#](/intl.en-US/Introduction/Glossary.md). |
|Definition|-   Valid values for videos: Low Definition, Standard Definition, High Definition, Ultra High Definition, 2K, 4K, and Original.
-   Valid values for audio: Standard Quality and High Quality. |
|②|Video parameters|Disable Video|If you select Disable Video, the transcoded stream does not contain video information. Generally, you can select Disable Video to extract audio, for example, in the radio station scenario.|
|Encoding Format|Valid values: H.264 and H.265.|
|Bitrate|Valid values: 10 to 50000, in Kbit/s. The bitrate is used to control the definition. We recommend that you use the recommended bitrate for each definition.|
|Resolution|Valid values of the width or height: 128 to 4096, in pixels. You only need to set one side of the width and height. The other side is automatically set based on the aspect ratio of the video mezzanine file.|
|Frame Rate|The number of frames per second. We recommend that you use the recommended frame rate for each definition.|
|Maximum Keyframe Interval|The number of frames in a group of pictures \(GOP\). We recommend that you use the recommended value for each definition.|
|Watermark|Specifies whether to add watermarks to a video. To add watermarks to a video, you must add watermark materials in watermark settings and select this check box. For more information, see [Watermark management](/intl.en-US/User Guide/Global settings/Manage watermarks.md).|
|③|Audio parameters|Disable Audio|If you select Disable Audio, the transcoded stream does not contain audio information. If you want to generate a video stream with no sound, select this check box.|
|Encoding Format|Valid values for the HLS and MP4 container formats: AAC and MP3. Valid value for the MP3 container format: MP3.|
|Sample Rate|We recommend that you use the recommended value.|
|Bitrate|Valid values: 8 to 1000, in Kbit/s. We recommend that you use the recommended value.|
|Audio Channels|We recommend that you use the recommended value.|
|④|Advanced parameter \(available when the container format is set to HLS\)|Fragment Length|The duration of each TS fragment. We recommend that you use the recommended value.|
|Video Encryption|Videos of the HLS format support encryption. After you enable video encryption, you must integrate an official player SDK that supports video decryption to play videos. This service offers free trial.**Note:** The video encryption feature that is configured here encrypts videos in Alibaba Cloud proprietary cryptography mode. For more information about how to encrypt videos in HLS Encryption mode, see [t1235535.md\#](/intl.en-US/API Reference/Media processing/Initiate Process/SubmitTranscodeJobs.md). |
|⑤|Conditional transcoding parameters|Video Resolution Check|Checks whether the input resolution is lower than the resolution that is specified in the transcoding template.|
|Video Bit Rate Check|Checks whether the bitrate of the video mezzanine file is lower than the bitrate that is specified in the transcoding template.|
|Audio Bit Rate Check|Checks whether the bitrate of the audio mezzanine file is lower than the bitrate that is specified in the transcoding template.|

**Note:**

-   The changes of transcoding settings apply only to newly uploaded videos.
-   To avoid transcoding failures, do not modify or delete the template or template group when a transcoding job is in progress.

The following table describes the recommended bitrate, recommended resolution, and resolution range for different definitions.

|Definition|Recommended bitrate|Recommended resolution|Resolution range|
|----------|-------------------|----------------------|----------------|
|LD|400|640x360|128x128~640x360|
|SD|900|960x540|641x361~960x540|
|HD|1500|1280x720|961x541~1280x720|
|Ultra HD|3000|1920x1080|1281x721~1920x1080|
|2K|3500|2560x1440|1920x1080 ~2560x1440|
|4K|6000|2560x1440|2560x1440 ~ 3840x2160|

Based on the proprietary transcoding technology of Alibaba Cloud, Narrowband HD™ 1.0 intelligently analyzes each scene, action, content, and texture of a video. This reduces the bitrate and bandwidth cost without compromising the video quality.

ApsaraVideo VOD presets multiple definitions that support Narrowband HD™. Narrowband HD™ transcoding supports the MP4, Flash Video \(FLV\), and HLS formats. The following table describes the parameters of transcoded videos.

|Definition|Bitrate range|Width of the resolution, in pixels|
|----------|-------------|----------------------------------|
|LD|≤ 400|640|
|SD|≤ 800|848|
|HD|≤ 1500|1280|
|Ultra HD|≤ 3000|1920|
|2K|≤ 4000|2048|
|4K|≤ 8000|3840|

