# Manage frame animation templates

ApsaraVideo VOD allows you to capture a part of a video by using a frame animation template and generate a GIF file. This topic describes how to add a frame animation template.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **Media Processing** \> **Frame Animation Templates**.

4.  On the Frame Animation Templates page, click **Add Template**.

    ![Click Add Template](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7580888061/p182945.png)

5.  On the Add Template page, configure the frame animation template.

    ![Configure the frame animation template](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8580888061/p182955.png)

    Valid values of Output Format:

    -   gif

        GIF images provide high compatibility and are often used to decorate web pages.

    -   webp

        WebP images have a smaller file size than GIF images but are not compatible with some browsers.

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |Frame Rate|The frame rate of the frame animation. Valid values: 1 to 60. The value must be an integer.|
    |Size \(Width × Height\)|The width and height of the frame animation. Unit: pixels.**Note:**

    -   If you leave these parameters empty, the width and height of the frame animation are the same as those of the input video.
    -   If you set only the width or height, the frame animation is proportionally scaled based on one side of the input video. |
    |Trim Mode|Valid values:    -   Trim from Beginning
    -   Trim from Beginning and End |
    |From Beginning|The start time when the frame animation is captured. Valid values: 0.000 to 86399.999. Unit: seconds.|
    |Duration|The duration of the frame animation. Valid values: 0.000 to 86399.999. Unit: seconds.|
    |From End|The duration between the end time of the frame animation and that of the video. Valid values: 0.000 to 86399.999. Unit: seconds.|
    |Use as Default Cover|If you enable this feature, the frame animation is used as the cover of the video.|

6.  Click **Save**.

    Frame animation templates can be used when you add workflows.


