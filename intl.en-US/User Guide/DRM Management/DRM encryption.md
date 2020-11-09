# DRM encryption

This topic describes how to enable digital rights management \(DRM\) encryption in the ApsaraVideo VOD console. This topic also describes how to configure ApsaraVideo Player to play DRM-encrypted videos.

## Limits

You can enable DRM encryption only by using the ApsaraVideo VOD console rather than the API.

## Upload a certificate

**Note:** If you develop applications that run on iOS, you must upload a FairPlay Streaming certificate to the ApsaraVideo VOD console.

1.  Apply for a FairPlay Streaming certificate.

    To use FairPlay DRM encryption, you must apply for a FairPlay Streaming certificate from Apple. For more information, see [Apply for a FairPlay Streaming certificate](/intl.en-US/User Guide/DRM Management/Apply for a FairPlay Streaming certificate.md).

2.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

3.  In the left-side navigation pane, choose **Configuration Management \> Media Processing \> DRM Certificates**.

4.  On the DRM Certificates page, click **Upload Certificate**.

    ![Upload](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1185194061/p177092.png)


## Enable DRM encryption in the ApsaraVideo VOD console

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Configuration Management \> Media Processing \> Transcode**.

3.  On the Transcode page, click **Create Template**.

    ![Click Create Template](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1185194061/p177096.png)

4.  On the **Added Transcoding Template Group** page, click **Add Template** in the Normal Transcoding Template section.

5.  In the **Basic Parameters** section, select **hls** from the Encapsulation Format drop-down list.

6.  Click the unfold icon on the left of **Advanced Parameters**. Turn on Video Encryption. Then, select **DRM Encryption** for Encryption Method.

    ![Enable DRM encryption](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1185194061/p177122.png)

7.  Transcode a video.

    When you upload a video by using the ApsaraVideo VOD console, API, or upload SDK, use the template with DRM encryption enabled to transcode the video. After the video is transcoded, choose **Media Files \> Audio/Video** in the left-side navigation pane. Click **Manage** in the Actions column of the video. On the management page of the video, click **Video URL** to view the information about the video. The **DRM Encryption** label is displayed in the Format column of the resolution to which the video is transcoded by using the DRM encryption-enabled template.

    ![DRM Encryption label](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1185194061/p177131.png)


## Configure ApsaraVideo Player

To play DRM-encrypted videos, you must use ApsaraVideo Player. You do not need to develop your own players to play DRM-encrypted videos. To use ApsaraVideo Player to play DRM-encrypted videos, take note of the following points:

-   The version of ApsaraVideo Player must be 5.2.1 and later. You can use FairPlay DRM encryption for iOS and Widevine DRM encryption for Android.
-   If you use ApsaraVideo Player for Android, we recommend that you use SurfaceView to play videos with high security levels.
-   If you use ApsaraVideo Player for iOS, you must call the setFairPlayCertID method of AliPlayerGlobalSettings to specify the ID of your FairPlay Streaming certificate. This method needs to be called only once. To obtain the ID of your FairPlay Streaming certificate, log on to the ApsaraVideo VOD console. Choose **Configuration Management \> Media Processing \> DRM Certificates**. Then, find your certificate ID on the DRM Certificates page.

**Note:** You can play DRM-encrypted videos only on mobile clients. Web clients will be supported soon. When you play a DRM-encrypted video with a high security level, you cannot rotate the video, mirror the video, or take snapshots from the video.

