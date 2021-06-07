# Use the online editing service

This topic describes the features of the online editing service. This topic also describes how to use the online editing service in the ApsaraVideo VOD console.

## Online editing environment

**Note:**

-   The online editing service is newly upgraded. To experience the latest version of the online editing service, go to the [Intelligent Cloud Editing \(ICE\) console](https://ice.console.aliyun.com/mediaEdit/list).
-   The ICE console is available only in the China \(Beijing\) and China \(Shanghai\) regions. The ICE API is available only in the China \(Beijing\), China \(Shanghai\), and China \(Hangzhou\) regions.

To use the online editing service, you must use Google Chrome. The following table describes the formats of media assets that you can edit by using the online editing service.

|Type|Format|
|----|------|
|Video|MP4|
|Image|PNG and JPG|
|Audio|MP3|

**Note:** To edit media assets in other formats, we recommend that you transcode the media assets to a suitable format that is described in the preceding table. For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).

## Online editing GUI

The following figure shows the graphical user interface \(GUI\) for online editing.

![Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1086503261/p240210.jpg)

-   Material area \(1 in the preceding figure\)
-   Video preview area \(2 in the preceding figure\)
-   Track editing area \(3 in the preceding figure\)

## Features

Basic editing

|Feature|Description|
|-------|-----------|
|Cut a single video track into clips and merge multiple clips.|You can cut a single video track into clips and merge multiple clips. For example, you can cut a single video track with the starting part, ending part, or middle part retained, and merge clips of required parts.|
|Overlay text or images on a single video track.|You can overlay banner text, images, static watermarks, or animated image watermarks on a single video track. In addition, you can overlay such content on the video track from the start time to the end time of the video track, on specified areas of the video track, or in specified intervals along the timeline of the video track.|
|Blur specified areas of a single video track.|You can blur specified areas of a single video track.|
|Crop an image of a single video track or add black borders.|You can crop an image of a single video track or add black borders.|
|Extract audio from a single video track and mute or adjust the volume of the video track.|You can extract audio from a single video track and mute or adjust the volume of the video track. You can mute the entire video track or a specified part of the video track.|
|Cut a single audio track into clips and merge multiple clips.|You can cut a single audio track into clips and merge multiple clips.|
|Mute or adjust the volume of a single audio track.|You can mute the entire audio track or a specified part of the audio track or adjust the volume of the audio track.|
|Overlay an independent subtitle file on a single video track.|You can overlay an independent subtitle file on a single video track. Subtitle files in the .ass and .srt formats are supported.|

Advanced editing

|Feature|Description|
|-------|-----------|
|Mix multiple audio or video tracks.|You can mix multiple audio tracks, multiple video tracks, or multiple audio and video tracks. This feature applies to dubbing and picture-in-picture \(PiP\) scenarios.|
|Add effects.|The following effects are supported: fade, translation, and zoom in or out.|
|Convert images into a video.|After multiple images are uploaded, you can convert the images into a video.|

## Material area

The material area provides you with a variety of editing features, including **Materials**, **Subtitles**, **Stickers**, and **Transitions**.

Feature description and basic operations

-   **Materials**

    The materials in the Materials module are available from the media asset library of the ApsaraVideo VOD console. The materials in the media asset library are not affected when you add materials to the Materials module or remove materials from the Materials module. However, if you delete materials from the media asset library, the materials are also deleted from the Materials module. For more information about how to manage media assets in the media asset library, see [Manage media assets](/intl.en-US/User Guide/Media library/Manage media assets.md).

    **Add materials**

    In the **Materials** section, click **Videos**, **Audio**, or **Images**, and then click **Add from Media Asset Library** in the upper-right corner of the Materials section. In the Add Media File panel, select the material that you want to add, and then click **OK**. If you have many materials, you can select **By Name** or **By Editing Time** to search for the material that you want to add. If the existing materials do not meet your requirements, you can click **Upload Media Files** and add materials. For more information, see [Upload media assets](/intl.en-US/User Guide/Media library/Upload media assets.md).

    After the material is added to the Materials section, move the pointer over the material and click the **plus** icon. Then, the material is added to the track editing area.

-   **Subtitles**

    When you use the online editing service, you can add only text subtitles.

    **Add subtitles**

    Mover the pointer over the sample subtitle and click the **plus** icon. Then, the subtitle is added to the track editing area.

-   **Stickers**

    When you use the online editing service, you can add the following styles of stickers: **Bubbles**, **Life**, **Emojis**, **Atmosphere**, and **Cute**.

    **Add stickers**

    Mover the pointer over the sticker that you want to add and click the **plus** icon. Then, the sticker is added to the track editing area.

-   **Transitions**

    When you use the online editing service, you can add the following types of transitions: **Zoom In II**, **Grid**, **Left-to-Right Wipe I**, **Clockwise Scan I**, and **Fade**.

    **Add transitions**

    Drag the required transition between two video clips of the same video track.


## Video preview area

In the video preview area, you can play, fast forward, and rewind the video.

You can preview the video, stickers, and subtitles and adjust the positions or sizes of materials in real time.

## Track editing area

In the track editing area, you can use the following editing features: **undo**, **redo**, **cut**, **delete**, **display**, and **volume setting**.

The following table describes the shortcut keys that you can use to speed up the editing.

|Shortcut key|Feature|
|------------|-------|
|Space|Pause or preview a video.|
|Ctrl+C|Copy a clip.|
|Ctrl+V|Paste a clip.|
|← or →|Rewind or forward a video. If you hold the → key, the video is fast forwarded.|
|Ctrl++ or Ctrl+-|Zoom in or out the timeline of a video.|
|Home|Seek to the beginning of a video.|
|End|Seek to the end of a video.|
|Ctrl+S|Save the editing.|
|Ctrl+Z|Undo an operation.|
|Ctrl+Shift+Z|Redo an operation.|
|-   macOS: Delete
-   Windows: Backspace

|Delete a material.|

**Usage notes on the track editing area**

-   The track editing area provides the following tracks from top to bottom: tracks for adding subtitles, stickers, filters, and effects, tracks for adding videos and images, and tracks for adding audio.
-   At least one video track must be retained in the track editing area.
-   A track that contains materials cannot be deleted.
-   If a material is added to the track editing area, you cannot remove the material from the Materials module.
-   When you add a material, the material is added next to the pointer in the corresponding track.
-   You can double-click a material in the corresponding track to edit the material.
-   When you click the cut icon, only the material in the track that you click is cut.
-   The cut feature cuts the material in the corresponding track at the position where the pointer resides.
-   If a track contains Material A and Material B and you drag Material A to cover part or all of Material B, the covered part or all of Material B disappears and is replaced with Material A.

**Edit the material in a track**

-   **Subtitle track**

    Click the subtitle in a subtitle track. In the material editing section, modify the value of the **Content**, **Font**, **Font Color**, or **Style** parameter as required. You can adjust the position of the subtitle in the video and view the results in the video preview area.

    When you click the cut icon, the subtitle is cut into two subtitles with the same settings. The length of the original subtitle is divided at the position where the pointer resides.

-   **Sticker track**

    Click the sticker in a sticker track. In the material editing section, adjust the position of the sticker in the video and view the results in the video preview area.

    When you click the cut icon, the sticker is cut into two stickers with the same settings. The length of the original sticker is divided at the position where the pointer resides.

-   **Video track**

    Click the video in a video track. In the material editing section, add an effect to the video and view the results in the video preview area.

    When you use the online editing service, you can add the following effects: **Mosaic**, **TV Snow**, **TV Flicker**, and **2x Split Screen**.

    When you click the cut icon, the video is cut into two clips at the position where the pointer resides.

-   **Audio track**

    Click the audio in an audio track. In the material editing section, adjust the volume of the audio.

    When you click the cut icon, the audio is cut into two clips at the position where the pointer resides.

-   **Image track**

    Click the image in an image track. In the material editing section, adjust the position of the image in the video and view the results in the video preview area.

    When you click the cut icon, the image is cut into two images with the same settings. The length of the original image is divided at the position where the pointer resides.


## Procedure

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, find **Production Center**.

3.  Click **Video Editing**. The Video Editor page appears.

4.  Click **Edit New Video**.

5.  Click **Materials** and add the material that you want to edit.

    Add subtitles, stickers, and effects as required.

6.  Edit the added materials in the track editing area.

7.  After the editing process is complete, click **Generate** in the upper-right corner of the page. A video is generated based on your settings.

    **Note:**

    -   Video Resolution: the resolution of the generated video. If you set this parameter to Same as Video Source, the resolution of the generated video is the same as that of the source video.
    -   Transcoding Template: the transcoding template that is used when you upload the generated video to the media asset library of the ApsaraVideo VOD console. For more information about how to transcode a video, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).

