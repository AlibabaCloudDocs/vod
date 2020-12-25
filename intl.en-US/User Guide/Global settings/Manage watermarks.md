# Manage watermarks

This topic describes how to create and delete a watermark, and how to configure a default watermark. You can set the size and position of a watermark and add the watermark as a copyright notice to your video when you transcode the video.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **Media Processing** \> **Watermarks**.

4.  On the Watermarks page, click **Create Watermark**.

    ![Create Watermark](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5670888061/p178966.png)

5.  Create a watermark.

    Configure the watermark type, location, horizontal shift, and vertical shift based on your needs.

    -   Watermark Type: Picture.
    -   Watermark Type: Text.
    You can check the watermark in the preview screen by adjusting the preview screen size, watermark size, and watermark location.![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5670888061/p172497.png)

    The following table describes the parameters of the watermark.

    |Parameter|Description|
    |---------|-----------|
    |Image|The image that is used to create a watermark.**Note:** Only PNG and GIF images are supported and the image size cannot exceed 20 MB. |
    |Watermark Name|The name of the watermark.**Note:** The watermark name can contain letters, digits, number signs \(`#`\), and hyphens \(`-`\). |
    |Size \(Width × Height\)|The size of the image.    -   Pixel count. Unit: pixels. Valid values: 8 to 4096.
    -   Aspect ratio. Unit: %. Valid values: 0 to 100, excluding 0 and 100. The value is rounded down to two decimal places.
**Note:** If you set only the width or height, the image is proportionally scaled based on one side. |
    |Location|The position of the watermark relative to the output video. Default value: Upper-right. Valid values:    -   Upper-left
    -   Lower-left
    -   Upper-right
    -   Lower-right |
    |Horizontal Shift|The horizontal shift of the watermark on the output video.    -   Pixel count. Unit: pixels. Valid values: 8 to 4096.
    -   Aspect ratio. Unit: %. Valid values: 0 to 100, excluding 0 and 100. The value is rounded down to two decimal places. |
    |Vertical Shift|The vertical shift of the watermark on the output video.    -   Pixel count. Unit: pixels. Valid values: 8 to 4096.
    -   Aspect ratio. Unit: %. Valid values: 0 to 100, excluding 0 and 100. The value is rounded down to two decimal places. |
    |Timeline|The watermark timeline specifies the start time and duration of a watermark on a video. You can configure multiple watermarks to control the dynamic display effect of an image watermark on a video.**Note:** This parameter is unavailable for watermarks of the text type. |
    |Preview Screen Size \(Width × Height\)|Specify this parameter based on your needs to preview the position and effect of the watermark. Unit: pixels.|

    The following table describes the parameters about the watermarks of the text type.

    |Parameter|Description|
    |---------|-----------|
    |Watermarking Content|The text content of the watermark.|
    |Watermark Name|The name of the watermark.**Note:** The watermark name can contain letters, digits, number signs \(`#`\), and hyphens \(`-`\). |
    |Font|The font of the watermark. Valid values:    -   SimSum
    -   WenQuanYi Zen Hei
    -   WenQuanYi Zen Hei Mono
    -   WenQuanYi Zen Hei Sharp
    -   Yuanti SC |
    |Font Size|The size of the font. Unit: pixels.|
    |Transparency|The transparency of the watermark. The lower the value, the more transparent the watermark. Unit: pixels. The value is rounded down to two decimal places. Valid values: 0 to 1, excluding 0.|
    |Font color|The color of the font.|
    |Stroke Width|The width of the font stroke. Unit: pixels. Valid values: 0 to 4096, excluding 0.|
    |Stroke Color|The color of the font stroke.|
    |Vertical Shift|The vertical shift of the watermark on the output video.    -   Pixel count. Unit: pixels. Valid values: 8 to 4096.
    -   Aspect ratio. Unit: %. Valid values: 0 to 100, excluding 0 and 100. The value is rounded down to two decimal places. |
    |Horizontal Shift|The horizontal shift of the watermark on the output video.    -   Pixel count. Unit: pixels. Valid values: 8 to 4096.
    -   Aspect ratio. Unit: %. Valid values: 0 to 100, excluding 0 and 100. The value is rounded down to two decimal places. |
    |Preview Screen Size \(Width × Height\)|Specify this parameter based on your needs to preview the position and effect of the watermark. Unit: pixels.|

6.  Click **Save**.

7.  Configure a default watermark.

    On the Watermarks page, click **Set as Default** in the Actions column.


