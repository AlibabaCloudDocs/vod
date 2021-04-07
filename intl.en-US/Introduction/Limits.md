# Limits

By default, ApsaraVideo VOD limits the resource usage and the number of API calls. To raise the limits, you can contact after-sales technical support or submit a ticket. In the meantime, we recommend that you describe your scenarios and expected thresholds, such as the number of domain names and the frequency of playback operation calls.

|Resource type|Limit|Scenario|
|-------------|-----|--------|
|Domain name|A maximum of 20 domain names can be configured within an Alibaba Cloud account. If your website is located in China, make sure that the domain name has an Internet content provider \(ICP\) filing.|For more information, see [Add a domain name](/intl.en-US/User Guide/Domain management/Add a domain name.md).|
|Resource refreshing and prefetching|You can refresh a maximum of 2,000 URLs and 100 directories and prefetch a maximum of 500 URLs per day. You cannot prefetch content based on directories.|For more information, see [Refresh and prefetch](/intl.en-US/User Guide/Domain management/Refresh and prefetch.md).|
|Storage|A maximum of one dedicated bucket is allocated in one region.|For more information, see [Manage VOD resources](/intl.en-US/User Guide/Global settings/Manage VOD resources.md).|
|Category|A maximum of three levels of categories can be created in each category tree within an Alibaba Cloud account. Each category can contain a maximum of 100 subcategories.|For more information, see [Manage video categories](/intl.en-US/User Guide/Global settings/Manage video categories.md).|
|Custom tag|A maximum of 16 tags can be specified for a video.|For more information, see [Manage media assets](/intl.en-US/User Guide/Media library/Manage media assets.md).|
|Workflow|A maximum of 20 custom workflows can be configured within an Alibaba Cloud account.|N/A|
|Transcoding template group|A maximum of 20 transcoding template groups can be configured within an Alibaba Cloud account.|For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).|
|Review, editing, and snapshot templates|A maximum of 20 templates for video reviewing, editing, or snapshot capture can be configured within an Alibaba Cloud account.|For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).|
|Transcoding templates configured in a transcoding template group|A maximum of 20 transcoding templates can be configured in a transcoding template group.|For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).|
|Watermark|A maximum of 20 watermarks can be configured within an Alibaba Cloud account.|For more information, see [Manage watermarks](/intl.en-US/User Guide/Global settings/Manage watermarks.md).|
|Watermarks associated with a transcoding template|A maximum of five watermarks can be configured for a transcoding template.|For more information, see [Manage transcoding settings](/intl.en-US/User Guide/Global settings/Manage transcoding settings.md).|
|Online editing|You can edit only media files that are stored in the same region.|For more information, see [t1959244.md\#](/intl.en-US/User Guide/Production center/Production center.md).|
|Callback URL|A maximum of one callback URL can be configured in one region within an Alibaba Cloud account.|For more information, see [Configure a callback](/intl.en-US/User Guide/Global settings/Configure a callback.md).|

## Limits on server API calls

By default, ApsaraVideo VOD limits the frequency of calling server API operations. If the number of requests for calling an API operation exceeds the upper limit, these excess requests are rejected.

When the upper limit is reached, ApsaraVideo VOD rejects the excess requests in a random manner and returns a 400 status code. The error code is Throttling.User, and the error message is "Request was denied due to user flow throttling."

## Limits on API operations

|Type of API operation|Frequency limit \(count/s\)|API operation|
|---------------------|---------------------------|-------------|
|Media upload|100|[CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md), [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md), [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md), [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md), [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md), and [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md)|
|Audio and video playback|300|[GetPlayInfo](/intl.en-US/API Reference/Audio and video playback/GetPlayInfo.md) and [GetVideoPlayAuth](/intl.en-US/API Reference/Audio and video playback/GetVideoPlayAuth.md)|
|High-frequency query|100|API operations that are called to query media assets and video AI jobs, such as [SearchMedia](/intl.en-US/API Reference/Media asset management/Media asset search/SearchMedia.md) and [GetVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfo.md)|
|Configuration management|10|API operations for configuring transcoding templates, snapshot templates, video watermarks, video AI templates, and domain names, such as [AddTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/AddTranscodeTemplateGroup.md)|
|Other API operations|30|API operations for submitting transcoding jobs, capturing snapshots, implementing video AI processing, reviewing videos, modifying or deleting videos, and editing or merging videos, such as [DeleteVideo](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteVideo.md) and [SubmitTranscodeJobs](/intl.en-US/API Reference/Media processing/Process initiation/SubmitTranscodeJobs.md)|

## Limits on IP addresses

By default, the number of requests from an IP address is limited to 300 per second. Note that the limit is applicable to Internet egress IP addresses.

## ICP filing for domain names for CDN

You can determine whether an ICP filing is required for a domain name for CDN that is added to ApsaraVideo VOD based on the edge group of the domain name for CDN. If the edge group of a domain name for CDN is the globe or mainland China, an ICP filing is required for the domain name for CDN. We recommend that you apply for an ICP filing in the [Alibaba Cloud ICP Filing system](https://beian.aliyun.com/?spm=5176.8142029.388261.3.a0SCC3).

**Note:** You may need to accelerate content deliveries for ApsaraVideo VOD in mainland China. In this case, you must complete the ICP filing for the domain name of your application at your origin site, no matter where your origin site is.

## Content moderation

All the content of domain names added to Alibaba Cloud must be reviewed. Domain names that cannot be added to Alibaba Cloud CDN include but are not limited to:

-   Content that is inaccessible or does not include valid information
-   Servers that host pirated games
-   Websites that provide multiplayer games and card games
-   Websites that provide downloads of pirated software
-   Websites that run P2P lending
-   Lottery websites
-   Websites of unlicensed hospitals and pharmaceuticals
-   Websites that contain content of pornography, drugs, or gambling

**Note:**

-   If the preceding content is detected from your domain name for CDN, you must bear all risks that may arise. Alibaba Cloud CDN regularly reviews the content of accelerated domain names. If illicit content is detected from a domain name, Alibaba Cloud CDN immediately disables or blocks the domain name. If the violation is severe, Alibaba Cloud CDN may even permanently block all domain names of the Alibaba Cloud account.
-   If you add a wildcard domain name, for example, `*.example.com`, to Alibaba Cloud CDN and a specific domain name, for example, `a.example.com` contains illicit content, Alibaba Cloud CDN disables the wildcard domain name \(`*.example.com`\).
-   If a domain name is rejected after the review, you can check the reason for the rejection on the Domain Names page in the Alibaba Cloud CDN console. You can modify the content based on the rejection details, and submit the domain name for review again.

