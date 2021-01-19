# Obtain a playback credential

ApsaraVideo Player SDK allows you to use playback credentials or Security Token Service \(STS\) to ensure secure playback of audio and video files. The player can automatically obtain and decode the streaming URL based on the authorization information.

## Comparison

We recommend that you use upload and playback credentials to implement upload and playback authorization in ApsaraVideo VOD. The following table describes the advantages of credentials over STS.

|Item|Credential|STS|
|----|----------|---|
|Ease of use|Upload and playback credentials are easy to use. They can be used after you have the AccessKey pairs ready and are granted permissions on accessing ApsaraVideo VOD.|STS requires complicated configurations of roles and policies.|
|Security|Upload and playback credentials are used on a per video basis and can be used only once.|STS is used at the API operation level in ApsaraVideo for VOD. After receiving STS authorization, you can upload as many videos as you want and play any videos in your account.|
|Flexibility|Upload and playback credentials allow you to configure more parameters. For example, you can specify the message callback URL when you upload media files or specify the domain name when you play media files. For more information, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md) and [GetVideoPlayAuth](/intl.en-US/API Reference/Video playback/GetVideoPlayAuth.md).|New iterative versions of the client SDK must be released before new features can be used.|
|Access capacity|By default, upload and playback credentials allow for a larger number of access times. They support automatic scaling to process personalized authorization requests from any number of users.|STS is a centralized service. It manages authorization for all products and has strict throttling requirements. This makes STS unsuitable for high concurrency access.|

**Note:** By using a playback credential, you can use ApsaraVideo VOD in an easier and secure way. Compared with STS, playback credentials have more advantages. For more information, see [Comparison between credentials and STS](/intl.en-US/Developer Guide/Access authorization/Comparison between credentials and STS.md).

## Instruction

For more information about how to obtain and use a playback credential, see [t1959342.md\#](/intl.en-US/Developer Guide/Video play/Use playback credentials to play videos.md).

