# Alibaba Cloud video encryption

This topic describes the benefits, the overall architecture, and access methods of Alibaba Cloud video encryption. This topic also introduces best practices to enhance solutions.

## Background information

Users can pay a one-time fee for a video and download the video file from the playback URL that has hotlink protection. However, distribution of the video file cannot be controlled after the video file is downloaded from the playback URL. Therefore, hotlink protection is not enough to protect video copyrights.

## Advantages

Alibaba Cloud video encryption service **encrypts video data**. Video files downloaded to a local device are encrypted, which prevents unauthorized redistribution. Video encryption can prevent video leakage and hotlinking. Video encryption can be applied to a wide range of online copyrighted video fields such as **online education, finance, industry training, and premium TV shows**.

Alibaba Cloud utilizes the private encryption algorithm to provide a high level of security, which allows you to protect your video resources in a convenient, efficient, and secure manner.

-   Each media file has a dedicated encryption key. This way, if a single key is leaked, a large number of video files are not exposed.
-   ApsaraVideo VOD provides a comprehensive permission management system. You can create RAM users and use playback credentials to control the access permissions.
-   ApsaraVideo VOD uses ciphertext and plaintext keys to provide an envelope encryption system. The plaintext keys are not stored and are used only to process data in the memory.
-   ApsaraVideo VOD provides secure player kernel SDKs.

## Overall architecture

Alibaba Cloud video encryption consists of two parts: **encryption and transcoding** and **decryption and playback**.

-   Encryption and transcoding
    1.  A video encryption request is initiated in the application background

        You submit a transcoding job that requires data encryption.

    2.  ApsaraVideo VOD obtains the encryption key

        ApsaraVideo VOD uses Key Management Service \(KMS\) to generate a plaintext key and a ciphertext key.

    3.  Video encryption and transcoding

        ApsaraVideo VOD uses the plaintext key to encrypt the video file. After the video file is transcoded, the plaintext key is discarded.

    4.  Message notification after transcoding completion

        ApsaraVideo VOD saves the encrypted video file and sends you a notification.

-   Decryption and playback
    1.  Authorization

        When a user requests to play a video by using a mobile application or web page, the request is first sent to your API or backend page. You can configure permission control to manage content. For example, you can require users to log on before they can play the video. We recommend that you configure HTTPS for your added CDN domain name. If the playback request is authorized, the AccessKey of the RAM user is used to access ApsaraVideo VOD and obtain a playback credential. Then, the playback credential is sent to the mobile application or web page.

    2.  Obtain the playback URL

        The mobile application or web page sends the playback credential and media ID to ApsaraVideo Player. ApsaraVideo Player SDK proceeds with the following operations:

        -   Obtain the playback URL for the specific video format and definition from ApsaraVideo VOD based on the media ID.
        -   Obtain the encryption key of the encrypted video.
    3.  Decryption and playback

        ApsaraVideo VOD provides secure player kernel SDKs, which use the encryption key to decrypt and play the video.


**Note:**

-   The output files after the video is encrypted must be in the HLS format.
-   You must use the iOS, Android, HTML5, and Flash players provided by ApsaraVideo VOD to decrypt and play encrypted videos.

## Access method

Prerequisites:

1.  [ApsaraVideo VOD](/intl.en-US/Quick Start/Get started with ApsaraVideo for VOD.md) is activated.

2.  A domain name is added. For more information, see [Add a domain name](/intl.en-US/User Guide/Domain management/Add a domain name.md).

3.  A CNAME is bound to the CDN domain name of ApsaraVideo VOD. For more information, see [Configure a CNAME record in Alibaba Cloud DNS](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure a CNAME record in Alibaba Cloud DNS.md).


Access process:

1.  On the [Added Transcoding Template Group](https://vod.console.aliyun.com/#/settings/transcode/add) page, select an encryption template. For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).
    -   Set **Basic Parameters-Encapsulation Format** to **hls**.
    -   Turn on **Video Encryption** in the Advanced Parameters section to encrypt data.
2.  Video uploading

    To upload a video to ApsaraVideo VOD, you can use an SDK, an API, the ApsaraVideo VOD console, or a third-party OSS tool. For more information, see [Upload Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md)

3.  Video transcoding

    After the video is uploaded, the video is transcoded. The transcoded video is marked as **Normal** and is available for playback. For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).

4.  Video playback

    ApsaraVideo VOD provides player SDKs that can be integrated on multiple platforms, which include iOS, Android, HTML5, and Flash. You can use the required player SDK to play the video on your application or web page.

    **Note:** Playback credentials are required to play encrypted videos. You can call the API or SDK to obtain the playauth parameter required by different players. For more information, see [GetVideoPlayAuth](/intl.en-US/API Reference/Video playback/GetVideoPlayAuth.md).

    -   Web players \(HTML5 or Flash\): On the Video and Audio page, click Manage in the Actions column and click the Web Player Code tab. To embed a video player on your web page, you can integrate the web player code snipped on your webpage. For more information, see [Integration](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Integration.md).
    -   Mobile players \(iOS or Android\): You can integrate the SDK into your application. For more information about the Android player, see [Integration](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Android/Integration.md). For more information about the iOS player, see [Integration](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/Integration.md).
5.  Video streams management

    After the video is encrypted and transcoded, the video is marked as Encrypt in the playback information. For more information, see [PlayInfo](/intl.en-US/API Reference/Appendix/Basic data types.md). The video is also marked as **Alibaba Cloud Private Encryption** in the console to facilitate content management in multiple ways.

    ![Alibaba Cloud private encryption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0170401161/p183729.png)


## Solution enhancement

If end users want to download videos for offline playback, we recommend that you set Download Mode to Encrypted to protect your videos. For more information, see [Configure offline download](/intl.en-US/User Guide/Domain management/Configure offline download.md). This option uses a key to perform a secondary encryption on video files. After a video is downloaded, ApsaraVideo Player SDK decrypts the video that allows the video to be played only by the specified application. This way, the copyright of offline videos is protected.

