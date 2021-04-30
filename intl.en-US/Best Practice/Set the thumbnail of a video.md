# Set the thumbnail of a video

To beautify the display of videos, ApsaraVideo VOD sets a thumbnail for each uploaded video and provides multiple ways for you to change the thumbnail. After a video is uploaded, ApsaraVideo VOD takes snapshots. If you specify a snapshot as the thumbnail during the upload, the specified snapshot is set as the thumbnail by default. Otherwise, one of the snapshots is used as the default thumbnail. You can change the thumbnail after the video is uploaded.

## Preparations

-   [Register](https://account.aliyun.com/register/register.htm?oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh) an Alibaba Cloud account, complete [real-name verification](https://help.aliyun.com/knowledge_list/37170.html), and then activate [ApsaraVideo VOD](https://www.aliyun.com/product/vod).
-   Obtain an AccessKey pair to access ApsaraVideo VOD. You can create an AccessKey pair for your Alibaba Cloud account on the [Security Management](https://ak-console.aliyun.com/?spm=5176.doc57741.2.8.uLYY2M#/accesskey) page in the Alibaba Cloud Management Console. You can also create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=5176.doc57741.2.2.fQnI2T#/user/list) and grant the RAM user the permissions to access ApsaraVideo VOD. For more information, see [Grant permissions to a RAM user](https://help.aliyun.com/document_detail/116146.html).
-   If you want to use the intelligent thumbnail feature, you must apply to [enable](https://ai.aliyun.com/vi/cover) the feature.

## Set the thumbnail in the console

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane of the ApsaraVideo VOD console, choose **Media Files** \> **Audio/Video**. Then, click Upload.

    ![Upload audio and video files](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0316319061/p184170.png)

3.  Find the video for which you want to change the thumbnail and click **Manage** in the Actions column.

    **Note:**

    After a video is uploaded, a default video snapshot is used as the video thumbnail.

    ![Select a video](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7335679161/p251306.png)

4.  Click **Editing Video Information** and select one of the snapshots that are automatically taken as the video thumbnail. You can also click **Upload** and select an on-premises image to upload it as the thumbnail.

    ![Upload](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7335679161/p251311.png)

    **Note:** The uploaded image must be in the PNG or JPG format. The maximum size is 1 MB, and the maximum resolution is 1920 × 1080 pixels.


## Set the thumbnail by using the API or SDK

ApsaraVideo VOD provides various [methods to upload videos](/intl.en-US/Developer Guide/Upload Medias/Overview.md). You can specify the thumbnail when you upload a video. If you do not specify a thumbnail, ApsaraVideo VOD selects a snapshot as the default thumbnail. You can call the following operations to set the thumbnail:

-   When you call the [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md) operation, you can set the CoverURL parameter to specify the URL of the thumbnail.
-   When you call the [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md) operation, you can set the CoverURL parameter in UploadMetadata to specify the URL of the thumbnail.
-   If the video is stored in Object Storage Service \(OSS\), you can call the [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md) operation to register the media asset in ApsaraVideo VOD. When you call this operation, you can set the CoverURL parameter in RegisterMetadata to specify the URL of the thumbnail.
-   After the video is uploaded to ApsaraVideo VOD, you can call the [UpdateVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfo.md) or [UpdateVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfos.md) operation and set the CoverURL parameter to specify the URL of the thumbnail.

## Use the intelligent thumbnail feature

The intelligent thumbnail feature can analyze video content and extract multiple snapshots that best represent the video content as backup thumbnails. This feature can also extract keyframes from the video content and automatically merge them into a GIF file as the video thumbnail. To experience the intelligent thumbnail feature, click [here](https://retina.aliyun.com). Before you use the [intelligent thumbnail](https://ai.aliyun.com/vi/cover) feature, submit an application to enable the feature. The following figure shows the effect of the intelligent thumbnail feature.![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8335679161/p178456.png)

