# Set the video thumbnail

To beautify the display of videos, ApsaraVideo VOD allows you to add a thumbnail to each uploaded video and provides multiple ways for you to change the thumbnail. After a video is uploaded, ApsaraVideo VOD takes snapshots. If you specify a snapshot as the thumbnail during the upload, the specified snapshot is set as the thumbnail by default. Otherwise, one of the snapshots is used as the default thumbnail. You can change the thumbnail after the video is uploaded.

## Preparations

-   [Register](https://account.aliyun.com/register/register.htm?oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh) an Alibaba Cloud account, complete [real-name verification](https://help.aliyun.com/knowledge_list/37170.html), and then activate [ApsaraVideo VOD](https://www.aliyun.com/product/vod).
-   Obtain an AccessKey to access ApsaraVideo VOD. You can create an AccessKey for your Alibaba Cloud account on the [Security Management](https://ak-console.aliyun.com/?spm=5176.doc57741.2.8.uLYY2M#/accesskey) page in the Alibaba Cloud Management console. You can also create a RAM user in the [Resource Access Management \(RAM\) console](https://ram.console.aliyun.com/?spm=5176.doc57741.2.2.fQnI2T#/user/list) and grant the RAM user the permission to access ApsaraVideo VOD. For more information, see [Grant permissions to a RAM user]().
-   If you want to use the intelligent thumbnail feature, you must apply to [enable](https://ai.aliyun.com/vi/cover) the feature.

## Set the thumbnail in the console

-   Upload a video in the [console](). After the video is uploaded, a video snapshot is used as the default video thumbnail. To change the thumbnail, log on to the **ApsaraVideo VOD console** and choose **Media Files** \> **Audio/Video**. In the Video and Audio list, click **Manage** for a video to go to the details page of the video. At the top of the page, you can select one of the snapshots that are automatically taken as the video thumbnail. You can also click **Upload** and select an on-premises image as the thumbnail. The PNG, JPG, JPEG, and GIF formats are supported. The maximum size of a thumbnail is 1 MB, and the maximum resolution is 1920 × 1080 pixels. The following figure shows the page on which you can customize the thumbnail.![](../images/p178455.png)

## Set the thumbnail by using the API or SDK

ApsaraVideo VOD provides various [methods to upload videos](). You can specify the thumbnail when you upload a video. If you do not specify a thumbnail, ApsaraVideo VOD selects a snapshot as the default thumbnail. You can call the following operations to set the thumbnail:

-   When you call the [CreateUploadVideo]() operation, you can set the CoverURL parameter to specify the URL of the thumbnail.
-   When you call the [UploadMediaByURL]() operation, you can set the CoverURL parameter in UploadMetadata to specify the URL of the thumbnail.
-   If the video is stored in Object Storage Service \(OSS\), you can call the [RegisterMedia]() operation to register the media asset in ApsaraVideo VOD. When you call this operation, you can set the CoverURL parameter in RegisterMetadata to specify the URL of the thumbnail.
-   After the video is uploaded to ApsaraVideo VOD, you can call the [UpdateVideoInfo]() or [UpdateVideoInfos]() operation and set the CoverURL parameter to specify the URL of the thumbnail.

## Use the intelligent thumbnail feature

The intelligent thumbnail feature can analyze video content and extract multiple snapshots that best represent the video content as backup thumbnails. This feature can also extract keyframes from the video content and automatically merge them into a GIF file as the video thumbnail. To experience the intelligent thumbnail feature, click [here](https://retina.aliyun.com). Before you use the [intelligent thumbnail](https://ai.aliyun.com/vi/cover) feature, submit an application to enable the feature. The following figure shows the effect of the intelligent thumbnail feature.![](../images/p178456.png)

