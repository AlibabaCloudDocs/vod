# Overview

ApsaraVideo Player SDK is essential for streaming videos from ApsaraVideo to clients. This topic describes the features and scenarios of ApsaraVideo Player SDK. For example, ApsaraVideo Player SDK supports encrypted playback, secure download, resolution switching, and short video playback. These features provide you with simple, fast, secure, and stable video playback.

## Features

ApsaraVideo Player SDK provides a player framework to meet different user needs in different business scenarios. You can integrate ApsaraVideo Player SDK as needed. The following table describes the features of ApsaraVideo Player SDK.

|Feature|Description|
|-------|-----------|
|Format and codec|ApsaraVideo Player SDK supports video files in the MP4, M3U8, Flash Video \(FLV\), and Matroska Video \(MKV\) formats, and audio files in the MP3 format. ApsaraVideo Player SDK supports the H.264 and H.265 video codecs, and the Advanced Audio Coding \(AAC\) audio codec. ApsaraVideo Player SDK for iOS supports Audio Codec 3 \(AC3\).|
|Complete UI|ApsaraVideo Player SDK provides complete source code for multiple user interfaces \(UIs\). You can integrate the UI source code based on your application style.|
|Playback control|ApsaraVideo Player SDK supports multiple playback control features, such as start, stop, pause, resume, replay, and loop playback.|
|List playback|ApsaraVideo Player SDK allows you to play videos in a list. This increases the video loading speed.|
|Scaling mode|ApsaraVideo Player SDK supports image padding and cropping.|
|Mute|ApsaraVideo Player SDK allows you to enable or disable the mute feature.|
|Volume adjustment|ApsaraVideo Player SDK allows you to adjust the system volume in real time. You can use gestures to adjust the volume on the UI.|
|Brightness adjustment|ApsaraVideo Player SDK allows you to adjust the system brightness. You can use gestures to adjust the brightness on the UI.|
|Audio-only playback|ApsaraVideo Player SDK allows you to play MP3 audio files that are encoded by using the AAC codec.|
|Multi-player playback|ApsaraVideo Player SDK allows you to add multiple players on one UI to simultaneously play videos.|
|VOD playback or live video playback|ApsaraVideo Player SDK supports the playback feature of ApsaraVideo VOD and ApsaraVideo Live.|
|URL-based playback|ApsaraVideo Player SDK allows you to play on-premises videos and online videos based on their URLs.|
|VID-based playback|ApsaraVideo Player SDK supports the video playback in ApsaraVideo VOD.|
|Autoplay|ApsaraVideo Player SDK supports autoplay of a video after the video is prepared.|
|Seek|ApsaraVideo Player SDK allows you to drag the slider on the progress bar to the specified point in time. You can use gestures to control the slider on the UI.|
|Screen lock|ApsaraVideo Player SDK supports the screen lock feature, which allows you to lock the screen orientation and hide UI elements. You can use gestures to use the screen lock feature on the UI.|
|Resolution switching|ApsaraVideo Player SDK allows you to switch between multiple resolutions for VOD and transcoded streams.|
|Encrypted playback|ApsaraVideo Player SDK allows you to play VOD and transcoded streams that are encrypted.|
|Secure download|ApsaraVideo Player SDK allows you to use the specified application to download and encrypt videos.|
|Time shifting during live streaming|ApsaraVideo Player SDK allows you to play live streams in time shifting mode. You can set the start, stop, and current playback time and seek to the specified point in time.|
|Play-and-cache|ApsaraVideo Player SDK supports the play-and-cache feature for loop playback of short videos.|
|Playback speed adjustment|ApsaraVideo Player SDK allows you to adjust the playback speed from 0.5x to 2x speed. The audio pitch remains unchanged at different playback speeds.|
|Background playback|ApsaraVideo Player SDK allows you to continue playing audio streams when the application is switched from the UI to the background.|
|Instant loading|ApsaraVideo Player SDK supports instant loading within seconds for VOD and live streaming.|
|Dynamic frame synchronization|ApsaraVideo Player SDK supports dynamic frame synchronization for live streaming to reduce latency.|
|Automatic reconnection|ApsaraVideo Player SDK supports automatic reconnection during live streaming.|
|Video snapshot|ApsaraVideo Player SDK allows you to capture a frame of a playback image.|
|In-cache seeking|ApsaraVideo Player SDK allows you to retain the cached video content during seeking without clearing it to accelerate the seeking speed.|
|Rendering angle|ApsaraVideo Player SDK supports the following rendering angles of video images: 0°, 90°, 180°, and 270°.|
|Image rendering|ApsaraVideo Player SDK supports the following image rendering modes: no image, horizontal image, and vertical image.|
|Multi-bitrate switching|ApsaraVideo Player SDK supports seamless multi-bitrate switching of HTTP Live Streaming \(HLS\) Encryption-based live streams.|
|Preview|ApsaraVideo Player SDK supports the preview feature of ApsaraVideo VOD.|
|Hardware decoding|ApsaraVideo Player SDK supports H.264 and H.265 hardware decoding and allows you to switch between H.264 and H.265 hardware decoding.|
|Decoding blacklist|ApsaraVideo Player SDK allows you to set a blacklist for hardware decoding.|
|HTTP header|ApsaraVideo Player SDK supports custom HTTP request headers.|

## Feature highlights

|Feature|Description|
|-------|-----------|
|Short video playback|ApsaraVideo Player SDK supports loop playback of short videos and instant playback within seconds after you slide to a short video. For more information, see [Overview](/intl.en-US/Short Video Solution/Overview.md).|
|Playback speed adjustment|ApsaraVideo Player SDK allows you to adjust the playback speed from 0.5x to 2x speed in real time. The audio pitch remains unchanged at different playback speeds.|
|Encrypted playback|ApsaraVideo Player SDK allows you to transcode video streams into encrypted streams in the cloud. The encrypted streams can be decrypted only by using ApsaraVideo Player SDK. This ensures video security.|
|Secure download|ApsaraVideo Player SDK supports secondary encryption for downloaded videos. This ensures that the downloaded videos can be played only by the specified application. This way, advanced hotlink protection is provided.|
|Video caching|ApsaraVideo Player SDK supports the play-and-cache feature for loop playback of short videos. This helps reduce traffic consumption.|
|Video snapshot|ApsaraVideo Player SDK allows you to capture the current frame of a playback image. You can use a snapshot as a video thumbnail, store snapshots on your on-premises device, or share snapshots with your friends.|

## Benefits

-   Ease of integration

    Unified operations and error codes are provided for Android and iOS applications. The interfaces are similar to system operations in design. This facilitates developers to integrate ApsaraVideo Player SDK.

-   Hierarchical architecture design

    Basic features, business features, and UI components are hierarchically designed. This ensures the most compact package size and allows you to select a proper combination as needed.

-   Cloud and client integration

    Video streams are encrypted in the cloud and decrypted on the clients to ensure video security. Data is collected on the clients and analyzed in the cloud. This facilitates business operations.

-   Multiple security protection features

    Multiple features are provided to protect videos in different scenarios, including hotlink protection, URL signing, encrypted playback, and secure download.


## Scenarios

-   Sliding and loop playback of short videos

    ApsaraVideo Player SDK allows you to customize the view size to play videos in full screen. It also supports multi-player playback, autoplay, and pre-loading. These features allow you to watch multiple videos in full-screen sliding mode. To reduce traffic consumption and ensure seamless loop playback, ApsaraVideo Player SDK provides the play-and-cache and loop playback operations. You can configure these operations with several simple steps to meet business demands.

-   Video copyright protection

    For example, if you want to build an education website with video courses from teachers and open the courses only to premium users, you must protect your videos from being pirated. ApsaraVideo Player SDK provides the following multiple protection features:

    -   Hotlink protection: This feature allows only the users in the whitelist to access your resources.
    -   URL signing: This feature ensures that videos can be played only within their authentication validity period.
    -   Encrypted playback: This feature ensures that videos can be played only by using ApsaraVideo Player SDK.
    -   Secure download: This feature ensures that the downloaded videos can be played only by the application with a unique bundle ID or signature that you specify in the console.
-   Data-driven operations

    ApsaraVideo Player SDK collects usage data of users from user devices and sends the data to the cloud in real time. It provides data isolation and confidentiality features to ensure that the data that is generated for a user serves only the user.


## SDK download

For more information, see [SDK download](/intl.en-US/SDK Downloads/SDK download.md), where you can download the SDK and demo as needed.

