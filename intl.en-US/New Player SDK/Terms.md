# Terms

This topic describes the general terms that are used in the ApsaraVideo VOD console or related documentations. This helps you understand and use ApsaraVideo VOD with ease.

## Terms

-   RAM and STS

    Resource Access Management \(RAM\) and Security Token Service \(STS\) are permission management systems that are provided by Alibaba Cloud. You can create RAM users within your Alibaba Cloud account and grant different permissions to them. STS is a security token management system that grants temporary access permissions. STS can be used to grant access permissions to temporary users. For more information, see [Create a role and grant temporary access permissions to the role by using STS](/intl.en-US/Developer Guide/Access authorization/Create a role and grant temporary access permissions to the role by using STS.md).

-   PlayConfig

    A field that specifies the custom configuration for media playback. The value is a JSON string. You can specify a streaming domain to play videos. For more information, see [Request parameters](/intl.en-US/API Reference/Appendix/Request parameters.md).

-   Temporary AccessKey ID, AccessKey secret, and security token

    The AccessKey ID, AccessKey secret, and security token are obtained by using the STS API or ApsaraVideo VOD SDKs after RAM authorization is enabled. They are used to make playback and download requests. For more information, see [STS SDK overview](https://help.aliyun.com/document_detail/121136.html?spm=a2c4g.11186623.2.13.5a25928b9vFwg3).

-   PlayAuth

    The unique credential for video playback. Each playback credential is bound to a user ID. Playback credentials cannot be exchanged among different users. Otherwise, videos cannot be played. By default, a playback credential has a limited validity period of 100 seconds. For more information, see [Obtain a playback credential](/intl.en-US/New Player SDK/Playback credential.md).

-   Hotlink protection

    ApsaraVideo VOD checks the referer in the header of a request to determine whether the request is originated from the local site and whether the requested video can be played. You can set the referer in the ApsaraVideo VOD or Alibaba Cloud CDN console. For more information, see [Hotlink protection](/intl.en-US/User Guide/Domain management/Access control/Hotlink protection.md).

-   Secure download

    Secure download is a process where a private key is used to perform secondary encryption on videos when they are downloaded. After a video is downloaded, ApsaraVideo Player SDK decrypts the video. This ensures that the offline video can be played only by the application with the bundle ID or keystore that is specified in secure download settings. This feature is available only to ApsaraVideo VOD and ApsaraVideo for Media Processing users. For more information, see [Secure download](/intl.en-US/New Player SDK/Best practice/Secure download.md).


