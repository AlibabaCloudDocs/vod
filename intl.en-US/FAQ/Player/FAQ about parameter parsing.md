# FAQ about parameter parsing

## What is a video ID? Why is a video ID required? How can I obtain a video ID?

A video ID is the ID of a video that is uploaded to ApsaraVideo VOD. For security reasons, ApsaraVideo VOD provides you with video IDs instead of video URLs. For more information about how to obtain a video URL, see [GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md).

After you upload a video to ApsaraVideo VOD, you can obtain a video ID. You can view the video IDs in the video list in the ApsaraVideo VOD console. You can use the video IDs to test the download and playback features. For more information about how to upload videos to ApsaraVideo VOD, see [Overview](/intl.en-US/Upload SDK/Overview.md).

## What are an AccessKey ID and an AccessKey secret? How can I obtain an AccessKey ID and an AccessKey secret?

The AccessKey ID and AccessKey secret are the only credentials that you can use to call Alibaba Cloud APIs. The AccessKey ID is used to identify you as a user. The AccessKey secret is used to encrypt the signature string of your access request. This can prevent data from being tampered with. The AccessKey secret is similar to a logon password. Keep the AccessKey secret confidential.

Perform the following steps to obtain the AccessKey ID and AccessKey secret:

1.  Log on to the Alibaba Cloud International site \(alibabacloud.com\).
2.  Click Console in the top navigation bar.
3.  Move the pointer over the profile picture in the upper-right corner and select AccessKey Management.
4.  In the Note message, click Use Current AccessKey Pair. The AccessKey ID and AccessKey secret are displayed.

## What is a playKey? How can I obtain a playKey?

A playKey is an API key. It is used for authentication when ApsaraVideo Player SDK obtains the streaming URL of a video. Playback authentication is a secondary authentication mechanism that is implemented by ApsaraVideo VOD based on Alibaba Cloud AccessKey authentication. The playKey effectively prevents hotlinking. By default, ApsaraVideo VOD provides playKeys for Flash, HTML5, iOS, and Android to meet your video playback needs.

**Note:** To ensure security, if you want to view your playKey, you must enter the verification code that is sent to your mobile phone.

Perform the following steps to obtain the playKey:

1.  Log on to the Alibaba Cloud International site \(alibabacloud.com\).
2.  Click Console in the top navigation bar.
3.  Move the pointer over the icon in the upper-left corner and click Products and Services.
4.  Select ApsaraVideo VOD.
5.  In the ApsaraVideo VOD console, choose Configuration Management \> CDN Configuration \> Download in the left-side navigation pane. On the Download page, turn on Download. In the Turn on the download function dialog box, select Encrypted.
6.  In the Get the key section, set the Unique App Identifier and Private Key parameters.
7.  Click Generate and Download Key.

## What is a playAuth? How can I obtain a playAuth?

ApsaraVideo Player plays videos in three modes that apply to different scenarios. Among them, the setAuthInfo method is the most secure mode, in which a playAuth is provided.

|Playback mode|Scenario|Advantages and disadvantages|Recommended|
|-------------|--------|----------------------------|-----------|
|setDataSource|This mode is used for testing.|Risky. You must fix your AccessKey pair to your client. If the client is cracked, your AccessKey pair may be leaked.|Not recommended for commercial use.|
|setAuthInfo|This mode is available for commercial use.|Secure. All video URLs and links are not exposed.|Recommended for commercial use.|
|Playback of on-premises videos and online videos|In this mode, on-premises videos can be played and videos can be played based on video URLs.|Simple. Videos on other platforms can be played.|Used for playing on-premises videos and online videos.|

A playAuth is a playback credential in which the video ID, AccessKey ID, and AccessKey secret are packaged and encrypted. After you obtain the playAuth, you can obtain a string of data that contains various information for ApsaraVideo Player to play videos.

Procedure: The server obtains the playAuth, the server sends the playAuth to the client, and then the client plays the video.

1.  Obtain the playAuth: You can use the playback authentication SDK on the server to obtain the playAuth from ApsaraVideo VOD.
2.  Play a video: ApsaraVideo Player SDK obtains the streaming URL of the video from ApsaraVideo VOD based on the video ID and playAuth. Then, ApsaraVideo Player SDK loads and decodes the video stream, and plays the video.

**Note:** A playAuth is valid for 100 seconds. It is used only to obtain the streaming URL of the specified video and cannot be used for other videos or reused. If the playAuth expires, you cannot obtain the streaming URL. In this case, you must obtain the playAuth again. ApsaraVideo Player SDK automatically obtains the streaming URL for decoding and playback based on the playAuth. The streaming URL is valid for 30 minutes. If the streaming URL expires, obtain the playAuth again and send it to ApsaraVideo Player SDK to refresh the streaming URL. To ensure the security of your Alibaba Cloud account, we recommend that you use the AccessKey pair of a RAM user, especially when you use ApsaraVideo Player SDK for web.

