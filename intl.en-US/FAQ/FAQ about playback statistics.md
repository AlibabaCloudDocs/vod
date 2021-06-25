# FAQ about playback statistics

This topic provides answers to some frequently asked questions on the accuracy of playback statistics and playback counts.

## How does ApsaraVideo VOD collect playback statistics? Are the statistics accurate?

|Statistical method|Accuracy|Description|
|------------------|--------|-----------|
|Use the data tracking feature of ApsaraVideo Player SDK to collect playback behavior data.|This method provides accurate statistics and is recommended.|Player SDKs with the data tracking feature, such as ApsaraVideo Player SDK, can collect accurate and detailed playback behavior data from logs that are regularly reported. The data contains the number of video views, the number of video viewers, and the playback duration. ApsaraVideo VOD provides a service to collect statistics on playbacks that use ApsaraVideo Player SDK. Each user device counts as a user. ApsaraVideo VOD does not collect statistics on URL-based playbacks and playbacks that use player SDKs other than ApsaraVideo Player SDK. The detailed behavior data of such playbacks may not be obtained to ensure accurate statistics.|
|Estimate the number of video views based on the number of requests sent to Alibaba Cloud CDN.|This method provides inaccurate statistics and is not recommended.|Some video services may estimate the number of video views based on the number of requests sent to Alibaba Cloud CDN. Each request counts as a video view. However, such statistics are inaccurate and may cause losses to you. For example, the number of requests is generally greater than the number of video views. These statistics do not differentiate playbacks between different devices or users. They also do not contain playback duration or behavior data. ApsaraVideo VOD does not collect statistics in this way.|

## I use only ApsaraVideo Player SDK to play videos. If I query the playback statistics from the previous day, can ApsaraVideo VOD provide me with completely accurate statistics?

Yes. However, playback statistics may have unavoidable discrepancies due to the following reasons:

-   ApsaraVideo Player collects logs every 30 seconds. In between log collections, ApsaraVideo Player detects unexpected playback interruptions in the player but not on web pages. As a result, statistics on playback duration may have deviations of 30 seconds or fewer.
-   The key of an HTML5 player changes when users use a new device. ApsaraVideo Player recognizes the new device as a new unique visitor, which results in deviations in playback statistics on unique visitors.

## Why do I get inconsistent traffic statistics and number of video views when I use only ApsaraVideo Player SDK to play videos?

ApsaraVideo VOD provides playback and traffic statistics with acceptable delays. You get inconsistent traffic statistics and number of video views because of the difference in the way that ApsaraVideo VOD collects and processes playback and traffic statistics. This difference causes a time window between the two statistics. As a result, the number of video views and traffic statistics may not match at the latest point in time. Such discrepancies do not exist for playback and traffic statistics earlier than the time window. For example, you get consistent data when you query the statistics from the previous day. ApsaraVideo VOD is working to resolve this issue as soon as possible to reduce impacts on your business.

Note that one video view is not equal to a full video playback. Events that interrupt, seek, or stop a playback may cause acceptable deviations in the statistics. Therefore, the traffic estimation may be inaccurate if you use these formulas: `Number of video views × Video size` or `Number of video views × Video bitrate × Playback duration`.

## Why do I get inaccurate playback statistics when I play videos by using both ApsaraVideo Player SDK and streaming URLs?

ApsaraVideo VOD collects statistics only on playbacks that use ApsaraVideo Player SDK. ApsaraVideo VOD does not collect statistics on URL-based playbacks and playbacks that use player SDKs other than ApsaraVideo Player SDK. The detailed behavior data of such playbacks may not be obtained to ensure accurate statistics. However, ApsaraVideo VOD collects statistics on traffic consumed by all playback requests. Therefore, the ApsaraVideo VOD console shows that more traffic is consumed for fewer playbacks.

## I do not use ApsaraVideo Player SDK. Why does the ApsaraVideo VOD console show that the number of video views is zero but traffic is consumed?

The ApsaraVideo VOD console provides statistics and top rankings only for playbacks performed by ApsaraVideo Player, as shown in the following figure. ApsaraVideo VOD does not collect statistics on URL-based playbacks and playbacks that use player SDKs other than ApsaraVideo Player SDK. The detailed behavior data of such playbacks may not be obtained to ensure accurate statistics. If the number of video views in the ApsaraVideo VOD console is zero, it only indicates that your videos are not played by ApsaraVideo Player. However, your videos may be played in other ways. ApsaraVideo VOD collects statistics on traffic consumed by all playback requests. Therefore, the ApsaraVideo VOD console shows that the number of video views is zero but traffic is consumed.

![vod-qa.jpg ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1516854261/p179099.jpg)

