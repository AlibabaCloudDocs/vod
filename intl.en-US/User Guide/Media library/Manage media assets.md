# Manage media assets

The ApsaraVideo VOD console allows you to upload multiple media assets such as audio, videos, images, and short video materials at a time. This topic uses videos as an example to describe how to manage media assets.

## Manage videos

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane of the ApsaraVideo VOD console, choose **Media Files** \> **Audio/Video**.

    You can filter videos by the type, category, status, and source. You can also enter the ID or name of a video to search for the video.

    The value in the Status column indicates the processing status of the video, including Uploading, Uploaded, Transcoding, Transcoding Failed, Normal, Reviewing, Flagged, and All.

    **Note:** If your video is in the Transcoding Failed state, delete the video and upload it again. If the transcoding fails for multiple times, submit a [ticket](https://selfservice.console.aliyun.com/ticket/createIndex).

    ![Video and Audio page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2344319061/p184462.png)


Description about supported actions

-   Action: **Manage**

    On the **Video and Audio** page, click **Manage** in the Actions column to manage the video.

    -   **Basic information** tab

        On the Basic Information tab, view or modify the name, description, category, tag, and thumbnail of the video. After you modify the configuration, click **Save**.

        ![Basic Information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2344319061/p184487.png)

        The following table describes the parameters.

        |Parameter|Description|
        |---------|-----------|
        |**Cover**|Upload an image or select a video snapshot as the default video thumbnail.**Note:** You can customize the thumbnail by uploading an image. The image must be in the JPG or PNG format and can be up to 1 MB in size. The maximum resolution of the image is 1920 × 1080 pixels. |
        |**Name**|The name that is displayed in the player window during playback. It can contain up to 30 characters.|
        |**Description**|The detailed description about the video. It can contain up to 120 characters.|
        |**Category**|Configure video categories on the Categories page. For more information, see [Manage video categories](/intl.en-US/User Guide/Global settings/Manage video categories.md).|
        |**Tag**|Add one or more tags for a video. The name of a tag can contain up to 15 characters.|

    -   **Video URL** tab

        You can view the URLs, resolutions, and bitrates of the video mezzanine file and the transcoded videos in all formats and definitions.

        ![Address](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2344319061/p184490.png)

        The following table describes the supported actions.

        |Action|Description|
        |------|-----------|
        |**Copy**|Copy the URL of the video in the current definition to a browser or player and preview the video.|
        |**Preview**|Preview the video in the current definition in the console.|
        |**Delete**|Delete the video.|
        |**Delete All**|Delete all transcoded files but not the mezzanine file. The files that are deleted cannot be restored. Therefore, perform this action with caution.|

    -   **Web Player Code** tab

        If you are a developer, you can use HTML code or JavaScript code for each video as needed. In addition, you can set the Player Size parameter and turn on or off Auto Play in Player Settings to modify the corresponding parameters in the code snippet. This way, you can improve work efficiency.

        **Note:** Use the latest version of ApsaraVideo Player for web when you use ApsaraVideo VOD. For more information, see [ApsaraVideo Player for web](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Overview.md).

        ![ApsaraVideo Player for web](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3344319061/p184493.png)

-   Action: **Delete**

    On the **Video and Audio** page, click **Delete** in the Actions column to delete the video. After the video is deleted, all resources that are related to the video are permanently deleted and cannot be restored, including the mezzanine file, transcoded files, and snapshots. Therefore, perform this action with caution.

-   Action: **More**

    On the **Video and Audio** page, click **More** in the Actions column and perform more actions that are supported for video management.

    ![More](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3344319061/p184528.png)

    The following table describes the supported actions.

    |Action|Description|
    |------|-----------|
    |**Media Processing**|You can use transcoding templates or workflows to process videos.|
    |**Disable Download**|This action forbids users to download videos. This action must be performed in conjunction with a player.**Note:** You can forbid users to download videos only when the videos are in the Normal state. For more information about the secure download settings, see [Configure offline download](/intl.en-US/User Guide/Domain management/Configure offline download.md). |
    |**Make Available on Cloud Studio**|Click **Make Available on Cloud Studio** to transcode the video into two streams, which can be added for playback in the production studio of ApsaraVideo VOD. For more information about the production studio features, see [Introduction to production studios]().**Note:** You can click **Make Available on Cloud Studio** only once for each video. |

-   Action: **Export Media URL**

    On the **Video and Audio** page, click the **Export Media URL** icon in the upper-right corner to export the information of the videos in the list to a Comma Separated Value \(CSV\) file. The exported information includes the ID, name, length, size, creation time, update time, and bucket of the videos.

    ![Export](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3344319061/p184531.png)

-   Action: Preview media files

    Open a video that is in the Normal state in the video and audio list.

    ApsaraVideo VOD provides a player for you to preview videos. The player allows you to set fast-forwarding, volumes, subtitles, audio tracks, definitions, and bullet messages for videos. This enables you to preview videos in a convenient way.

    ![Preview videos](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3344319061/p184532.png)


