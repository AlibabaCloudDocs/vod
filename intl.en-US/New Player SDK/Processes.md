# Processes

This topic describes the processes that are involved when you use ApsaraVideo Player SDK, including the basic playback process, STS-based playback process, PlayAuth-based playback process, and secure download process.

## Basic playback process

ApsaraVideo Player SDK provides various features of ApsaraVideo VOD and ApsaraVideo Live. For more information, see [Overview](/intl.en-US/New Player SDK/Overview.md).

1.  Obtain a video ID or streaming URL by using ApsaraVideo VOD or ApsaraVideo Live.
2.  Integrate the ApsaraVideo Player SDK framework. For more information, see [Integration of ApsaraVideo Player SDK for iOS](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for iOS/Integration.md) and [Integration of ApsaraVideo Player SDK for Android](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Android/Integration.md).
3.  Play a VOD program based on the video ID and Security Token Service \(STS\) token or play a live streaming program based on the streaming URL.

## STS-based playback process

1.  Your application requests an STS token.
2.  The AppServer delivers an STS token.
3.  You upload a video and obtain a video ID.
4.  The AppServer obtains the STS token.
5.  The AppServer delivers the STS token to the client.
6.  The video is played.

**Note:** The AppServer is the server of your application. You can use the server API or SDK to develop your own AppServer.

## PlayAuth-based playback process

1.  Your application requests an upload credential.
2.  The AppServer delivers an upload credential.
3.  You upload a video and obtain a video ID.
4.  The AppServer obtains a playback credential.
5.  The AppServer delivers the playback credential to the client.
6.  The video is played.

**Note:** The AppServer is the server of your application. You can use the server API or SDK to develop your own AppServer.

## Secure download process

1.  Log on to the [ApsaraVideo VOD console](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F%3Fspm%3D5176.8413026.J_2349663800.2.3dc011cfeVYJhB#/overview).
2.  Click Modify next to **Download Settings** and select Encrypted for the **Download Mode** parameter.
3.  Enter the bundle ID of the application or the SHA1 signature of the keystore.
4.  Generate and download the private key file for encryption.
5.  Integrate the private key file into the SDK and call the `setEncrptyFile or setSecretImagePath` method to set a path for the private key file. For more information, see [Obtain the security file](/intl.en-US/FAQ/Player/Obtain the security file.md).

**Note:** If you select the secure download mode, you must download a private key file from the [ApsaraVideo VOD console](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F%3Fspm%3D5176.8413026.J_2349663800.2.3dc011cfeVYJhB#/overview) and integrate the file into the SDK. This way, both encrypted and unencrypted streaming videos are locally saved as encrypted videos. If you select the normal download mode, both encrypted and unencrypted streaming videos are locally saved as unencrypted videos that can be played by various players.

