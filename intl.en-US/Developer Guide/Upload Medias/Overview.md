# Overview

ApsaraVideo VOD allows you to upload media files such as audio, video, and image files to OSS buckets allocated by ApsaraVideo VOD. You can also initiate subsequent processing operations such as transcoding, editing, and distribution by using automatic triggering or by calling API operations. This topic describes the upload methods and file formats supported by ApsaraVideo VOD.

For information about the AccessKey pairs and permissions required for media uploads, see [Overview](/intl.en-US/Developer Guide/Access authorization/Overview.md).

ApsaraVideo VOD issues **upload URLs and credentials** to authorize users to upload media files to OSS buckets allocated by ApsaraVideo VOD. For more information, see [Upload URLs and credentials](/intl.en-US/Developer Guide/Upload Medias/Upload URLs and credentials.md).

## Upload methods

The following table describes the methods that you can use to upload media files in ApsaraVideo VOD.

|Method|Description|Scenario|Reference|
|------|-----------|--------|---------|
|Upload in the ApsaraVideo VOD console|After you activate ApsaraVideo VOD, you can log on to the ApsaraVideo VOD console to upload audio, video, and image files. Batch upload is supported.|Scenarios in which you want to upload media resources to ApsaraVideo VOD in a fast and convenient manner.|[Upload media assets](/intl.en-US/User Guide/Media library/Upload media assets.md)|
|Upload from servers|You can upload media files stored on application servers to ApsaraVideo VOD. Server upload SDKs are required.|Scenarios in which you require automated upload or you want to upload a large amount of video files.|[Upload from servers](/intl.en-US/Developer Guide/Upload Medias/Upload from servers.md)|
|Upload from clients|Users of mobile terminals, web pages, or PCs upload media files from the client to ApsaraVideo VOD. Client upload SDKs are required. The following SDKs are supported:-   Upload SDK for Android
-   Upload SDK for iOS
-   Web upload SDK

|Scenarios in which user generated content \(UGC\) and professionally generated content \(PGC\) are uploaded.|[Upload from clients](/intl.en-US/Developer Guide/Upload Medias/Upload from clients.md)|
|Upload offline|You can upload media files stored not in servers or clients to ApsaraVideo VOD. You can call the UploadMediaByURL operation and specify the URLs of the media files to be uploaded. Then, ApsaraVideo VOD automatically pulls the media files from the source storage in the background to upload them.|Scenarios where media files are not stored on servers or clients.|[UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md)|
|Upload by using client tools|You can use client tools to upload media files from your computers. You must download and install the client tools before you can use them. Currently, only the Windows and MacOS operating systems are supported. **Note:** When you upload large files in the ApsaraVideo VOD console, it typically takes an extended period of time to complete the upload. Your logon session may expire due to security settings before the upload is complete. You can use client tools to avoid this issue.

|Scenarios where you want to upload large files for an extended period of time or where operations are not sophisticated.|Download links:-   [ApsaraVideo VOD client tool \(Windows\)](https://alivc-demo-cms.alicdn.com/versionProduct/installPackage/upload/ApsaraVideo_vodClient_v1.0.0_Windows_20201023.zip)
-   [ApsaraVideo VOD client tool \(MacOS\)](https://player.alicdn.com/download/aliyun_video_client_1.3.2_1024.dmg?spm=a2c4g.11186623.2.22.515927b0580YmN&file=aliyun_video_client_1.3.2_1024.dmg) |

**Note:**

-   By default, multipart upload can be used to upload single files of up to 48.8 TB in size by using the console, upload SDKs, or upload tools. Simple upload is also supported to upload single files of up to 5 GB in size by using upload SDKs.
-   Resumable upload is supported.
-   In multipart upload, fragments may be generated if the upload fails. The fragments are automatically deleted seven days later.

## Supported file formats

|File type|Supported format|
|---------|----------------|
|Video|-   MPEG formats: MP4, TS, 3GP, MPG, MPEG, MPE, DAT, VOB, and ASF.
-   AVI format: AVI.
-   Windows Media Video formats: WMV and ASF.
-   Flash Video formats: FLV and F4V.
-   Real Video formats: RM and RMVB.
-   QuickTime format: MOV.
-   Matroska format: MKV.
-   HLS format: M3U8.
-   Other formats: DV, GIF, M2T, M4V, MJ2, MJPEG, MTS, OGG, QT, SWF, and WEBM. |
|Audio|MP3, WMA, WAV, AAC, RA, M4A, FLAC, APE, AC3, AMR, CAF, and ACM.|
|Image|PNG, JPG, JPEG, and GIF.|
|attached media resource|-   Watermark files: PNG, GIF, APNG, and MOV.
-   Subtitle files: SRT, ASS, STL, TTML, and VTT
-   Material files: JPG, GIF, PNG, MP4, MAT, and ZIP. |

**Note:** File name extensions are case-insensitive. For example, MP4 and mp4 refer to the same format.

## Upload instructions

-   **Storage**
    -   ApsaraVideo VOD allows you to store VOD resources by using Object Storage Service \(OSS\) buckets. You do not need to activate OSS. When you activate ApsaraVideo VOD, a system bucket in the China \(Shanghai\) region is allocated by default. You can also specify another region to store VOD resources. For more information, see [Manage VOD resources](/intl.en-US/User Guide/Global settings/Manage VOD resources.md).
    -   You can upload media files to the default bucket or specify a bucket when you upload each media file. To prevent uploaded media files from overwriting each other, ApsaraVideo VOD automatically specifies the storage paths of uploaded media files. After media files are uploaded, you can view and manage them. For example, you can obtain, update, search, download, and delete data. For more information, see [Manage media assets](/intl.en-US/User Guide/Media library/Manage media assets.md).
    -   The storage service supports the following billing methods: pay-as-you-go and resource plans. For more information, see the "Media management" section in [ApsaraVideo VOD pricing](https://www.aliyun.com/price/detail/vod#module3) and [ApsaraVideo VOD storage plan](https://common-buy.aliyun.com/?spm=5176.8296044.671734.pricedetail2222.5c22435bMzdW0P&commodityCode=vodstoragebag#/buy).
-   **Additional settings**

    You can also make the following settings when you upload media files:

    -   Metadata: You can configure metadata such as the titles, categories, and tags of audio, video, and image files to facilitate subsequent management and queries.
    -   Bucket: You can specify the `StorageLocation` parameter in upload SDKs and API operations to specify the bucket to store uploaded media files. By default, the default bucket is used.
    -   Event notification method and URL: You can specify the `MessageCallback` parameter in the upload SDKs or API operations to specify the event notification method and URL. For more information, see the "UserData" section in [Request parameters](/intl.en-US/API Reference/Appendix/Request parameters.md). By default, global callback settings are used.
    -   Video processing method: After a video is uploaded, ApsaraVideo VOD takes thumbnail snapshots of the video and processes the video by using a specified processing method.
        -   You can specify a transcoding template group by setting the `TemplateGroupId` parameter to enable video transcoding. You can also specify not to transcode the video \(the `no transcoding` template is used\). If you do not specify a transcoding template group, the global transcoding settings are used by default.
        -   You can also specify the WorkFlowId parameter to process the video by using the specified workflow. After a video is uploaded, the specified workflow is executed.
    **Note:** For more information about parameters for the preceding additional settings, see the "Media upload" section in [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).

-   **Acceleration**

    ApsaraVideo VOD provides the upload acceleration feature to improve performance in file transfers over a long distance \(such as across oceans\) and uploads of files of gigabytes or terabytes in size.

    -   Activation: [Submit a ticket](https://selfservice.console.aliyun.com/ticket/category/vod/recommend/561). You must provide the **UID of your Alibaba Cloud account** and the **bucket** to which you want to apply the upload acceleration feature.
    -   Use method: Specify the `AccelerateConfig` parameter \(a JSON string\) in the upload SDKs or API operations. For more information, see the "UserData" section in [Request parameters](/intl.en-US/API Reference/Appendix/Request parameters.md).
    -   Notes: Upload acceleration takes effect only for a single upload. If you want to use this feature for an upload, you must specify upload acceleration parameters before the upload. If you do not specify upload acceleration parameters, upload acceleration is not used.
    -   Upload acceleration is billed based on usage. No fees are charged if you only activate upload acceleration but do not use it. For more information about prices, see [VOD Pricing](https://www.aliyun.com/price/product?#/vod/detail).
    Examples of upload acceleration parameters:

    -   Examples: `{"Type":"oss","Domain":"https://oss-accelerate.aliyuncs.com"}`
        -   Type: the acceleration mode. Set it to oss.
        -   Domain: the accelerated domain name, which corresponds to the [accelerate endpoints](/intl.en-US/Developer Guide/Endpoint/Regions and endpoints.md) in OSS. The default value is https.
    -   The following example shows how to set the preceding upload acceleration parameters:

        ```
            public static String buildUserdata() {
        
                JSONObject userData = new JSONObject();
                // Configure the upload acceleration parameters if you want to use upload acceleration.
                JSONObject accelerateConfig = new JSONObject();
                accelerateConfig.put("Type", "oss");
                accelerateConfig.put("Domain", "https://oss-accelerate.aliyuncs.com");
                userData.put("AccelerateConfig", accelerateConfig);
                
                return userData.toJSONString();
            }
        ```

-   **Transcoding**

    When you upload a video, you can specify a transcoding template or disable transcoding by using the No Transcoding template. For example, you can use the No Transcoding template to upload short videos because short videos are already encoded and compressed when they are captured. For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).

    -   Quick transcoding: default. ApsaraVideo VOD automatically triggers transcoding for uploaded videos.
    -   No transcoding: If the No Transcoding template is used to upload videos, the videos can be played immediately after they are uploaded. If a [domain name for CDN](/intl.en-US/User Guide/Domain management/Add a domain name.md) is configured, uploaded videos are distributed in accelerated mode by default to ensure smooth playback.

## Event notifications

After media files are uploaded, you can receive real-time event notifications, provided that you have configured callback methods and callback URLs in the ApsaraVideo VOD console. For more information, see [Overview](/intl.en-US/Developer Guide/Event notification/Overview.md). Event notifications for upload completion include:

-   [FileUploadComplete](/intl.en-US/Developer Guide/Event notification/Events/FileUploadComplete.md) \(including audio\)
-   [ImageUploadComplete](/intl.en-US/Developer Guide/Event notification/Events/ImageUploadComplete.md)

## Notes for post-upload processing

-   **Post-upload processing**

    ApsaraVideo VOD supports audio and video transcoding, automated review, online editing, and AI processing for uploaded media files.

    Unlike OSS, ApsaraVideo VOD automatically extracts the metadata of uploaded audio and video files, such as the video resolution, duration, and bitrate. ApsaraVideo VOD also takes thumbnail snapshots of videos. The metadata extraction and thumbnail snapshot taking are free of charge.

-   **Media management**

    You can manage uploaded media files such as source video files, transcoded stream files, and image files in ApsaraVideo VOD. You can manage media resources by using one of the following methods:

    -   Manage media resources in the ApsaraVideo VOD console. For more information, see [Media management](/intl.en-US/User Guide/Media library/Manage media assets.md).
    -   Call media management API operations. For more information, see the "Media management" section in [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).
    **Note:** For more information about media management, see [Overview](/intl.en-US/Developer Guide/Media asset management/Overview.md) \(this topic describes how to query, search for, and update information about media resources\), [Download media files](/intl.en-US/Developer Guide/Media asset management/Download media files.md), and [Delete media files](/intl.en-US/Developer Guide/Media asset management/Delete media files.md).

-   **Playback**

    When a video is uploaded, it is not immediately ready for playback. ApsaraVideo VOD needs to confirm that the video has been received. You can determine whether the video is ready for playback based on `event notifications`.

    -   For a video \(or audio\) that does not need to be transcoded, you can play it after you receive the [FileUploadComplete](/intl.en-US/Developer Guide/Event notification/Events/FileUploadComplete.md) event notification. You can call the [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md) operation to obtain the playback URL.
    -   For a transcoded video, you can play it after you receive the [StreamTranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/StreamTranscodeComplete.md) event notification. To ensure that streams in all definitions can be obtained, we recommend that you play the video after you receive the [TranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/TranscodeComplete.md) event notification.
    You can also use the No Transcoding template to upload videos so that they are not transcoded. After you receive the [FileUploadComplete](/intl.en-US/Developer Guide/Event notification/Events/FileUploadComplete.md) event notification, you can call the [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md), or [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Process initiation/SubmitSnapshotJob.md) operation to process the uploaded videos.


