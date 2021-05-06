Overview 
=============================

ApsaraVideo VOD provides comprehensive protection over content security by delivering features such as access control, URL signing, content delivery network (CDN) reauthentication, video encryption, and secure download. You can use these features to meet your security requirements in different business scenarios. 

Overview 
-----------------------------

ApsaraVideo VOD provides comprehensive mechanisms to protect video content from hotlinking and illegal download or distribution. You can use ApsaraVideo VOD to protect the copyright of online videos in industries such as education, finance, industry training, and premium TV shows. 

The following table describes the security mechanisms that are provided by ApsaraVideo VOD.


|                              Security mechanism                              |                                                        Security method                                                         |                                                                                                             Characteristic                                                                                                              | Security level  |                                                           Threshold                                                            |
|------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|--------------------------------------------------------------------------------------------------------------------------------|
| [Access control](#section-kvj-w98-xpu)                       | Referer blacklist or whitelist                                                                                                 | This feature tracks sources based on HTTP headers, which are prone to forgery.                                                                                                                                                          | Low             | Low. Only configurations in the cloud are required.                                                                            |
| [Access control](#section-kvj-w98-xpu)                       | User-Agent blacklist or whitelist                                                                                              | This feature tracks sources based on HTTP headers, which are prone to forgery.                                                                                                                                                          | Low             | Low. Only configurations in the cloud are required.                                                                            |
| [Access control](#section-kvj-w98-xpu)                       | IP address blacklist or whitelist                                                                                              | This feature rejects or allows access only from specified IP addresses. This feature is unsuitable for the distribution of content to a large number of consumers.                                                                      | Relatively low  | Low. Only configurations in the cloud are required.                                                                            |
| [Access control](#section-kvj-w98-xpu)                       | Limits on the number of access times and the number of unique IP addresses                                                     | This feature sets access limits. This feature is unsuitable for the distribution of content to a large number of consumers. In addition, illegal access may occur even when the limit on threshold values is not exceeded.              | Relatively low  | Low. Only configurations in the cloud are required.                                                                            |
| [URL signing by ApsaraVideo VOD](#section-rwn-udf-1na)       | URL signing                                                                                                                    | This feature generates signed URLs that dynamically change. You can customize the validity period of signed URLs.                                                                                                                       | Medium          | Relatively low. Signed URLs are obtained by calling API operations or automatically generated based on the key.                |
| [CDN reauthentication by the customer](#section-iwq-rbj-l48) | ApsaraVideo Live passes through business requests to the authentication center of a customer for authentication.               | The customer can add custom information to the requests and use their own authentication center to verify requests.                                                                                                                     | Relatively high | Relatively high. You must deploy an authentication center and ensure its high availability.                                    |
| [Video encryption](#section-h1i-ytf-tam)                     | Alibaba Cloud proprietary cryptography                                                                                         | ApsaraVideo VOD provides a cloud-device integrated solution to encrypt videos. The solution uses a proprietary encryption algorithm to ensure the security of transmission links.                                                       | High            | Relatively low. You need only to perform simple configurations and integrate ApsaraVideo Player SDK.                           |
| [Video encryption](#section-h1i-ytf-tam)                     | HTTP-Live-Streaming (HLS) encryption                                                                                           | HLS encryption uses AES-128 to encrypt video content. This applies to all HLS players. However, the keys are prone to theft.                                                                                                            | Relatively high | High. You must construct a key management service and a token issuance service, and ensure the security of transmission links. |
| [Video encryption](#section-h1i-ytf-tam)                     | Commercial digital rights management (DRM)                                                                                     | Many platforms, such as Apple FairPlay and Google Widevine, provide native support for commercial DRM. Commercial DRM provides high security and meets the requirements of large copyrighted content providers.                         | High            | High. You are charged based on the number of license calls. You need only to integrate ApsaraVideo Player SDK.                 |
| [Secure download and caching](#section-x3i-rmm-yy3)          | A private key is used to perform a secondary encryption on a downloaded video file, which can be decrypted and played offline. | Multiple mechanisms are used to ensure that a video can be decrypted and played offline only on the specified application. Each video has an independent private key. The private key file is stored after encryption to prevent theft. | High            | Relatively low. You need only to perform simple configurations and integrate ApsaraVideo Player SDK.                           |



Access control 
-----------------------------------

**Introduction:** Access policies are configured on the cloud to provide basic protection for video resources. 

The following common access control policies are provided:

* Referer

  You can use the Referer header in HTTP requests to track and identify where the requests come from. You can configure a referer blacklist or whitelist to manage access to video resources.
  

* User-Agent

  You can use the User-Agent header in HTTP requests to track and identify where the requests come from. You can configure a User-Agent blacklist or whitelist to manage access to video resources.
  

* IP address

  You can configure an IP address blacklist or whitelist by using the X-Forwarded-For header or actual IP addresses of users to manage access to video resources. You can configure the IP address blacklist or whitelist by using an IP address list or a subnet mask.
  

* Limits on the number of access times

  You can configure the maximum number of times that a video URL can be accessed in a specific period and the maximum number of unique IP addresses that are granted access to the video URL.
  




For more information, see [Access control](/intl.en-US/Developer Guide/Video security/Access control.md).

URL signing by ApsaraVideo VOD 
---------------------------------------------------

**Background:** If fixed streaming URLs are used, unauthorized video distribution may occur and cannot be controlled. 

**Introduction:** ApsaraVideo VOD provides the URL signing feature. This feature generates dynamic signed URLs that contain information such as the permission verification and validity period to distinguish legal requests and protect video resources. 

After URL signing is enabled:

* The URLs of all media resources, including videos, audio, thumbnails, and snapshots, must be signed.

  

* ApsaraVideo Player SDKs and the API or SDKs for obtaining streaming URLs automatically generate streaming URLs with a validity period. For more information about how to manually generate a dynamic signed URL, see the "`Authentication method`" section of the [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md) topic.

  




For more information, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md).

CDN reauthentication by the customer 
---------------------------------------------------------

**Background:** The URL signing by ApsaraVideo VOD cannot detect all illegal requests such as hotlinking requests. CDN reauthentication allows customers to authenticate business requests and makes the authentication more accurate. 

**Introduction:** In CDN reauthentication mode, CDN passes through user requests to your authentication center for you to determine whether the requests are legal. CDN allows or rejects the requests based on your judgment. 

* To implement CDN reauthentication, you must develop and deploy an authentication center. If the domain name of the authentication center is accelerated in CDN, CDN can cache the authentication results based on specific rules. This reduces the workloads on your authentication center.

  

* By default, CDN passes through the headers and request_uri fields in user requests to your authentication center and performs operations based on the authentication results that are returned by the authentication center.

  

* You can use CDN to verify requests. If you hide the logon cookie or universally unique identifier (UUID) of a user in a playback request and pass through the playback request, CDN can verify the request. This way, you can determine whether the user is a legal user.

  



**Note**

You must develop and deploy your own authentication center to use CDN reauthentication. If you want to use CDN reauthentication, submit a ticket or contact ApsaraVideo VOD after-sales to enable and configure CDN reauthentication.

Video encryption 
-------------------------------------

**Background:** The hotlink protection mechanism protects access to your content. However, in the paid video scenario, users can pay a one-time fee for a video and download the video file from the legitimate streaming URL for which hotlink protection is configured. After the video is downloaded, distribution of the video is uncontrollable. Therefore, hotlink protection is far from enough to protect video copyrights. The leakage of video files may cause serious economic losses to customers that charge users for watching videos. 

**Introduction:** Alibaba Cloud proprietary cryptography encrypts video data. The video files that are downloaded to on-premises devices are encrypted. This prevents unauthorized redistribution and video leakage and hotlinking. 

* Alibaba Cloud proprietary cryptography

  Alibaba Cloud proprietary cryptography uses the proprietary cryptography algorithm and secure transmission mechanism to provide a cloud-device integrated solution to secure video security. Alibaba Cloud proprietary cryptography consists of **encrypted transcoding** and **playback after decryption** . 

  Benefits:
  * Each media file has a dedicated encryption key. This reduces the risk of leaking a large number of video files when a unified key that is used for video files is disclosed.

    
  
  * ApsaraVideo VOD provides an envelope encryption system by using **ciphertext and plaintext keys** . Only the ciphertext keys are stored. The plaintext keys are used in the memory and are immediately destroyed after use.

    
  
  * ApsaraVideo VOD provides secure ApsaraVideo Player SDKs for multiple platforms, including iOS, Android, HTML5, and Flash. ApsaraVideo Player SDKs can automatically decrypt and play encrypted videos.

    
  
  * The proprietary cryptography protocol is used to transmit ciphertext keys between players and the cloud. The plaintext keys are not transmitted. This effectively prevents the keys from being intercepted.

    
  
  * ApsaraVideo VOD provides the secure download feature. The videos that are cached on on-premises devices are encrypted again. This allows videos to be played offline and prevents videos from being copied.

    
  

  
  **Notice**

  Videos that are encrypted by using Alibaba Cloud proprietary cryptography have the following limits:
  * The videos can be exported only in the HLS format.

    
  
  * The videos can be played only by ApsaraVideo Player.

    
  
  * The videos cannot be played on web pages in the iOS system.

    
  

  

  For more information, see [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md).
  

* HLS encryption

  HLS encryption supports the common encryption scheme that is specified in [HLS](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23). HLS encryption uses AES-128 to encrypt the video content and supports all HLS-compatible players. You can use your custom player or an open source player to play the videos that are encrypted in HLS encryption mode. Compared with Alibaba Cloud proprietary cryptography, HLS encryption is more flexible but is difficult to use and less secure. 
  * You must construct a key management service to generate keys to encrypt videos during transcoding and obtain decryption keys during playback. You can also use [Key Management Service (KMS)](https://www.aliyun.com/product/kms) of Alibaba Cloud to encapsulate keys.

    
  
  * In addition, you must construct a token issuance service to verify players and prevent unauthorized access to decryption keys.

    
  
  * The plaintext keys are transmitted between players and the cloud and are prone to interception.

    
  

  

  For more information, see [HLS Encryption](/intl.en-US/Developer Guide/Video security/HLS Encryption.md).
  

* Commercial DRM

  High-end video programs must meet the security requirements of content providers, such as Hollywood and Warner. ApsaraVideo VOD provides a cloud-based DRM solution that supports FairPlay and Widevine DRM encryption. This solution integrates the video encryption, license issuance, and video playback features. 

  For more information, see [Introduction](/intl.en-US/User Guide/DRM Management/Introduction.md).
  



**Note**

Each video encryption solution has advantages and disadvantages. In general, a more standard and universal solution provides higher flexibility but lower security. Select a solution based on your business scenario.

**Feature comparison:** 

* Security level: commercial DRM \> Alibaba Cloud proprietary cryptography \> HLS encryption 

  The security level of Alibaba Cloud proprietary cryptography is approximately equal to that of commercial DRM. The security levels of Alibaba Cloud proprietary cryptography and commercial DRM are significantly higher than that of HLS encryption.
  

* Ease of use: commercial DRM = Alibaba Cloud proprietary cryptography \> HLS encryption 

  * Alibaba Cloud proprietary cryptography provides a cloud-device integrated solution that allows you to seamlessly integrate the encryption capability by using simple configurations and ApsaraVideo Player SDKs.

    
  
  * To use HLS Encryption, you must construct a KMS service and a token issuance service.

    
  
  * To use commercial DRM, you must purchase a license and integrate a specific SDK.

    
  

  

* Universality: HLS encryption \> commercial DRM \> Alibaba Cloud proprietary cryptography 

  * HLS encryption supports all HLS-compatible players.

    
  
  * Commercial DRM supports only authorized platforms such as the Google Chrome, Safari, Internet Explorer, and Microsoft Edge browsers and the Android and iOS operating systems.

    
  
  * Alibaba Cloud proprietary cryptography supports ApsaraVideo Player only for Android, iOS, HTML5, and Flash.

    
  

  

* Cost: Alibaba Cloud proprietary cryptography = HLS encryption \< commercial DRM 

  Both Alibaba Cloud proprietary cryptography and HLS encryption are free of charge. Commercial DRM requires additional license fees.
  




Secure download and caching 
------------------------------------------------

**Background:** Video applications, especially those for mobile devices on Android and iOS, must cache videos on or download videos to on-premises devices. The videos that are stored on on-premises devices must be protected from unauthorized playback or redistribution. The secure download feature provided by ApsaraVideo Player can protect the videos that are downloaded to on-premises devices. 

**Introduction:** Secure download is a process where secondary encryption is performed on a video by using a private key. After the video is downloaded, it is decrypted in ApsaraVideo Player SDKs. This ensures that the offline video can be played only by the application with the bundle ID or keystore that is specified in secure download settings. 

Benefits:

* After a video is downloaded, it can be decrypted and played offline and can be played only by the specified application.

  

* The private key file is stored after encryption to prevent theft.

  

* Each video file has an independent private key on each application. When the private key of a single video is disclosed, other videos are not affected.

  




To use this feature, enable encrypted download in the ApsaraVideo VOD console. For more information, see [Configure offline download](/intl.en-US/User Guide/Domain management/Configure offline download.md). Only [ApsaraVideo Player for Android](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Android/Implementation.md)and [ApsaraVideo Player for iOS](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/Implementation.md) support the secure download feature.
