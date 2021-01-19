# Comparison between credentials and STS

Upload credentials, playback credentials, and Security Token Service \(STS\) can be used to handle authorization and security issues in the upload and playback processes to prevent malicious upload and playback.

-   Upload credential

    Upload credentials are issued by ApsaraVideo VOD and are used to upload media files to OSS. Upload credentials have validity periods and limits on access objects and access times. For more information, see [Upload URLs and credentials](/intl.en-US/Developer Guide/Upload Medias/Upload URL and credential.md).

-   Playback credentials

    Playback credentials are issued by ApsaraVideo VOD and are used for the player to obtain playback URLs. Playback credentials have validity periods and limits on access objects and access times. For more information, see [Play by using playback URLs](/intl.en-US/Developer Guide/Video play/Use playback URLs.md).

-   STS

    STS is a cloud service that provides short-term access control for Alibaba Cloud accounts \(or RAM users\). STS issues an access credential with a custom validity period and access permissions to third-party users. Then, the third-party users can use the STS access credential to call Alibaba Cloud APIs or log on to the Alibaba Cloud Management Console to manage authorized resources. For more information, see [Create a role and grant temporary access permissions to the role by using STS](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md).


## Benefits of credentials

Upload and playback credentials are recommended for use in ApsaraVideo VOD. The following table compares these credentials with STS.

|Item|Credential|STS|
|----|----------|---|
|Ease of use|Upload and playback credentials are easy to use. They can be used after you have the AccessKey pairs ready and are granted permissions on accessing ApsaraVideo VOD.|STS requires complicated configurations of roles and policies.|
|Security|Upload and playback credentials are used on a per video basis and can be used only once.|STS is used at the API operation level in ApsaraVideo for VOD. After receiving STS authorization, you can upload as many videos as you want and play any videos in your account.|
|Flexibility|Upload and playback credentials allow you to configure more parameters. For example, you can specify the message callback URL when you upload media files or specify the domain name when you play media files. For more information, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md) and [GetVideoPlayAuth](/intl.en-US/API Reference/Video playback/GetVideoPlayAuth.md).|New iterative versions of the client SDK must be released before new features can be used.|
|Access capacity|By default, upload and playback credentials allow for a larger number of access times. They support automatic scaling to process personalized authorization requests from any number of users.|STS is a centralized service. It manages authorization for all products and has strict throttling requirements. This makes STS unsuitable for high concurrency access.|

