List of operations by function 
===================================================



Overview 
-----------------------------

The following tables list the API operations available for use in ApsaraVideo VOD. We recommend that you use [server SDKs](https://help.aliyun.com/document_detail/101789.html) to call the API operations. For more information about the API endpoint, see [VOD centers and endpoints](https://help.aliyun.com/document_detail/98194.html). For more information about the usage limits, see [Limits](https://help.aliyun.com/document_detail/98195.html).

Media upload 
---------------------------------



|                                                Operation                                                 |                                                                    Description                                                                    |
|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md)         | Obtains a URL and a credential for uploading a video and generates the video ID.                                                                  |
| [RefreshUploadVideo](https://help.aliyun.com/document_detail/55408.html)                 | Obtains a new upload credential after the video upload times out.                                                                                 |
| [CreateUploadImage](https://help.aliyun.com/document_detail/55619.html)                  | Obtains a URL and a credential for uploading an image.                                                                                            |
| [CreateUploadAttachedMedia](https://help.aliyun.com/document_detail/98467.html)          | Obtains a URL and a credential for uploading an auxiliary media asset, such as a watermark file or a subtitle file.                               |
| [UploadMediaByURL](https://help.aliyun.com/document_detail/86311.html)                   | Uploads multiple media files based on the URLs of mezzanine files to ApsaraVideo VOD at a time.                                                   |
| [GetURLUploadInfos](/intl.en-US/API Reference/Media upload/GetURLUploadInfos.md)         | Queries the information about URL-based upload jobs.                                                                                              |
| [DeleteMultipartUpload](/intl.en-US/API Reference/Media upload/DeleteMultipartUpload.md) | Immediately deletes the fragments generated during upload.                                                                                        |
| [GetUploadDetails]()                                                                     | Queries the upload details, such as the upload time, upload ratio, and upload source, about one or more media assets based on the media asset ID. |



Audio and video playback 
---------------------------------------------



|                                            Operation                                             |                                            Description                                            |
|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| [GetPlayInfo](/intl.en-US/API Reference/Video playback/GetPlayInfo.md)           | Queries the streaming URL of a media file, such as an audio or video file, based on the video ID. |
| [GetVideoPlayAuth](/intl.en-US/API Reference/Video playback/GetVideoPlayAuth.md) | Queries the playback credential that is required for playing a video.                             |



Media asset management 
-------------------------------------------

**Media asset search** 


|                                     Operation                                     |                                                    Description                                                     |
|-----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| [SearchMedia](https://help.aliyun.com/document_detail/86044.html) | Searches for the information about media assets such as audio and video files, images, and auxiliary media assets. |



**Media asset categories** 


|                                      Operation                                       |                                                                                       Description                                                                                       |
|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [AddCategory](https://help.aliyun.com/document_detail/56401.html)    | Creates a video category. A maximum of three category levels can be created. Each category can contain up to 100 subcategories.                                                         |
| [UpdateCategory](https://help.aliyun.com/document_detail/56403.html) | Modifies a video category.                                                                                                                                                              |
| [DeleteCategory](https://help.aliyun.com/document_detail/56404.html) | Deletes a video category. If a video category is deleted, its subcategories, including level 2 and level 3 categories, are also deleted. Exercise caution when you call this operation. |
| [GetCategories](https://help.aliyun.com/document_detail/56406.html)  | Queries the information about the specified category and its subcategories.                                                                                                             |



**Audio and video file management** 


|                                                         Operation                                                         |                                                                                                         Description                                                                                                         |
|---------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [GetVideoInfo](https://help.aliyun.com/document_detail/52835.html)                                        | Queries the basic information about a video based on the video ID. The basic information includes the title, description, duration, thumbnail URL, status, creation time, size, snapshots, category, and tags of the video. |
| [UpdateVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfo.md)   | Modifies the information about a video.                                                                                                                                                                                     |
| [UpdateVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfos.md) | Modifies the information about multiple videos at a time.                                                                                                                                                                   |
| [DeleteMezzanines](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteMezzanines.md) | Deletes one or more mezzanine files.                                                                                                                                                                                        |
| [DeleteStream](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteStream.md)         | Deletes one or more media streams, such as audio and video streams, and their storage files.                                                                                                                                |
| [DeleteVideo](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteVideo.md)           | Deletes one or more videos, including their mezzanine files, transcoded stream files, and thumbnail snapshots.                                                                                                              |
| [GetMezzanineInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetMezzanineInfo.md) | Queries the information about an audio or video mezzanine file, including the file URL, resolution, and bitrate.                                                                                                            |
| [GetVideoList](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoList.md)         | Queries the information about videos based on query conditions.                                                                                                                                                             |
| [GetVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfos.md)       | Queries the information about multiple videos at a time.                                                                                                                                                                    |



**Image management** 


|                                       Operation                                        |                        Description                         |
|----------------------------------------------------------------------------------------|------------------------------------------------------------|
| [DeleteImage](https://help.aliyun.com/document_detail/89744.html)      | Deletes uploaded images and automatic snapshots of videos. |
| [GetImageInfo](https://help.aliyun.com/document_detail/89742.html)     | Queries the basic information about an image.              |
| [UpdateImageInfos](https://help.aliyun.com/document_detail/91004.html) | Modifies the information about multiple images at a time.  |
| [ListSnapshots](https://help.aliyun.com/document_detail/72212.html)    | Queries the snapshot data of a specified media file.       |



**Auxiliary media asset management** 


|                                            Operation                                            |                                                                                 Description                                                                                  |
|-------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [GetAttachedMediaInfo](https://help.aliyun.com/document_detail/111508.html)     | Queries the basic information about one or more auxiliary media assets. The basic information includes the title, type, tags, and creation time of an auxiliary media asset. |
| [UpdateAttachedMediaInfos](https://help.aliyun.com/document_detail/111531.html) | Modifies the information about multiple auxiliary media assets at a time.                                                                                                    |
| [DeleteAttachedMedia](https://help.aliyun.com/document_detail/111522.html)      | Deletes one or more auxiliary media assets.                                                                                                                                  |



**Animated sticker management** 


|                                        Operation                                        |                                   Description                                   |
|-----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| [ListDynamicImage](https://help.aliyun.com/document_detail/180958.html) | Queries the information about animated stickers that are captured from a video. |



Media processing 
-------------------------------------

**Processing initiation** 


|                                          Operation                                           |                                                               Description                                                                |
|----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| [SubmitTranscodeJobs](https://help.aliyun.com/document_detail/68570.html)    | Submits a transcoding job and starts asynchronous transcoding.                                                                           |
| [SubmitSnapshotJob](https://help.aliyun.com/document_detail/72213.html)      | Submits a video snapshot job and starts asynchronous snapshot processing. This operation supports normal snapshots and sprite snapshots. |
| [SubmitDynamicImageJob](https://help.aliyun.com/document_detail/186842.html) | Submits an animated image job and starts asynchronous processing.                                                                        |
| [SubmitPreprocessJobs]()                                                     | Preprocesses a video by using the production studio.                                                                                     |



**Transcoding templates** 


|                      Operation                       |                                                                                               Description                                                                                                |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [AddTranscodeTemplateGroup]()        | Configures a transcoding template group. You can create a transcoding template group or add one or more transcoding templates to a specified transcoding template group.                                 |
| [UpdateTranscodeTemplateGroup]()     | Modifies the configurations of a transcoding template group. You can modify the configurations of the specified transcoding templates in a transcoding template group.                                   |
| [DeleteTranscodeTemplateGroup]()     | Deletes the configurations of a transcoding template group. You can remove one or more transcoding templates from a transcoding template group or forcibly delete the entire transcoding template group. |
| [ListTranscodeTemplateGroup]()       | Queries transcoding template groups.                                                                                                                                                                     |
| [SetDefaultTranscodeTemplateGroup]() | Specifies a transcoding template group as the default one.                                                                                                                                               |
| [GetTranscodeTemplateGroup]()        | Queries the details of a transcoding template group based on the transcoding template group ID.                                                                                                          |



**Video watermarks** 


|                                         Operation                                         |                Description                |
|-------------------------------------------------------------------------------------------|-------------------------------------------|
| [AddWatermark](https://help.aliyun.com/document_detail/98617.html)        | Creates a watermark.                      |
| [UpdateWatermark](https://help.aliyun.com/document_detail/98663.html)     | Modifies a watermark.                     |
| [DeleteWatermark](https://help.aliyun.com/document_detail/98665.html)     | Deletes a watermark.                      |
| [ListWatermark](https://help.aliyun.com/document_detail/98668.html)       | Queries watermarks.                       |
| [GetWatermark](https://help.aliyun.com/document_detail/98669.html)        | Queries a single watermark.               |
| [SetDefaultWatermark](https://help.aliyun.com/document_detail/98670.html) | Specifies a watermark as the default one. |



**Snapshot templates** 


|                                        Operation                                        |             Description             |
|-----------------------------------------------------------------------------------------|-------------------------------------|
| [AddVodTemplate](https://help.aliyun.com/document_detail/99406.html)    | Creates a snapshot template.        |
| [UpdateVodTemplate](https://help.aliyun.com/document_detail/99427.html) | Modifies a snapshot template.       |
| [DeleteVodTemplate](https://help.aliyun.com/document_detail/99430.html) | Deletes a snapshot template.        |
| [ListVodTemplate](https://help.aliyun.com/document_detail/99432.html)   | Queries snapshot templates.         |
| [GetVodTemplate](https://help.aliyun.com/document_detail/99435.html)    | Queries a single snapshot template. |



**Transcoding tasks** 


|                                         Operation                                          |                                                                                                                             Description                                                                                                                              |
|--------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [GetTranscodeSummary](https://help.aliyun.com/document_detail/109119.html) | Queries the transcoding summary of one or more videos based on the video ID. The transcoding summary includes the transcoding status and transcoding progress. A video may be transcoded multiple times. This operation returns only the latest transcoding summary. |
| [ListTranscodeTask](https://help.aliyun.com/document_detail/109120.html)   | Queries the historical transcoding tasks of a video based on the video ID. This operation does not return the detailed job information.                                                                                                                              |
| [GetTranscodeTask](https://help.aliyun.com/document_detail/109121.html)    | Queries the details of transcoding jobs based on the transcoding task ID.                                                                                                                                                                                            |



Online video editing 
-----------------------------------------

**Editing and production** 


|                                            Operation                                             |                    Description                     |
|--------------------------------------------------------------------------------------------------|----------------------------------------------------|
| [ProduceEditingProjectVideo](https://help.aliyun.com/document_detail/68536.html) | Produces a video from one or more mezzanine files. |



**Editing project management** 


|                                                              Operation                                                               |                          Description                          |
|--------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| [AddEditingProject](https://help.aliyun.com/document_detail/69048.html)                                              | Creates an online editing project.                            |
| [UpdateEditingProject](https://help.aliyun.com/document_detail/69049.html)                                           | Modifies an online editing project.                           |
| [DeleteEditingProject](/intl.en-US/API Reference/Video editing/Editing Projects/DeleteEditingProject.md)             | Deletes one or more online editing projects.                  |
| [GetEditingProject](/intl.en-US/API Reference/Video editing/Editing Projects/GetEditingProject.md)                   | Queries the details of an online editing project.             |
| [SearchEditingProject](/intl.en-US/API Reference/Video editing/Editing Projects/SearchEditingProject.md)             | Queries online editing projects.                              |
| [SetEditingProjectMaterials](/intl.en-US/API Reference/Video editing/Editing Projects/SetEditingProjectMaterials.md) | Sets materials to be edited for an online editing project.    |
| [GetEditingProjectMaterials](https://help.aliyun.com/document_detail/69051.html)                                     | Queries materials to be edited for an online editing project. |



Media review 
---------------------------------

**Review settings** 


|                                                        Operation                                                        |                            Description                             |
|-------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| [SetAuditSecurityIp](https://help.aliyun.com/document_detail/87249.html)                                | Adds IP addresses to review security groups.                       |
| [ListAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/ListAuditSecurityIp.md) | Queries the IP addresses that are added to review security groups. |



**Manual review** 


|                                                    Operation                                                    |                             Description                              |
|-----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| [CreateAudit](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md)         | Performs manual review on media files such as audio and video files. |
| [GetAuditHistory](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md) | Queries the manual review history.                                   |



**Automated review** 


|                     Operation                      |                                                                                              Description                                                                                               |
|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SubmitAIMediaAuditJob]()          | Submits an automated review job. After the job is submitted, ApsaraVideo VOD processes the job asynchronously. Therefore, the operation may return a response before the job is complete.              |
| [SubmitAIImageAuditJob]()          | Submits an automated review job for an image. After the job is submitted, ApsaraVideo VOD processes the job asynchronously. Therefore, the operation may return a response before the job is complete. |
| [GetAIMediaAuditJob]()             | Queries an automated review job. After a job is submitted, ApsaraVideo VOD processes the job asynchronously. You can call this operation to query the job information in real time.                    |
| [GetMediaAuditResult]()            | Queries the summary of automated review results.                                                                                                                                                       |
| [GetMediaAuditResultDetail]()      | Queries the details of automated review results. You can call this operation to query the details of review results in real time.                                                                      |
| [GetMediaAuditResultTimeline]()    | Queries the timelines of all snapshots that contain violations.                                                                                                                                        |
| [GetMediaAuditAudioResultDetail]() | Queries the details of audio review results.                                                                                                                                                           |



Video AI 
-----------------------------

**Basic operations** 


|            Operation            |                                                                                 Description                                                                                 |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SubmitAIJob]() | Submits an AI job. After the job is submitted, ApsaraVideo VOD processes the job asynchronously. Therefore, the operation may return a response before the job is complete. |
| [ListAIJob]()   | Queries AI jobs. After a job is submitted, ApsaraVideo VOD processes the job asynchronously. You can call this operation to query the job information in real time.         |



**AI templates** 


|                Operation                 |                   Description                   |
|------------------------------------------|-------------------------------------------------|
| [AddAITemplate]()        | Creates an AI template.                         |
| [DeleteAITemplate]()     | Deletes an AI template.                         |
| [UpdateAITemplate]()     | Modifies an AI template.                        |
| [GetAITemplate]()        | Queries the details of an AI template.          |
| [ListAITemplate]()       | Queries AI templates.                           |
| [SetDefaultAITemplate]() | Specifies an AI template as the default one.    |
| [GetDefaultAITemplate]() | Queries the details of the default AI template. |



**Media fingerprinting** 


|               Operation               |                                                                        Description                                                                         |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [GetMediaDNAResult]() | Queries a media fingerprinting result. After a media fingerprinting job is complete, you can call this operation to query the media fingerprinting result. |



**Smart tags** 


|               Operation               |         Description         |
|---------------------------------------|-----------------------------|
| [GetMediaDNAResult]() | Queries a smart tag result. |



**Intelligent thumbnails** 


|               Operation                |                                      Description                                       |
|----------------------------------------|----------------------------------------------------------------------------------------|
| [SubmitAIImageJob]()   | Submits a job of image AI processing.                                                  |
| [GetAIImageJobs]()     | Queries jobs of image AI processing.                                                   |
| [ListAIImageInfo]()    | Queries the AI processing results about the images of a specified video.               |
| [DeleteAIImageInfos]() | Deletes the information about one or more images that are submitted for AI processing. |



Live to VOD 
--------------------------------



|                                             Operation                                              |         Description         |
|----------------------------------------------------------------------------------------------------|-----------------------------|
| [ListLiveRecordVideo](/intl.en-US/API Reference/Conversion/ListLiveRecordVideo.md) | Queries live-to-VOD videos. |



CDN for ApsaraVideo VOD 
--------------------------------------------

**Data monitoring** 


|                                                             Operation                                                             |                                       Description                                       |
|-----------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| [DescribeVodDomainTrafficData](/intl.en-US/API Reference/VoD CDN/Data Monitoring/DescribeVodDomainTrafficData.md) | Queries the network traffic for one or more specified domain names for CDN. Unit: byte. |
| [DescribeVodDomainBpsData](/intl.en-US/API Reference/VoD CDN/Data Monitoring/DescribeVodDomainBpsData.md)         | Queries the bandwidth for one or more specified domain names for CDN.                   |



**Domain name management** 


|                  Operation                  |                                                                                               Description                                                                                               |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [AddVodDomain]()            | Adds a domain name for CDN to ApsaraVideo VOD. You can add only one domain name for CDN to ApsaraVideo VOD each time. You can add a maximum of 20 domain names for CDN within an Alibaba Cloud account. |
| [UpdateVodDomain]()         | Modifies a specified domain name for CDN.                                                                                                                                                               |
| [DeleteVodDomain]()         | Removes a domain name for CDN from ApsaraVideo VOD.                                                                                                                                                     |
| [BatchStartVodDomain]()     | Enables one or more domain names for CDN that are disabled. After a domain name for CDN is enabled, the value of the DomainStatus parameter is changed to online.                                       |
| [BatchStopVodDomain]()      | Disables one or more domain names for CDN. After a domain name for CDN is disabled, the value of the DomainStatus parameter is changed to offline.                                                      |
| [DescribeVodUserDomains]()  | Queries the domain names for CDN within your Alibaba Cloud account.                                                                                                                                     |
| [DescribeVodDomainDetail]() | Queries the basic information about a specified domain name for CDN.                                                                                                                                    |



**Domain name configurations** 


|                      Operation                       |                                                                                                   Description                                                                                                    |
|------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BatchSetVodDomainConfigs]()         | Configures one or more domain names for CDN.                                                                                                                                                                     |
| [DescribeVodDomainConfigs]()         | Queries the configurations of a specified domain name for CDN. You can query the configurations of one or more features at a time.                                                                               |
| [DeleteVodSpecificConfig]()          | Deletes the configurations of a domain name for CDN.                                                                                                                                                             |
| [SetVodDomainCertificate]()          | Enables or disables the Secure Sockets Layer (SSL) certificate for a specified domain name for CDN. When you call this operation to enable the SSL certificate, you can also modify the certificate information. |
| [DescribeVodCertificateList]()       | Queries the certificates of a specified domain name for CDN or all the domain names for CDN within your Alibaba Cloud account.                                                                                   |
| [DescribeVodDomainCertificateInfo]() | Queries the certificate information about a specific domain name for CDN.                                                                                                                                        |



**Refresh and prefetch** 


|                                                           Operation                                                            |                                                                                                                           Description                                                                                                                           |
|--------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [PreloadVodObjectCaches](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/PreloadVodObjectCaches.md)   | Prefetches resources from an origin server to L2 nodes. Users can directly hit the cache upon their first visits. This way, workloads on the origin server can be reduced. This operation supports POST requests and request parameters are in the form format. |
| [RefreshVodObjectCaches](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/RefreshVodObjectCaches.md)   | Refreshes files on Alibaba Cloud CDN nodes. You can refresh multiple files at a time based on URLs. This operation supports POST requests and request parameters are in the form format.                                                                        |
| [DescribeVodRefreshTasks](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/DescribeRefreshTasks.md)    | Queries the information about one or more refresh or prefetch tasks.                                                                                                                                                                                            |
| [DescribeVodRefreshQuota](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/DescribeVodRefreshQuota.md) | Queries the maximum number and remaining number of requests to refresh or prefetch files on the current day. You can prefetch files based on URLs and refresh files based on URLs or directories.                                                               |



**Log management** 


|                                                    Operation                                                     |                                              Description                                              |
|------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| [DescribeVodDomainLog](/intl.en-US/API Reference/VoD CDN/Log Management/DescribeVodDomainLog.md) | Queries the information about the raw access logs for a specific domain name, including the log path. |



Data statistics 
------------------------------------

**Resource usage** 


|                   Operation                    |                                                     Description                                                      |
|------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| [DescribeVodDomainUsageData]() | Queries the traffic or bandwidth data for one or more domain names for CDN.                                          |
| [DescribeVodStorageData]()     | Queries the statistics of media asset management, including the storage statistics and outbound traffic for storage. |
| [DescribeVodTranscodeData]()   | Queries the statistics on transcoding of different specifications.                                                   |
| [DescribeVodAIData]()          | Queries the statistics on video AI of different types, such as automated review and media fingerprinting.            |



**Playback statistics** 


|                                                      Operation                                                       |                                                                     Description                                                                      |
|----------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| [DescribePlayTopVideos](/intl.en-US/API Reference/Statistics/Play Data/DescribePlayTopVideos.md)     | Queries the playback statistics of daily top videos. The playback statistics includes the video views, unique visitors, and total playback duration. |
| [DescribePlayUserAvg](/intl.en-US/API Reference/Statistics/Play Data/DescribePlayUserAvg.md)         | Queries the statistics on average playback each day in a specified time range.                                                                       |
| [DescribePlayUserTotal](/intl.en-US/API Reference/Statistics/Play Data/DescribePlayUserTotal.md)     | Queries the statistics on total playback each day in a specified time range.                                                                         |
| [DescribePlayVideoStatis](/intl.en-US/API Reference/Statistics/Play Data/DescribePlayVideoStatis.md) | Queries daily playback statistics on a video in a specified time range.                                                                              |



Multi-application service 
----------------------------------------------

**Application management** 


|             Operation             |                                      Description                                      |
|-----------------------------------|---------------------------------------------------------------------------------------|
| [CreateAppInfo]() | Creates an application.                                                               |
| [GetAppInfos]()   | Queries the information about one or more applications based on application IDs.      |
| [ListAppInfo]()   | Queries the applications that you are authorized to manage based on query conditions. |
| [UpdateAppInfo]() | Updates the information about an application.                                         |
| [DeleteAppInfo]() | Deletes an application.                                                               |



**Authorization management** 


|                    Operation                    |                                                    Description                                                     |
|-------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| [AttachAppPolicyToIdentity]()   | Grants the permissions on an application of ApsaraVideo VOD to a specified RAM user or RAM role.                   |
| [ListAppPoliciesForIdentity]()  | Queries the permissions that are granted to a specified RAM user or RAM role on an application of ApsaraVideo VOD. |
| [DetachAppPolicyFromIdentity]() | Revokes the permissions on an application of ApsaraVideo VOD from a specified RAM user or RAM role.                |



**Resource migration** 


|              Operation              |                                Description                                 |
|-------------------------------------|----------------------------------------------------------------------------|
| [MoveAppResource]() | Migrates one or more resources from an application to another application. |



Global configurations 
------------------------------------------

**Event notifications** 


|                                                          Operation                                                           |                                     Description                                     |
|------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| [SetMessageCallback](/intl.en-US/API Reference/Global Config/Event notification/SetMessageCallback.md)       | Sets the callback method, callback URL, and event type of an event notification.    |
| [GetMessageCallback](/intl.en-US/API Reference/Global Config/Event notification/GetMessageCallback.md)       | Queries the callback method, callback URL, and event type of an event notification. |
| [DeleteMessageCallback](/intl.en-US/API Reference/Global Config/Event notification/DeleteMessageCallback.md) | Deletes the callback method, callback URL, and event type of an event notification. |



**Storage management** 


|                 Operation                 |                                Description                                |
|-------------------------------------------|---------------------------------------------------------------------------|
| [SetCrossdomainContent]() | Updates the cross-domain policy file crossdomain.xml for ApsaraVideo VOD. |





