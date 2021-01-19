Use playback credentials to play videos 
============================================================

ApsaraVideo Player SDK can automatically obtain playback URLs based on playback credentials. This method is easy to use and makes the playback more secure. You can obtain playback credentials by calling the API operations and use the player SDK to play the video. This topic describes the playback process, instructions, and usage notes of a playback credential.

Playback process 
-------------------------------------

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3310401161/p178264.jpg)

Usage notes 
--------------------------------

* By default, a playback credential is valid for 100 seconds and up to 3,000 seconds. You can use the playback credential to obtain the playback URL for only the specified video. The playback credential cannot be reused or used to obtain the playback URL of a video other than the specified one. You cannot obtain the playback URL of a video by using a credential that has expired. A new credential is required.

  

* When URL authentication is enabled, the validity period of a playback credential is different from the validity period of a playback URL. The validity period of a playback URL can be configured without an upper limit.

  

* A playback credential (PlayAuth) is not a playback URL. ApsaraVideo Player SDK can automatically obtain playback URLs based on the playback credential to play the video. However, you must obtain a new credential after the existing credential expires.

  

* If videos are encrypted in [Alibaba Cloud video encryption](/intl.en-US/Developer Guide/Video security/Alibaba Cloud video encryption.md) mode, only ApsaraVideo Player SDK can play the videos.

  




Obtain the playback credential 
---------------------------------------------------

You can call the [GetVideoPlayAuth](/intl.en-US/API Reference/Video playback/GetVideoPlayAuth.md) operation to obtain the playback credential.

**Call methods:** 

* We recommend that you use a server SDK to obtain media asset information by calling the API operations. This method is simple and efficient. For more information, see [Usage notes](/intl.en-US/Server SDK Reference/Usage notes.md). For more information about API operations, see SDK examples for each API operation.

  

* For more information about how to generate HTTP or HTTPS requests, see [Common parameters](/intl.en-US/API Reference/Calling methods/Common parameters.md) and [Examples](/intl.en-US/API Reference/Calling methods/Call Examples.md).

  




Use ApsaraVideo Player SDK to play a video 
---------------------------------------------------------------

ApsaraVideo Player SDKs for Web, Android, and iOS are provided. These SDKs can use a playback credential to automatically obtain the playback URL to play the video. For more information, see the following topics.

* Web (HTML5 or Flash): [Overview](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for web/Overview.md)

  

* Android: [Feature](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Android/Features and usage.md)

  

* iOS: [Feature](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/Features and usage.md)

  



**Notice**

A playback credential has a validity period. You cannot obtain the playback URL of a video by using a credential that has expired. A new credential is required.
