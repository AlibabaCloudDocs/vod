# Encrypt videos for playback

This topic shows you how to use ApsaraVideo Player SDK to encrypt videos for playback.

## Overview

ApsaraVideo VOD provides a complete set of security mechanisms to protect videos from hotlinking and illegal download or distribution. The following table describes the security mechanisms.

|Security mechanism|Security measure|Feature|Security level|Deployment complexity|
|------------------|----------------|-------|--------------|---------------------|
|Access control|Referer blacklist or whitelist and User-Agent blacklist or whitelist|The source is traced based on HTTP headers. However, HTTP headers are prone to forgery.|Low|Low. You only need to configure this measure on Alibaba Cloud.|
|IP address blacklist or whitelist|Access from specific IP addresses is rejected or allowed. This measure is not applicable to scenarios where content needs to be delivered to a large number of consumers.|Relatively low|Low. You only need to configure this measure on Alibaba Cloud.|
|Maximum number of visits to a URL and maximum number of unique IP addresses|Access limits are set. This measure is not applicable to scenarios where widespread content delivery is required. In addition, this measure cannot identify legitimate access.|Relatively low|Low. You only need to configure this measure on Alibaba Cloud.|
|URL signing by ApsaraVideo VOD|URL signing and custom URL validity period|Signed URLs that dynamically change are generated. You can customize the validity period of signed URLs.|Medium|Relatively low. You can obtain signed URLs by calling API operations or based on the key.|
|Reauthentication by the customer|Pass-through of business requests to the custom authentication center of the customer for validity check|The customer knows its users better: The customer adds custom business request information and uses its own authentication center to accurately identify valid requests.|Relatively high|Relatively high. You must deploy an authentication center and ensure its high availability.|
|Video encryption|Alibaba Cloud video encryption \(proprietary cryptography\)|A cloud-device integrated video encryption solution that uses the proprietary cryptography algorithm is provided to ensure the security of transmission links.|High|Relatively low. You only need to perform simple configuration and integrate ApsaraVideo Player.|
|HTTP Live Streaming \(HLS\) encryption|AES-128 is used to encrypt video content. HLS encryption applies to all HLS-compatible players. However, the keys are prone to theft.|Relatively high|High. You must deploy the key management and token issuance services, and ensure the security of transmission links.|
|Commercial digital rights management \(DRM\)|The following DRM technologies are supported:-   China DRM
-   Microsoft PlayReady
-   Apple FairPlay
-   Google Widevine
-   Marlin

ApsaraVideo VOD provides native support for the preceding DRM technologies to ensure security.|High|High. You must purchase separate licenses and integrate specific SDKs.|

## Referer-based access control

You can use the Referer mechanism that is supported by HTTP to trace and identify the source. You can configure a Referer blacklist or whitelist \(but not both\) to control access to video resources.

-   The Alibaba Cloud Management Console allows you to configure a Referer blacklist or whitelist. After a visitor initiates a resource access request, the request is sent to a Content Delivery Network \(CDN\) node. Then, the CDN node checks the Referer header in the request based on the preconfigured Referer blacklist or whitelist. If the Referer header is allowed, the CDN node allows the access. If the Referer header is forbidden, the CDN node rejects the request and returns HTTP response code 403.
-   After you configure a Referer blacklist or whitelist, wildcard domain names are automatically supported. For example, if you enter a.com, the actual configuration \*.a.com takes effect. This means that all sub-domain names take effect.
-   Generally, mobile terminals cannot obtain the Referer header. By default, access requests without the Referer header are allowed. You can disable the access from such requests as required.

The following figure shows how to configure the Referer blacklist or whitelist in the Alibaba Cloud Management Console.

![Console](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2855160161/p184091.png)

## Referer settings by using ApsaraVideo Player SDK

You can configure the Referer whitelist by using ApsaraVideo Player SDK. For example, you can add aliyun.com to the whitelist in the console.

-   For Android devices, use the following sample code:

    ```
    AliPlayer player = AliPlayerFactory.createAliPlayer(context);
    ....
    // Obtain the parameters of the player.
    PlayerConfig config = player.getConfig();
    // Set the referer. Note that you must add the http(s):// protocol header.
    config.mReferrer = "http://aliyun.com";
    // Configure the settings for the player.
    player.setConfig(config);
    ```

-   For iOS devices, use the following sample code:

    ```
    // Obtain the parameters of the player.
    AVPConfig* config = [self.player getConfig];
    // Set the referer. Note that you must add the http(s):// protocol header.
    config.referer = @"http://aliyun.com";
    // Configure the settings for the player.
    [self.player setConfig:config];
    [self.player setStsSource:self.stsSource];
    [self.player prepare];
    ```


## Encrypted playback

Hotlink protection effectively protects users' legitimate access. However, after a user pays for a video, the user can download the video file from the legitimate playback URL with hotlink protection. Then, the user can distribute the video file to other users. Therefore, hotlink protection is far from enough to protect video copyrights. The leakage of video files may cause serious economic losses to customers that charge users for watching videos.

Alibaba Cloud video encryption service encrypts video data. Video files that are downloaded to an on-premises device are encrypted, preventing unauthorized redistribution. This effectively prevents video leakage and hotlinking.

-   Alibaba Cloud proprietary cryptography

    Alibaba Cloud video encryption uses the proprietary cryptography algorithm and secure transmission mechanism to provide a cloud-device integrated video security solution. Alibaba Cloud video encryption consists of **encrypted transcoding** and **decryption and playback**.

    -   Benefits

        -   Each media file has a dedicated encryption key. This reduces the risk of leaking a large number of video files when a unified key that is used for video files is disclosed.
        -   ApsaraVideo VOD provides an envelope encryption system that uses ciphertext and plaintext keys. Only the ciphertext keys are stored. The plaintext keys are used in the memory and are immediately destroyed after use.
        -   ApsaraVideo VOD provides secure ApsaraVideo Player SDKs for multiple platforms, such as iOS and Android. ApsaraVideo Player SDKs automatically decrypt and play encrypted videos.
        -   The proprietary cryptography protocol is used to transmit ciphertext keys between players and the cloud. The plaintext keys are not transmitted. This effectively prevents the keys from being intercepted.
        -   ApsaraVideo VOD provides the secure download feature. Videos that are cached on on-premises devices are encrypted again. This allows videos to be played offline and prevents videos from being copied.
        **Note:** Videos that are encrypted by using Alibaba Cloud video encryption are exported only in the HLS format, and can be played only by ApsaraVideo Player. For more information, see [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md).

    -   Use of proprietary cryptography

        ApsaraVideo Player SDK integrates the logic of player decryption and the logic of client-server interaction. Compared with common playback, Alibaba Cloud encrypted playback requires no extra attribute settings or cost. You only need to integrate ApsaraVideo Player SDK to implement video ID-based playback, and configure encrypted transcoding.

-   HLS encryption

    HLS encryption supports common encryption solutions that are specified in HLS. HLS encryption uses AES-128 to encrypt the video content and supports all HLS-compatible players. You can use your self-developed player or an open source player to play videos that are encrypted in HLS encryption mode. Compared with Alibaba Cloud video encryption, HLS encryption is more flexible but is difficult to use and less secure.

    1.  You must deploy the key management service to generate keys for encrypting videos during transcoding and obtain decryption keys during playback. You can also encapsulate Alibaba Cloud Key Management Service \(KMS\) as the key management service.
    2.  You must deploy the token issuance service to verify players and prevent unauthorized access to decryption keys.
    3.  The plaintext keys are transmitted between players and the cloud and may be intercepted. For more information, see [HLS standard encryption](/intl.en-US/Developer Guide/Video encryption/HLS standard encryption.md).
-   Use of HLS encryption

    ApsaraVideo Player supports transmission of the user token. Alibaba Cloud CDN dynamically modifies the decryption URI in the .m3u8 file. The decryption URI contains the user token. Then, you can verify the user token. For example, you can verify the validity of the key.

-   Set the HlsUriToken parameter by using STS
    -   For Android devices, use VidSts to set the playConfig parameter, which includes the mtsHlsUriToken parameter. Example:

        ```
        VidSts vidsts = new VidSts();
        VidPlayerConfigGen playerConfig = new VidPlayerConfigGen();
        // Set the user token.
        playerConfig.setMtsHlsUriToken("User token");
        vidsts.setPlayConfig(playerConfig);
        ```

    -   For iOS devices, use AVPVidStsSource to set the playConfig parameter, which includes the mtsHlsUriToken parameter. Example:

        ```
        - (instancetype)initWithVid:(NSString *)vid
                        accessKeyId:(NSString *)accessKeyId
                    accessKeySecret:(NSString *)accessKeySecret
                      securityToken:(NSString *)securityToken
                             region:(NSString *)region
                        playConfig:(NSString *)playConfig;
        - (void)setStsSource:(AVPVidStsSource*)source;
        ```

    -   Generate the playConfig parameter

        ApsaraVideo Player SDK provides the VidPlayerConfigGenerator class, in which the setHlsUriToken parameter is used to set the token. Then, you can call the generatePlayerConfig operation to generate the playConfig parameter. Example:

        ```
        -(void) setHlsUriToken:(NSString*)MtsHlsUriToken;
        -(NSString*) generatePlayerConfig;
        ```


## Set the HlsUriToken parameter by using PlayAuth

-   For Android devices, use VidAuth to set the playConfig parameter, which includes the mtsHlsUriToken parameter. Example:

    ```
    VidAuth vidauth = new VidAuth();
    VidPlayerConfigGen playerConfig = new VidPlayerConfigGen();
    // Set the user token.
    playerConfig.setMtsHlsUriToken("User token");
    vidauth.setPlayConfig(playerConfig);
    ```

-   For iOS devices, use AVPVidAuthSource to set the playConfig parameter, which includes the mtsHlsUriToken parameter. Example:

    ```
    - (instancetype)initWithVid:(NSString *)vid
            playAuth:(NSString *)playAuth
              region:(NSString *)region
              playConfig:(NSString *)playConfig;
    - (void)setAuthSource:(AVPVidAuthSource*)source;
    ```

-   Generate the playConfig parameter

    ApsaraVideo Player SDK provides the VidPlayerConfigGenerator class, in which the setHlsUriToken parameter is used to set the token. Then, you can call the generatePlayerConfig operation to generate the playConfig parameter. Example:

    ```
    -(void) setHlsUriToken:(NSString*)MtsHlsUriToken;
    -(NSString*) generatePlayerConfig;
    ```


## Set the HlsUriToken parameter by using MPS

-   For Android devices, after you create a VidMps object, you can call the setHlsUriToken method to set the HlsUriToken parameter, which is then passed to the player. Example:

    ```
    VidMps vidmps = new VidMps();
    // Set the user token.
    vidmps.setHlsUriToken("User token");
    ... // Set other parameters of the VidMps object.
    
    AliPlayer player = AliPlayerFactory.createAliPlayer(context);
    // Set the VidMps object in the player.
    player.setDataSource(vidmps);
    ... // Set other parameters of the player.
    ```

-   For iOS devices, use AVPVidMpsSource to set the mtsHlsUriToken parameter. Example:

    ```
    - (instancetype)initWithVid:(NSString*)vid
                     accId:(NSString *)accId
                 accSecret:(NSString*)accSecret
                  stsToken:(NSString*)stsToken
                  authInfo:(NSString*)authInfo
                    region:(NSString*)region
                playDomain:(NSString*)playDomain
            mtsHlsUriToken:(NSString*)mtsHlsUriToken;
    - (void)setMpsSource:(AVPVidMpsSource*)source;
    ```


