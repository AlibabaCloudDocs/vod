# Upload media assets

The ApsaraVideo VOD console allows you to upload multiple media assets such as audio, videos, images, and short video materials at a time.

The following table describes the supported file name extensions of the uploaded files.

|Media asset type|Format|
|----------------|------|
|Video|3GP, ASF, AVI, DAT, DV, FLV, F4V, GIF, M2T, M3U8, M4V, MJ2, MJEPG, MKV, MOV, MP4, MPE, MPG, MPEG, MTS, OGG, QT, RM, RMVB, SWF, TS, VOB, WMV, and WEBM|
|Audio|AAC, AC3, ACM, AMR, APE, CAF, FLAC, M4A, MP3, RA, WAV, and WMA|
|Image|PNG, JPG, JPEG, and GIF|
|Short video material|MAT and ZIP|

**Note:** You can upload a media file up to 48.8 TB in size. Only media asset files in the formats that are described in the preceding table can be uploaded. Files that meet the format requirements are queued up for upload in the console.

## Upload settings

-   Storage address settings

    Select an address to store the resources that you upload. If multiple storage addresses are available, the default storage address is selected. For more information about how to configure the default storage address, see [Manage VOD resources](/intl.en-US/User Guide/Global settings/Manage VOD resources.md).

-   Transcoding settings
    -   Before you upload videos, you can select a transcoding template group to transcode the videos as needed. You can specify a transcoding template group for one or more videos at a time.
    -   You can configure different definitions in the transcoding template group. You can also customize resolutions, bitrates, and watermarks for the videos of different definitions. For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).
    -   After you upload videos, the default template group that you configure is selected for the videos. If you upload videos for the first time, check and manage the transcoding settings so that the uploaded videos are transcoded based on your settings.
-   Category settings

    Before you upload media files, you can modify the title and category of the media files. You can modify the category of one or more media files at a time. You can also modify the category of media files on the details page of the files after they are uploaded. For more information about how to configure categories, see [Manage video categories](/intl.en-US/User Guide/Global settings/Manage video categories.md).


## Upload audio and video files

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane of the ApsaraVideo VOD console, choose **Media Files** \> **Audio/Video**. Then, click Upload.

    ![Upload audio and video files](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0316319061/p184170.png)

3.  Click **Add Media**.

    ![Add audio and video files](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0316319061/p184173.png)

4.  Add a file to be uploaded, configure the transcoding settings, and then click **Upload**.

    -   Upload files from an on-premises machine

        ![Upload files from an on-premises machine](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1316319061/p184186.png)

    -   Upload files based on the file URLs

        If the specified URL does not contain a file name extension, we recommend that you enter a file name extension to avoid upload failures. For more information, see [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md).

        ![Upload files based on the file URLs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1316319061/p184187.png)

    **Note:**

    -   After you start the upload, you can leave the upload page but you cannot refresh or close the browser.
    -   You can click **Cancel** to pause the upload of a video.
    -   You can re-upload a video when the previous upload of the video is paused or failed.

## Upload images

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane of the ApsaraVideo VOD console, choose **Media Files \> Image**. Then, click Upload Image.

    ![Upload images](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1316319061/p184215.png)

3.  Click **Add Images**.

    ![Add images](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1316319061/p184219.png)

4.  Add an image to be uploaded and click **Upload**.

    ![Image upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1316319061/p184220.png)


## Upload short video materials

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane of the ApsaraVideo VOD console, choose **Media Files \> Short Video Material**. Then, click Upload Material.

    ![Add a material to be uploaded](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1316319061/p184233.png)

3.  Configure the material to be uploaded and click **Upload**.

    ![Upload materials](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1316319061/p184238.png)

    **Note:** The image that you upload for the **Material Icon** parameter must be in the PNG format and cannot exceed 200 × 200 pixels in size.


## Upload files on the PC client

We recommend that you use the PC client to upload large files or upload multiple files at a time. The uploaded files are displayed in the console. The ApsaraVideo VOD console supports media upload, media asset management, and short video and animated sticker editing. More features will be available soon. Log on to the ApsaraVideo VOD console as a RAM user on the client. This helps you isolate permissions and reduce the risk of configuration errors in the console. For more information about RAM users and AccessKey management, see [Create and grant permissions to a RAM user](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).

Download the PC client of an appropriate application version.

|Operating system|Windows|macOS|
|----------------|-------|-----|
|Application version|[V1.0.0](https://alivc-demo-cms.alicdn.com/versionProduct/installPackage/upload/ApsaraVideo_vodClient_v1.0.0_Windows_20201023.zip)|[V1.3.2](https://player.alicdn.com/download/aliyun_video_client_1.3.2_1024.dmg)|

