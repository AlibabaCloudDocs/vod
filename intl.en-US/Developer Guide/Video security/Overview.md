Overview 
=============================

ApsaraVideo VOD provides a comprehensive content security protection mechanism to meet the security requirements in different business scenarios such as access control, URL authentication, CDN reauthentication, video encryption, and secure download.

Overview 
-----------------------------

ApsaraVideo VOD provides a complete secure playback mechanism to protect video content from hotlinking and illegal download or distribution. You can use ApsaraVideo VOD to protect the copyright of online videos in industries such as education, finance, industry training, and premium TV shows.

Apsaravideo VOD provides the following security mechanisms:


|                              Security mechanism                               |                                                        Security method                                                        |                                                                                                           Characteristic                                                                                                            | Security level  |                                                           Threshold                                                            |
|-------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|--------------------------------------------------------------------------------------------------------------------------------|
| [Access control](#section-kvj-w98-xpu)                        | Referer blacklist or whitelist                                                                                                | This feature tracks sources based on HTTP headers, which are prone to forgery.                                                                                                                                                      | Low             | Low. Only configurations on the cloud are required.                                                                            |
| [Access control](#section-kvj-w98-xpu)                        | User-Agent blacklist or whitelist                                                                                             | This feature tracks sources based on HTTP headers, which are prone to forgery.                                                                                                                                                      | Low             | Low. Only configurations on the cloud are required.                                                                            |
| [Access control](#section-kvj-w98-xpu)                        | IP address blacklist or whitelist                                                                                             | This feature rejects or allows access only from specified IP addresses. This feature is unsuitable for the distribution of content to a large number of consumers.                                                                  | Relatively low  | Low. Only configurations on the cloud are required.                                                                            |
| [Access control](#section-kvj-w98-xpu)                        | Limits on the number of access times and the number of unique IP addresses                                                    | This feature sets access limits. This feature is unsuitable for the distribution of content to a large number of consumers. Additionally, illegal access may occur even when the limit on threshold values are not exceeded.        | Relatively low  | Low. Only configurations on the cloud are required.                                                                            |
| [URL authentication by ApsaraVideo VOD](#section-rwn-udf-1na) | URL authentication                                                                                                            | This measure generates signed URLs that dynamically change. You can customize the validity period of signed URLs.                                                                                                                   | Medium          | Relatively low. Signed URLs are obtained by calling the API operations or automatically generated based on the key.            |
| [CDN reauthentication by the customer](#section-iwq-rbj-l48)  | CDN transparently transmits user requests to authentication centers of customers to determine whether the requests are legal  | You can add custom business request information and use their own authentication centers to verify requests.                                                                                                                        | Relatively high | Relatively high. You must deploy their own authentication centers and ensure high availability of the authentication centers.  |
| [Video encryption](#section-h1i-ytf-tam)                      | Alibaba Cloud video encryption (private encryption)                                                                           | ApsaraVideo VOD provides a cloud-device integrated the solution to encrypt video. The solution uses a proprietary encryption algorithm to ensure the security of transmission links.                                                | High            | Relatively low. You need only to perform simple configurations and integrate ApsaraVideo Player SDK.                           |
| [Video encryption](#section-h1i-ytf-tam)                      | HLS Encryption                                                                                                                | Http-Live-Streaming (HLS) Encryption uses AES-128 to encrypt video content. This applies to all HLS players. However, the keys are prone to theft.                                                                                  | Relatively high | High. You must construct a key management service and a token issuance service, and ensure the security of transmission links. |
| [Video encryption](#section-h1i-ytf-tam)                      | Commercial DRM                                                                                                                | Many platforms such as Microsoft PlayReady, Apple FairPlay, and Google Widevine provide native support for commercial DRM. Commercial DRM provides high security and meets the requirements of large copyrighted content providers. | High            | High. You must purchase a separate license and integrate a specified SDK.                                                      |
| [Secure download (caching)](#section-x3i-rmm-yy3)             | A private key is used to perform a secondary encryption on a downloaded video file, which can be decrypted and played offline | Multiple mechanisms are used to ensure that a video can be played only by the specified application. Each video has an independent private key. The private key file is stored after encryption to prevent theft.                   | High            | Relatively low. You need only to perform simple configurations and integrate ApsaraVideo Player SDK.                           |



Access control 
-----------------------------------

**Introduction:** describes access policies in the cloud to provide basic protection for video resources.

The following common access control policies are provided:

* Referer

  You can use the Referer header in HTTP requests to track and identify where requests come from. You can configure a Referer blacklist or whitelist to control access to video resources. You cannot use a Referer blacklist and whitelist for a video resource at the same time.
  

* User-Agent

  You can configure a User-Agent blacklist or whitelist by using the HTTP User-Agent header to control access to video resources.
  

* IP address

  You can configure an IP address blacklist or whitelist by using the HTTP X-Forwarded-For header or actual IP addresses of users to control access to video resources. You can configure the IP address blacklist or whitelist by using an IP address list or a subnet mask.
  

* Limits on the number of access times

  You can configure the maximum number of times that a video URL can be accessed in a specific period and the maximum number of unique IP addresses that are granted access to the video URL after deduplication.
  




For more information, see [Access control](/intl.en-US/Developer Guide/Video security/Access control.md).

URL authentication by ApsaraVideo VOD 
----------------------------------------------------------

**Background:** If fixed playback URLs are used, unauthorized video distribution may occur and cannot be controlled.

**Introduction:** ApsaraVideo VOD provides the URL authentication feature. This feature generates dynamic and signed URLs that contain information such as the permission verification and validity period to distinguish legal requests and protect video resources.

After URL authentication is enabled:

* The URLs of all media resources, which include videos, audio, thumbnails, and snapshots, must be signed.

  

* ApsaraVideo Player SDKs and the API or SDKs for obtaining playback URLs automatically generate playback URLs with a validity period. For more information about how to manually generate a dynamic authentication URL, see the "`Authentication method`" section of the [URL authentication](/intl.en-US/Developer Guide/Video security/URL signing.md) topic.

  




For more information, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL signing.md).

CDN reauthentication by the customer 
---------------------------------------------------------

**Background:** This authentication method cannot detect all illegal requests such as hotlinking requests. CDN reauthentication can introduce the business requests of customers and make the detection more accurate.

**Introduction:** In CDN reauthentication mode, CDN transparently transmits user requests to your authentication center whether the requests are legal. CDN allows or rejects the requests based on your judgment.

* To implement CDN reauthentication, you must develop and deploy an authentication center. If the domain name of the authentication center is accelerated in CDN, CDN can cache the authentication results based on specific rules. This reduces the pressure on your authentication center.

  

* By default, CDN transparently transmits the headers and request_uri fields in user requests to your authentication center and performs operations based on the authentication results returned by the authentication center.

  

* You can use CDN to verify requests. For example, if you hide the logon cookie or UUID of a user in a playback request and transparently transmits the playback request, CDN can verify the request. This way, you can determine whether the user is a legal user.

  



**Note**

You must develop and deploy your own authentication center to use CDN reauthentication. If you want to use CDN reauthentication, submit a ticket or contact ApsaraVideo VOD after-sales to enable and configure CDN reauthentication.

Video encryption 
-------------------------------------

**Background:** The hotlink protection mechanism can protect access to your content. However, in the paid video scenario, users can pay a one-time fee for a video and download the video file from the legitimate playback URL that has hotlink protection configured. After the video is downloaded, distribution of the video is uncontrollable. Therefore, the hotlink protection mechanism is insufficient to protect video copyrights. The leakage of video files can cause serious economic losses to businesses that charge users for watching videos.

**Introduction:** Alibaba Cloud video encryption service encrypts video data. Video files downloaded to a local device are encrypted, which prevents unauthorized redistribution. This prevents video leakage and hotlinking.

* Alibaba Cloud video encryption

  Alibaba Cloud proprietary cryptography uses a proprietary encryption algorithm and a secure transmission mechanism to provide a security solution for cloud-device integrated video. Alibaba Cloud video encryption contains two parts: **encryption and transcoding** and **decryption and playback** .

  Benefits:
  * Each media file has a dedicated encryption key. This prevents the leakage of a large number of video files if the key for a single file is leaked.

    
  
  * ApsaraVideo VOD provides an envelope encryption system by using **ciphertext and plaintext keys** . Only the ciphertext keys are stored. The plaintext keys are used only for processing in the memory but are not stored. They are immediately destroyed after use.

    
  
  * ApsaraVideo VOD provides secure ApsaraVideo Player SDKs for multiple platforms, including iOS, Android, HTML5, and Flash. ApsaraVideo Player SDKs can automatically decrypt and play encrypted videos.

    
  
  * The proprietary cryptography protocol is used to transmit ciphertext keys between players and the cloud. The plaintext keys are not transmitted. This can prevent the keys from being intercepted.

    
  
  * ApsaraVideo VOD provides the secure download feature. Videos cached locally are encrypted again. This allows videos to be played offline without being copied.

    
  

  
  **Notice**

  Alibaba Cloud video encryption has the following limits:
  * Only the HLS format is supported.

    
  
  * You can use only ApsaraVideo Player SDK.

    
  
  * Web pages do not support the playback in IOS.

    
  

  

  For more information, see [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md).
  

* HLS Encryption

  [HTTP-Live-Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) Encryption supports the common encryption scheme specified in HLS. HLS Encryption uses AES-128 to encrypt the video content and supports all HLS-compatible players. You can use your self-developed player or an open source player to play videos encrypted in HLS Encryption mode. Compared with Alibaba Cloud proprietary cryptography, HLS Encryption is relatively difficult to use and provides lower security.
  * You must construct a key management service (KMS) to generate keys to encrypt videos during transcoding and obtain decryption keys during playback. You can also encapsulate [Alibaba Cloud KMS](https://www.aliyun.com/product/kms).

    
  
  * In addition, you must construct a token issuance service to verify players and prevent unauthorized access to decryption keys.

    
  
  * The plaintext keys are transmitted between players and the cloud, which makes them prone to be intercepted.

    
  

  

  For more information, see [HLS Encryption](/intl.en-US/Developer Guide/Video security/Standard HLS encryption.md).
  

* Commercial DRM

  High-end video programs must meet the security requirements of content providers such as Hollywood. Alibaba ApsaraVideo cooperates with ChinaDRM, which has been certified by both National Radio and Television Administration (NRTA) of China and Hollywood, to launch the first cloud DRM solution in China. This solution will be commercially available.

  If you want to use this solution, contact your business manager, submit a ticket, or contact ApsaraVideo VOD after-sales.
  



**Note**

Each video encryption solution has advantages and disadvantages. In general, a more standard and universal solution provides higher flexibility but lower security. Select a solution based on your business scenario.

**Feature comparison:** 

* Security level: commercial DRM approximately equal to Alibaba Cloud video encryption greater than HLS Encryption

  The security level of Alibaba Cloud video encryption is approximately equal to that of commercial DRM. The security levels of both Alibaba Cloud video encryption and commercial DRM are significantly higher than that of HLS Encryption.
  

* Ease of use: Alibaba Cloud video encryption greater than HLS Encryption greater than commercial DRM

  * Alibaba Cloud video encryption provides a cloud-device integrated solution that allows you to seamlessly integrate the encryption capability by using simple configurations and ApsaraVideo Player SDKs.

    
  
  * To use HLS Encryption, you must construct a KMS service and a token issuance service.

    
  
  * To use commercial DRM, you must purchase a license and integrate a specific SDK.

    
  

  

* Universality: HLS Encryption greater than commercial DRM greater than Alibaba Cloud video encryption

  * HLS Encryption supports all HLS-compatible players.

    
  
  * Commercial DRM supports only authorized platforms such as the Google Chrome, Safari, Internet Explorer, and Microsoft Edge browsers and the Android and iOS operating systems.

    
  
  * Alibaba Cloud video encryption supports ApsaraVideo Player only for Android, iOS, HTML5, and Flash.

    
  

  

* Cost: Alibaba Cloud video encryption equal to HLS Encryption much smaller than commercial DRM 

  Both Alibaba Cloud video encryption and HLS Encryption are free of charge.
  




Commercial DRM requires additional license fees. 
---------------------------------------------------------------------

**Background:** Video applications, especially those for mobile devices such as Android and iOS, often must cache videos on or download videos to local devices. The videos stored locally must be protected from unauthorized playback or redistribution. The secure download feature provided by ApsaraVideo Player can protect the videos downloaded to local devices.

**Introduction:** Secure download is a process where asymmetric encryption is used to encrypt a video. After the video is downloaded, it is decrypted in ApsaraVideo Player SDKs. This ensures that the offline video can be played only by the application with the bundleID or keystore specified in secure download settings.

Benefits:

* After a video is downloaded, it can be decrypted and played offline and can be played only by the specified application.

  

* Each video has an independent private key. The private key file is stored after encryption to prevent theft.

  

* Each video file has an independent private key on each application. When the private key of a single video is disclosed, other videos are not affected.

  




To use this feature, configure download in the ApsaraVideo VOD console. For more information, see [Configure offline download](/intl.en-US/User Guide/Domain management/Configure offline download.md). Only [ApsaraVideo Player for Android](https://help.aliyun.com/document_detail/61910.html#h2-2-4-4) and [ApsaraVideo Player for iOS](https://help.aliyun.com/document_detail/61668.html#h2-2-4-4) support the secure download feature.
