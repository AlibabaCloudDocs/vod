Overview 
=============================

ApsaraVideo VOD is an all-in-one solution for on-demand audio and video streaming. It provides features such as video collection, editing, uploading, automated transcoding, online editing, delivery acceleration, and playback as well as media resource management. The Developer Guide introduces these features and describes how to use them.

Overall process 
------------------------------------

The following figure shows the overall process for audio and video uploading, storage, processing, and playback in ApsaraVideo VOD.![Flowchart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7426201161/p182454.png)
**Note**

The preceding figure shows a standard process that includes transcoding and credential-based playback. If transcoding is disabled or if media review is enabled, the process may change accordingly.

1. The user obtains the upload permission.

   

2. ApsaraVideo VOD delivers the upload URL, upload credential, and video ID (VideoId).

   

3. The user uploads a video and saves the video ID (VideoId).

   

4. The server obtains the playback permission.

   

5. The client requests the playback URL and credential. ApsaraVideo VOD delivers the playback URL and the playback credential with a validity period.

   

6. The server delivers the playback credential to the client for video playback.

   




Access and storage 
---------------------------------------

Before you use ApsaraVideo VOD, you must have a knowledge about service regions, API regions, and storage regions. ApsaraVideo VOD provides access in a number of regions around the world. Each endpoint corresponds to a storage region. You cannot call resources across storage regions. For the mappings between service regions, API regions, and supported storage regions, see [VOD centers and endpoints](/intl.en-US/Developer Guide/VOD centers and endpoints.md).

Global configurations 
------------------------------------------



|       Configuration       |                                                                                                                                                                                                                    Description                                                                                                                                                                                                                    |                                                   Reference                                                    |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| Account and authorization | ApsaraVideo VOD supports Resource Access Management (RAM) and Security Token Service (STS). You can use one of the following methods to perform authorization operations: * Attach system policies to RAM users   * Attach custom policies to RAM users   * Grant permissions to roles by using STS           | [Account and authorization](/intl.en-US/Developer Guide/Access authorization/Overview.md)      |
| Multi-application service | ApsaraVideo VOD allows you to isolate resources, configurations, and data of multiple users in the same account. You can build the multi-application service by managing applications and attaching policies to identity entities.                                                                                                                                                                                                                | [Multi-application service](/intl.en-US/Developer Guide/Multi-application service/Overview.md) |
| Event notification        | ApsaraVideo VOD supports event notifications through callbacks. * HTTP callback (HTTPS compatible)   * Alibaba Cloud Message Service (MNS) callback                                                                                                                                                                                            | [Event notification](/intl.en-US/Developer Guide/Event notification/Overview.md)               |
| Video security            | ApsaraVideo VOD provides a wide range of security mechanisms to ensure security of video content: * Access control   * URL signing by ApsaraVideo VOD   * CDN re-authentication by the customer   * Video encryption   * Secure download    | [Video security](/intl.en-US/Developer Guide/Video security/Overview.md)                       |



Features 
-----------------------------



|         Feature          |                                                                                                                                                                                                                                                                                   Description                                                                                                                                                                                                                                                                                   |                                                                                                                                                 Reference                                                                                                                                                  |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Media upload             | ApsaraVideo VOD allows you to upload media files (including audio, video, and image files) to OSS buckets allocated by ApsaraVideo VOD. Before you upload media files, you must obtain the upload URL and credential from ApsaraVideo VOD. The following upload methods are supported: * Upload in the ApsaraVideo VOD console   * Upload from the server   * Upload from the client   * Upload offline    | [Media upload](/intl.en-US/Developer Guide/Upload Medias/Overview.md)                                                                                                                                                                                                                      |
| Media management         | ApsaraVideo VOD allows you to manage media resources such as basic information, source file information, playback information, and AI data that are generated after media upload or processing. You can obtain, update, search, download, or delete these resources.                                                                                                                                                                                                                                                                                                            | [Media management](/intl.en-US/Developer Guide/Media asset management/Overview.md)                                                                                                                                                                                                         |
| Media processing         | ApsaraVideo VOD provides basic media processing capabilities such as audio and video transcoding, video snapshotting, frame animation, and video watermarking, as well as advanced features such as automated review and online editing.                                                                                                                                                                                                                                                                                                                                        | [Media processing](/intl.en-US/Developer Guide/Media processing/Overview.md) [Media review](/intl.en-US/Developer Guide/Media review/Overview.md) [Online editing](/intl.en-US/Developer Guide/Online editing/Overview.md) |
| Audio and video playback | ApsaraVideo VOD provides three methods for you to playback audio and video files: preview in the console, use the ApsaraVideo Player SDK, and use third-party players.                                                                                                                                                                                                                                                                                                                                                                                                          | [Audio and video playback](/intl.en-US/Developer Guide/Video play/Overview.md)                                                                                                                                                                                                             |
| Live-to-VOD              | ApsaraVideo VOD allows you to synchronously record live streams as videos for on-demand playback.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | [Live-to-VOD](/intl.en-US/Developer Guide/Live-to-VOD/Overview.md)                                                                                                                                                                                                                         |


