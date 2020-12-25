# Manage snapshot templates

ApsaraVideo VOD allows you to capture snapshots based on a snapshot template. This topic describes how to configure a snapshot template.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **Media Processing** \> **Snapshot Templates**.

4.  On the Snapshot Templates page, click **Add Template**.

    ![Click Add Template](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3380888061/p182736.png)

5.  On the Add Template page, configure the snapshot template.

    ![Configure the snapshot template](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3380888061/p182746.png)

    Snapshot types include **Normal Snapshot**, **WebVTT**, and **Image Sprite**. For more information, see [Video snapshots](/intl.en-US/Developer Guide/Media processing/Video snapshot.md).

    The following table describes the parameters.

    |Parameter|Screenshot type|Description|
    |---------|---------------|-----------|
    |Start Time|Normal Snapshot, WebVTT, and Image Sprite|The time when the first snapshot is created. The time is in the HH:MM:SS format.|
    |Snapshot Count|Normal Snapshot, WebVTT, and Image Sprite|The total number of snapshots.|
    |Snapshot Interval|Normal Snapshot, WebVTT, and Image Sprite|The interval at which multiple snapshots are created. If you set this parameter to 0 or leave it empty, snapshots are evenly created throughout the video duration.|
    |Size \(Width × Height\)|Normal Snapshot, WebVTT, and Image Sprite|The width and height of the snapshot. Unit: pixels.**Note:**

    -   If you leave these parameters empty, the width and height of the snapshot are the same as those of the input video.
    -   If you set only the width or height, the snapshot is proportionally scaled based on one side of the input video. |
    |Frame Type|Normal Snapshot, WebVTT, and Image Sprite|Valid values: Frame and Keyframe.**Note:** If you select Keyframe, only keyframes are captured. If no keyframe is found at the specified time, the keyframe closest to the specified time is selected. Keyframes are captured faster than normal frames if the same snapshot rules are applied. |
    |Generate Image Sprite|WebVTT|If you disable this feature, snapshots are separately stored. If you enable this feature, snapshots are put into a single image.|
    |Arrangement \(Rows x Columns\)|Image Sprite|The width and height of snapshots in the image sprite.**Note:**

    -   If you leave these parameters empty, the width and height of snapshots are the same as those of normal images.
    -   If you set only the width or height, the snapshots are proportionally scaled based on one side. |
    |Row Space|Image Sprite|The spacing between the rows in the image sprite. Unit: pixels.|
    |Column Space|Image Sprite|The spacing between the columns in the image sprite. Unit: pixels.|
    |Background Color|Image Sprite|The background color of the image sprite.|
    |Retain Snapshots|Image Sprite|If you enable this feature, the original snapshots are retained. If you disable this feature, the original snapshots are not retained.|

6.  Click **Save**.

    Snapshot templates can be used when you add workflows or upload and process media files.


