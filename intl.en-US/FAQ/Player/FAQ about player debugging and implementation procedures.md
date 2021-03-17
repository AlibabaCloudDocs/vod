# FAQ about player debugging and implementation procedures

ApsaraVideo Player is free of charge. We recommend that you use it with services such as ApsaraVideo VOD, ApsaraVideo Live, and ApsaraVideo for Media Processing to obtain better experience. For example, you can switch between multiple resolutions, securely play videos, and download encrypted videos.

## How do I upload and play a video on the client?

For more information, see [Media upload](/intl.en-US/Developer Guide/Upload Medias/Overview.md) and [Overview](/intl.en-US/Developer Guide/Video play/Overview.md).

Procedure: 1. Your application requests an upload credential. 2. The AppServer issues an upload credential. 3. You upload a video and obtain the video ID. 4. The AppServer obtains a playback credential \(playAuth\). 5. The AppServer delivers the playAuth to the client. 6. The video is played. The following figure shows the procedure.

![Obtain the playAuth.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2554695161/p179095.png)

**Note:** A video can be played only after it is uploaded to ApsaraVideo VOD and is transcoded. After a video is transcoded, ApsaraVideo VOD sends the TranscodeComplete callback notification. For more information, see [TranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/TranscodeComplete.md).

## What can I do if ApsaraVideo Player SDK for iOS cannot play videos in the background?

ApsaraVideo Player SDK for iOS cannot play videos in the background after you press the Home button, even if you use the demo. To resolve this issue, perform the following steps:

1.  In Xcode, turn on Background Modes and enable the feature of collecting data in the background.

    ![DuCXfvnsZJMUdeDiGjnX.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2554695161/p179092.png)

2.  Open the `AliyunPlayerVodPlayViewController.m` file in the vod folder.

    ![JmiOhyxQtRjxCkoopwDY.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3554695161/p179093.png)

3.  Find the **resignActive** method below the **becomeActive** method. Comment out the **pause** method in the **resignActive** method, as shown in the following figure.

    ![HYpasKrmWAuWslCvcmxd.png ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3554695161/p179094.png)


## What are the updates in each version of ApsaraVideo VOD?

For more information about the updates in each version of ApsaraVideo Player SDK, see [Release notes of ApsaraVideo Player SDKs](/intl.en-US/SDK Downloads/player-sdk-new-history/Release notes of ApsaraVideo Player SDK for Android.md).

## How can I obtain a playAuth for player debugging during client development?

During client development, you can use a Python script to obtain a playAuth for debugging. Perform the following steps:

1.  Install Python 2.7 and pip. This environment is built in MacOS and must be installed in Windows.
2.  Run the following commands on a terminal to install the SDK:

    ```
    pip install aliyun-python-sdk-core
    pip install aliyun-python-sdk-vod
    ```

3.  Download the [Python script](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/52848/cn_zh/1500973333876/playAuth.py). Use the AccessKey ID and AccessKey secret that you obtain from the Alibaba Cloud Management Console to replace the corresponding fields in the script. Then, obtain the video ID of an uploaded video from the ApsaraVideo VOD console and replace the corresponding field in the script.
4.  Run the following command in the directory where the Python script resides on the terminal:

    ```
    python playAuth.py
    ```

5.  Check the obtained playAuth and video ID on the terminal.
6.  Play the video by using ApsaraVideo Player SDK based on the obtained playAuth and video ID.

**Note:** When you use this method to obtain a playAuth, make sure that the playAuth is within the validity period. A playAuth is valid only for 100 seconds. The most possible reason for playback failures is that the playAuth expires.

