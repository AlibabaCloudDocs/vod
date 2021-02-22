# Delivery and playback

ApsaraVideo VOD allows you to play audio and video files. You can preview audio and video files in the ApsaraVideo VOD console. You can also integrate ApsaraVideo Player SDK and third-party players to play audio and video files.

## CDN acceleration

ApsaraVideo VOD uses Alibaba Cloud CDN to accelerate video delivery and optimize the user experience of video playback.

**Hotlink protection**: Hotlink protection uses the HTTP Referer header field to trace and identify request sources. You can configure a Referer blacklist or whitelist \(but not both\) to identify and filter visitors. This way, you can limit access to the videos to be managed and delivered in ApsaraVideo VOD.

**URL signing**: URL signing is a more secure and reliable method that integrates Alibaba Cloud CDN nodes with the origin server to protect resources on the origin server. URL signing protects the resources that you upload to ApsaraVideo VOD from illegal download and misuse.

**Playback authentication**: Playback authentication is a secondary authentication mechanism of ApsaraVideo VOD, which is based on Alibaba Cloud AccessKey authentication.

## Audio and video playback

As an essential part of ApsaraVideo, ApsaraVideo Player SDK helps implement end-to-end video services. It provides the basic playback features of ApsaraVideo VOD and ApsaraVideo Live, and integrates various ApsaraVideo services. It supports features such as encrypted playback, secure download, resolution switching, and live Q&A. You can use ApsaraVideo Player SDK to implement simple, fast, secure, and stable video playback services.

## Statistical analysis

**Resource usage**: ApsaraVideo VOD allows you to query multi-dimensional statistics on traffic, bandwidth, storage, and transcoding length in the past 30 days. You can also export the details of resource usage.

**Operation statistics**: Based on the data that is collected by ApsaraVideo Player from clients, ApsaraVideo VOD provides statistics on playback behaviors and popular resources that are applicable to your operations. For example, ApsaraVideo VOD collects statistics on the number of unique visitors \(UVs\), the number of video views \(VVs\), playback duration per capita, and popular videos.

