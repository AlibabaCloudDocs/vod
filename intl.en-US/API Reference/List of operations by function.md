List of operations by function 
===================================================



The following tables list the API operations available for use in ApsaraVideo VOD. 


**Note**

We recommend that you use [server SDKs](/intl.en-US/Server SDK Reference/Usage notes.md) to call the API operations. For more information about the API endpoint, see [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md). For more information about the usage limits, see Limits.

Media upload 
---------------------------------



|                                                    Operation                                                     |                                                                    Description                                                                     |
|------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md)                 | Obtains a URL and a credential for uploading a video and generates the video ID.                                                                   |
| [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md)               | Obtains a new upload credential after the video upload times out.                                                                                  |
| [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md)                 | Obtains a URL and a credential for uploading an image.                                                                                             |
| [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md) | Obtains a URL and a credential for uploading an auxiliary media asset, such as a watermark file or a subtitle file.                                |
| [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md)                   | Uploads multiple media files based on the URLs of mezzanine files to ApsaraVideo VOD at a time.                                                    |
| [GetURLUploadInfos](/intl.en-US/API Reference/Media upload/GetURLUploadInfos.md)                 | Queries the information about URL-based upload jobs.                                                                                               |
| [DeleteMultipartUpload](/intl.en-US/API Reference/Media upload/DeleteMultipartUpload.md)         | Immediately deletes the fragments generated during upload.                                                                                         |
| [GetUploadDetails](/intl.en-US/API Reference/Media upload/GetUploadDetails.md)                   | Queries the upload details, such as the upload time, upload ratio, and upload source, about one or more media assets based on the media asset IDs. |
| [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md)                         | Registers media assets.                                                                                                                            |



Audio and video playback 
---------------------------------------------



|                                                 Operation                                                  |                                           Description                                            |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md)           | Queries the streaming URL of a media file, such as a video or audio file, based on the video ID. |
| [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md) | Queries the playback credential that is required for playing a video.                            |



Media asset management 
-------------------------------------------

**Media asset search** 


|                                                     Operation                                                     |                                              Description                                              |
|-------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| [SearchMedia](/intl.en-US/API Reference/Media asset management/Media asset search/SearchMedia.md) | Queries the information about media assets such as videos, audio, images, and auxiliary media assets. |



**Media asset categories** 


|                                                         Operation                                                         |                                                                                       Description                                                                                       |
|---------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [AddCategory](/intl.en-US/API Reference/Media asset management/Media asset category/AddCategory.md)       | Creates a video category. A maximum of three category levels can be created. Each category can contain up to 100 subcategories.                                                         |
| [UpdateCategory](/intl.en-US/API Reference/Media asset management/Media asset category/UpdateCategory.md) | Modifies a video category.                                                                                                                                                              |
| [DeleteCategory](/intl.en-US/API Reference/Media asset management/Media asset category/DeleteCategory.md) | Deletes a video category. If a video category is deleted, its subcategories, including level 2 and level 3 categories, are also deleted. Exercise caution when you call this operation. |
| [GetCategories](/intl.en-US/API Reference/Media asset management/Media asset category/GetCategories.md)   | Queries the information about the specified category and its subcategories.                                                                                                             |



**Audio and video management** 


|                                                              Operation                                                              |                                                                                                         Description                                                                                                         |
|-------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [GetVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfo.md)         | Queries the basic information about a video based on the video ID. The basic information includes the title, description, duration, thumbnail URL, status, creation time, size, snapshots, category, and tags of the video. |
| [UpdateVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfo.md)   | Modifies the information about a video.                                                                                                                                                                                     |
| [UpdateVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfos.md) | Modifies the information about multiple videos at a time.                                                                                                                                                                   |
| [DeleteMezzanines](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteMezzanines.md) | Deletes one or more mezzanine files at a time.                                                                                                                                                                              |
| [DeleteStream](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteStream.md)         | Deletes one or more video or audio streams and their storage files at a time.                                                                                                                                               |
| [DeleteVideo](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteVideo.md)           | Deletes one or more videos at a time, including their mezzanine files, transcoded stream files, and thumbnail snapshots.                                                                                                    |
| [GetMezzanineInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetMezzanineInfo.md) | Queries the information about the mezzanine file of an audio or video. The information includes the mezzanine file URL, resolution, and bitrate of the audio or video.                                                      |
| [GetVideoList](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoList.md)         | Queries the information about videos based on query conditions.                                                                                                                                                             |
| [GetVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfos.md)       | Queries the information about multiple videos at a time.                                                                                                                                                                    |



**Image management** 


|                                                         Operation                                                         |                            Description                            |
|---------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| [DeleteImage](/intl.en-US/API Reference/Media asset management/Image management/DeleteImage.md)           | Deletes uploaded images and automatic snapshots of videos.        |
| [GetImageInfo](/intl.en-US/API Reference/Media asset management/Image management/GetImageInfo.md)         | Queries the basic information about an image.                     |
| [UpdateImageInfos](/intl.en-US/API Reference/Media asset management/Image management/UpdateImageInfos.md) | Modifies the information about one or more images at a time.      |
| [ListSnapshots](/intl.en-US/API Reference/Media asset management/Image management/ListSnapshots.md)       | Queries the snapshots that are captured from the specified media. |



**Auxiliary media asset management** 


|                                                                         Operation                                                                         |                                                                                 Description                                                                                  |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [GetAttachedMediaInfo](/intl.en-US/API Reference/Media asset management/Auxiliary media asset management/GetAttachedMediaInfo.md)         | Queries the basic information about one or more auxiliary media assets. The basic information includes the title, type, tags, and creation time of an auxiliary media asset. |
| [UpdateAttachedMediaInfos](/intl.en-US/API Reference/Media asset management/Auxiliary media asset management/UpdateAttachedMediaInfos.md) | Modifies the information about multiple auxiliary media assets at a time.                                                                                                    |
| [DeleteAttachedMedia](/intl.en-US/API Reference/Media asset management/Auxiliary media asset management/DeleteAttachedMedia.md)           | Deletes one or more auxiliary media assets at a time.                                                                                                                        |



**Animated sticker management** 


|                                                                Operation                                                                 |                                   Description                                   |
|------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| [ListDynamicImage](/intl.en-US/API Reference/Media asset management/Animated sticker management/ListDynamicImage.md)     | Queries the information about animated stickers that are captured from a video. |
| [DeleteDynamicImage](/intl.en-US/API Reference/Media asset management/Animated sticker management/DeleteDynamicImage.md) | Deletes the information about animated stickers.                                |



Media processing 
-------------------------------------

**Process initiation** 


|                                                            Operation                                                            |                                                                  Description                                                                   |
|---------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md)     | Submits a transcoding job and starts asynchronous transcoding.                                                                                 |
| [SubmitSnapshotJob](/intl.en-US/API Reference/Media processing/Process initiation/SubmitSnapshotJob.md)         | Submits a snapshot job for a video and starts asynchronous snapshot processing. This operation supports normal snapshots and sprite snapshots. |
| [SubmitDynamicImageJob](/intl.en-US/API Reference/Media processing/Process initiation/SubmitDynamicImageJob.md) | Submits an animated image job and starts asynchronous processing.                                                                              |
| [SubmitPreprocessJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitPreprocessJobs.md)   | Preprocesses a video by using the streaming panel.                                                                                             |
| [SubmitWorkflowJob](/intl.en-US/API Reference/Media processing/Process initiation/SubmitWorkflowJob.md)         | Initiates a video-on-demand (VOD) workflow to process audio and video files.                                                                   |



**Transcoding templates** 


|                                                                        Operation                                                                        |                                                                                               Description                                                                                                |
|---------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [AddTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/AddTranscodeTemplateGroup.md)               | Configures a transcoding template group. You can create a transcoding template group or add one or more transcoding templates to a specified transcoding template group.                                 |
| [UpdateTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/UpdateTranscodeTemplateGroup.md)         | Modifies the configurations of a transcoding template group. You can modify the configurations of the specified transcoding templates in a transcoding template group.                                   |
| [DeleteTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/DeleteTranscodeTemplateGroup.md)         | Deletes the configurations of a transcoding template group. You can remove one or more transcoding templates from a transcoding template group or forcibly delete the entire transcoding template group. |
| [ListTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/ListTranscodeTemplateGroup.md)             | Queries transcoding template groups.                                                                                                                                                                     |
| [SetDefaultTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/SetDefaultTranscodeTemplateGroup.md) | Specifies a transcoding template group as the default one.                                                                                                                                               |
| [GetTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/GetTranscodeTemplateGroup.md)               | Queries the details of a transcoding template group based on the transcoding template group ID.                                                                                                          |



**Video watermarks** 


|                                                        Operation                                                         |                Description                |
|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| [AddWatermark](/intl.en-US/API Reference/Media processing/Video watermark/AddWatermark.md)               | Creates a watermark.                      |
| [UpdateWatermark](/intl.en-US/API Reference/Media processing/Video watermark/UpdateWatermark.md)         | Modifies a watermark.                     |
| [DeleteWatermark](/intl.en-US/API Reference/Media processing/Video watermark/DeleteWatermark.md)         | Deletes a watermark.                      |
| [ListWatermark](/intl.en-US/API Reference/Media processing/Video watermark/ListWatermark.md)             | Queries watermarks.                       |
| [GetWatermark](/intl.en-US/API Reference/Media processing/Video watermark/GetWatermark.md)               | Queries a single watermark.               |
| [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video watermark/SetDefaultWatermark.md) | Specifies a watermark as the default one. |



**Snapshot templates** 


|                                                       Operation                                                        |             Description             |
|------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/AddVodTemplate.md)       | Creates a snapshot template.        |
| [UpdateVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/UpdateVodTemplate.md) | Modifies a snapshot template.       |
| [DeleteVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/DeleteVodTemplate.md) | Deletes a snapshot template.        |
| [ListVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/ListVodTemplate.md)     | Queries snapshot templates.         |
| [GetVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot template/GetVodTemplate.md)       | Queries a single snapshot template. |



**Transcoding tasks** 


|                                                         Operation                                                         |                                                                                                                             Description                                                                                                                              |
|---------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [GetTranscodeSummary](/intl.en-US/API Reference/Media processing/Transcoding task/GetTranscodeSummary.md) | Queries the transcoding summary of one or more videos based on the video ID. The transcoding summary includes the transcoding status and transcoding progress. A video may be transcoded multiple times. This operation returns only the latest transcoding summary. |
| [ListTranscodeTask](/intl.en-US/API Reference/Media processing/Transcoding task/ListTranscodeTask.md)     | Queries the historical transcoding tasks of a video based on the video ID. This operation does not return detailed job information.                                                                                                                                  |
| [GetTranscodeTask](/intl.en-US/API Reference/Media processing/Transcoding task/GetTranscodeTask.md)       | Queries the details of transcoding jobs based on the transcoding task ID.                                                                                                                                                                                            |



Online editing 
-----------------------------------

**Editing and production** 


|                                                      Operation                                                       |                    Description                     |
|----------------------------------------------------------------------------------------------------------------------|----------------------------------------------------|
| [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md) | Produces a video from one or more mezzanine files. |



**Project management for online editing** 


|                                                                         Operation                                                                          |                          Description                          |
|------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| [AddEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/AddEditingProject.md)                   | Creates an online editing project.                            |
| [UpdateEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/UpdateEditingProject.md)             | Modifies an online editing project.                           |
| [DeleteEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/DeleteEditingProject.md)             | Deletes one or more online editing projects.                  |
| [GetEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProject.md)                   | Queries the details of an online editing project.             |
| [SearchEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/SearchEditingProject.md)             | Queries online editing projects.                              |
| [SetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/SetEditingProjectMaterials.md) | Sets materials to be edited for an online editing project.    |
| [GetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProjectMaterials.md) | Queries materials to be edited for an online editing project. |



Media review 
---------------------------------

**Review settings** 


|                                                        Operation                                                        |                     Description                      |
|-------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| [SetAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/SetAuditSecurityIp.md)   | Manages the IP addresses in review security groups.  |
| [ListAuditSecurityIp](/intl.en-US/API Reference/Content Moderation/Audit Config/ListAuditSecurityIp.md) | Queries the IP addresses in a review security group. |



**Manual review** 


|                                                    Operation                                                    |                              Description                              |
|-----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| [CreateAudit](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md)         | Performs manual review on media files, such as audio and video files. |
| [GetAuditHistory](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md) | Queries the manual review history.                                    |



Live to VOD 
--------------------------------



|                                              Operation                                              |         Description         |
|-----------------------------------------------------------------------------------------------------|-----------------------------|
| [ListLiveRecordVideo](/intl.en-US/API Reference/Live to VOD/ListLiveRecordVideo.md) | Queries live-to-VOD videos. |



CDN for ApsaraVideo VOD 
--------------------------------------------

**Data monitoring** 


|                                                                     Operation                                                                     |                                       Description                                       |
|---------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| [DescribeVodDomainTrafficData](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Data monitoring/DescribeVodDomainTrafficData.md) | Queries the network traffic for one or more specified domain names for CDN. Unit: byte. |
| [DescribeVodDomainBpsData](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Data monitoring/DescribeVodDomainBpsData.md)         | Queries the bandwidth for one or more specified domain names for CDN.                   |



**Domain name management** 


|                                                                   Operation                                                                    |                                                                                               Description                                                                                               |
|------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [AddVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/AddVodDomain.md)                       | Adds a domain name for CDN to ApsaraVideo VOD. You can add only one domain name for CDN to ApsaraVideo VOD each time. You can add a maximum of 20 domain names for CDN within an Alibaba Cloud account. |
| [UpdateVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/UpdateVodDomain.md)                 | Modifies a specified domain name for CDN.                                                                                                                                                               |
| [DeleteVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/DeleteVodDomain.md)                 | Removes a domain name for CDN from ApsaraVideo VOD.                                                                                                                                                     |
| [BatchStartVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/BatchStartVodDomain.md)         | Enables one or more domain names for CDN that are disabled. After a domain name for CDN is enabled, the value of the DomainStatus parameter is changed to online.                                       |
| [BatchStopVodDomain](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/BatchStopVodDomain.md)           | Disables one or more domain names for CDN. After a domain name for CDN is disabled, the value of the DomainStatus parameter is changed to offline.                                                      |
| [DescribeVodUserDomains](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/DescribeVodUserDomains.md)   | Queries the domain names for CDN within your Alibaba Cloud account.                                                                                                                                     |
| [DescribeVodDomainDetail](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name management/DescribeVodDomainDetail.md) | Queries the basic information about a specified domain name for CDN.                                                                                                                                    |



**Domain name verification** 


|                                                                     Operation                                                                      |                    Description                     |
|----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------|
| [VerifyVodDomainOwner](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name verification/VerifyVodDomainOwner.md)         | Verifies the ownership of a specified domain name. |
| [DescribeVodVerifyContent](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name verification/DescribeVodVerifyContent.md) | Queries the ownership verification content.        |





**Domain name configurations** 


|                                                                              Operation                                                                               |                                                                                                   Description                                                                                                    |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BatchSetVodDomainConfigs](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name configurations/BatchSetVodDomainConfigs.md)                 | Configures one or more domain names for CDN.                                                                                                                                                                     |
| [DescribeVodDomainConfigs](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name configurations/DescribeVodDomainConfigs.md)                 | Queries the configurations of a specified domain name for CDN. You can query the configurations of one or more features at a time.                                                                               |
| [DeleteVodSpecificConfig](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name configurations/DeleteVodSpecificConfig.md)                   | Deletes the configurations of a domain name for CDN.                                                                                                                                                             |
| [SetVodDomainCertificate](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name configurations/SetVodDomainCertificate.md)                   | Enables or disables the Secure Sockets Layer (SSL) certificate for a specified domain name for CDN. When you call this operation to enable the SSL certificate, you can also modify the certificate information. |
| [DescribeVodCertificateList](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name configurations/DescribeVodCertificateList.md)             | Queries the certificates of a specified domain name for CDN or all the domain names for CDN within your Alibaba Cloud account.                                                                                   |
| [DescribeVodDomainCertificateInfo](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Domain name configurations/DescribeVodDomainCertificateInfo.md) | Queries the certificate information about a specific domain name for CDN.                                                                                                                                        |



**Refresh and prefetch** 


|                                                                  Operation                                                                   |                                                                                                                           Description                                                                                                                           |
|----------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [PreloadVodObjectCaches](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/PreloadVodObjectCaches.md)   | Prefetches resources from an origin server to L2 nodes. Users can directly hit the cache upon their first visits. This way, workloads on the origin server can be reduced. This operation supports POST requests and request parameters are in the form format. |
| [RefreshVodObjectCaches](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/RefreshVodObjectCaches.md)   | Refreshes files on Alibaba Cloud CDN nodes. You can refresh multiple files at a time based on URLs. This operation supports POST requests and request parameters are in the form format.                                                                        |
| [DescribeVodRefreshTasks](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/DescribeVodRefreshTasks.md) | Queries the information about one or more refresh or prefetch tasks.                                                                                                                                                                                            |
| [DescribeVodRefreshQuota](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Refresh and prefetch/DescribeVodRefreshQuota.md) | Queries the maximum number and remaining number of requests to refresh or prefetch files on the current day. You can prefetch files based on URLs and refresh files based on URLs or directories.                                                               |



**Log management** 


|                                                            Operation                                                             |                                              Description                                              |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| [DescribeVodDomainLog](/intl.en-US/API Reference/CDN for ApsaraVideo VOD/Log management/DescribeVodDomainLog.md) | Queries the information about the raw access logs for a specific domain name, including the log path. |



Data statistics 
------------------------------------

**Resource usage** 


|                                                              Operation                                                               |                                                     Description                                                      |
|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| [DescribeVodDomainUsageData](/intl.en-US/API Reference/Data statistics/Resource usage/DescribeVodDomainUsageData.md) | Queries the traffic or bandwidth data for one or more domain names for CDN.                                          |
| [DescribeVodStorageData](/intl.en-US/API Reference/Data statistics/Resource usage/DescribeVodStorageData.md)         | Queries the statistics of media asset management, including the storage statistics and outbound traffic for storage. |
| [DescribeVodTranscodeData](/intl.en-US/API Reference/Data statistics/Resource usage/DescribeVodTranscodeData.md)     | Queries the statistics on transcoding of different specifications.                                                   |
| [DescribeVodAIData](/intl.en-US/API Reference/Data statistics/Resource usage/DescribeVodAIData.md)                   | Queries the statistics on video AI of different types, such as automated review and media fingerprinting.            |



**Playback statistics** 


|                                                              Operation                                                              |                                                                     Description                                                                      |
|-------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| [DescribePlayTopVideos](/intl.en-US/API Reference/Data statistics/Playback statistics/DescribePlayTopVideos.md)     | Queries the playback statistics of daily top videos. The playback statistics includes the video views, unique visitors, and total playback duration. |
| [DescribePlayUserAvg](/intl.en-US/API Reference/Data statistics/Playback statistics/DescribePlayUserAvg.md)         | Queries the statistics on average playback each day in a specified time range.                                                                       |
| [DescribePlayUserTotal](/intl.en-US/API Reference/Data statistics/Playback statistics/DescribePlayUserTotal.md)     | Queries the statistics on total playback each day in a specified time range.                                                                         |
| [DescribePlayVideoStatis](/intl.en-US/API Reference/Data statistics/Playback statistics/DescribePlayVideoStatis.md) | Queries daily playback statistics on a video in a specified time range.                                                                              |



Multi-application service 
----------------------------------------------

**Application management** 


|                                                          Operation                                                           |                                      Description                                      |
|------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| [CreateAppInfo](/intl.en-US/API Reference/Multi-application service/Application management/CreateAppInfo.md) | Creates an application.                                                               |
| [GetAppInfos](/intl.en-US/API Reference/Multi-application service/Application management/GetAppInfos.md)     | Queries the information about one or more applications based on application IDs.      |
| [ListAppInfo](/intl.en-US/API Reference/Multi-application service/Application management/ListAppInfo.md)     | Queries the applications that you are authorized to manage based on query conditions. |
| [UpdateAppInfo](/intl.en-US/API Reference/Multi-application service/Application management/UpdateAppInfo.md) | Updates the information about an application.                                         |
| [DeleteAppInfo](/intl.en-US/API Reference/Multi-application service/Application management/DeleteAppInfo.md) | Deletes an application.                                                               |



**Authorization management** 


|                                                                         Operation                                                                          |                                                    Description                                                     |
|------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| [AttachAppPolicyToIdentity](/intl.en-US/API Reference/Multi-application service/Authorization management/AttachAppPolicyToIdentity.md)     | Grants the permissions on an application of ApsaraVideo VOD to a specified RAM user or RAM role.                   |
| [ListAppPoliciesForIdentity](/intl.en-US/API Reference/Multi-application service/Authorization management/ListAppPoliciesForIdentity.md)   | Queries the permissions that are granted to a specified RAM user or RAM role on an application of ApsaraVideo VOD. |
| [DetachAppPolicyFromIdentity](/intl.en-US/API Reference/Multi-application service/Authorization management/DetachAppPolicyFromIdentity.md) | Revokes the permissions on an application of ApsaraVideo VOD from a specified RAM user or RAM role.                |



**Resource migration** 


|                                                          Operation                                                           |                                Description                                 |
|------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| [MoveAppResource](/intl.en-US/API Reference/Multi-application service/Resource migration/MoveAppResource.md) | Migrates one or more resources from an application to another application. |



Global configurations 
------------------------------------------

**Event notifications** 


|                                                               Operation                                                               |                                     Description                                     |
|---------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| [SetMessageCallback](/intl.en-US/API Reference/Global configurations/Event notifications/SetMessageCallback.md)       | Sets the callback method, callback URL, and event type of an event notification.    |
| [GetMessageCallback](/intl.en-US/API Reference/Global configurations/Event notifications/GetMessageCallback.md)       | Queries the callback method, callback URL, and event type of an event notification. |
| [DeleteMessageCallback](/intl.en-US/API Reference/Global configurations/Event notifications/DeleteMessageCallback.md) | Deletes the callback method, callback URL, and event type of an event notification. |



**Storage management** 


|                                                              Operation                                                               |                      Description                      |
|--------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| [SetCrossdomainContent](/intl.en-US/API Reference/Global configurations/Storage management/SetCrossdomainContent.md) | Updates the cross-domain policy file crossdomain.xml. |





