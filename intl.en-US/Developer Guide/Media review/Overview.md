Overview 
=============================

ApsaraVideo VOD provides media review features. These features include manual review, and security review. This topic describes the benefits, features, scenarios, and preparations of ApsaraVideo VOD review.

Overview 
-----------------------------

Media resources uploaded may violate the content laws and regulations. ApsaraVideo VOD provides a full range of media review services such as manual review, and security review configurations for videos, audios, images, and texts. These automated and intelligent features can reduce the risks of illegal and non-compliant content such as terrorism, politically sensitive content, pornography, and violence. These features can also lower the cost of labor that is required to review content.

Benefits of ApsaraVideo VOD review 
-------------------------------------------------------

* The basic review capability is the same as that of [AliGreenNet](https://www.aliyun.com/product/lvwang). Media review can detect illegal and non-compliant content such as terrorism, politically sensitive content, pornography, advertisements, and abuse. Media review can be used to detect this content in images, videos, texts, and audios.

  

* Media review further aggregates videos, audios, images such as snapshots and thumbnails, and texts such as titles, profiles, and tags in the form of media resources. All audio and video media resources can be processed in a call, which is simpler and more efficient.

  

* ApsaraVideo VOD supports workflow capabilities and allows you to manually review files based on custom configuration templates. After a media file is uploaded to ApsaraVideo VOD, the system automatically reviews the video file and calls back the review results in real time.

  

* ApsaraVideo VOD review integrates all aspects of the review process. ApsaraVideo VOD review is integrated with media asset management, editing, production, distribution, and playback to meet the needs of more diverse scenarios. For example, you can transcode, discard, or archive a video after review. Non-compliant clips can also be automatically cropped and distributed.

  




Features 
-----------------------------



<!-- -->

* Manual review

  ApsaraVideo VOD provides the manual review service. This service enables you to detect and block illegal and non-compliant videos in advance or take them offline at your earliest opportunity. This way, you can avoid or reduce the adverse effects caused by illegal and non-compliant content.

  For more information, see [Manual review](/intl.en-US/Developer Guide/Media review/Manual review.md).
  




<!-- -->

* Security IP address preview

  ApsaraVideo VOD provides the security IP address preview service. This service ensures that only users whose IP addresses are added to review security groups can play videos in the Checking or Blocked state.

  For more information, see [Security IP address preview](/intl.en-US/Developer Guide/Media review/Security IP address preview.md).
  




Scenarios 
------------------------------

* Short video or UGC video service providers can use the intelligent review service to identify illegal and non-compliant content in a large number of videos uploaded by users. Intelligent review conducts manual review of suspected illegal videos. This reduces the manual review workload.

  

* ApsaraVideo VOD providers and media companies can use the intelligent review service to identify illegal and non-compliant content such as terrorism, politically sensitive content, and violence. This way, users can control illegal and non-compliant content.

  




Preparations 
---------------------------------

1. An Alibaba Cloud account is [registered](https://account.aliyun.com/register/register.htm?oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh), [Real-name verification](https://help.aliyun.com/knowledge_list/37170.html) is complete, and [ApsaraVideo VOD](https://www.aliyun.com/product/vod) is activated.

   

2. Obtain an AccessKey pair to access ApsaraVideo VOD.

   You can create an AccessKey pair for your Alibaba Cloud account on the [AccessKey Management](https://ak-console.aliyun.com/?spm=5176.doc57741.2.8.uLYY2M#/accesskey) page in the Alibaba Cloud Management Console. You can also create a RAM user in the [RAM console](https://ram.console.aliyun.com/?spm=5176.doc57741.2.2.fQnI2T#/user/list) and grant the user the permissions such as `AliyunVODFullAccess` to access ApsaraVideo VOD. For more information, see [RAM user access](/intl.en-US/Developer Guide/Access authorization/Create and grant permissions to a RAM user.md).
   

3. Click **Review** in the ApsaraVideo VOD console and click [Review Settings](https://vod.console.aliyun.com/#/check/setting).

   1. Configure the review process. You can select the Review Before Publish or Review After Publish mode. By default, the review mode is set to **Review After Publish** . You can set the review mode to **Review Before Publish** . If you set the review mode to Review Before Publish, an uploaded video cannot be accessed after transcoding and delivery acceleration and can be played only after the video is manually approved.![Review settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3563401161/p181782.png)

      
   
   2. Configure intelligent review. You can set the default intelligent review template and add intelligent review templates.![Intelligent review](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3563401161/p181784.png)

      
   

   

4. In the left-side navigation pane, choose **Media Processing \> Callback** . On the [Callback](https://vod.console.aliyun.com/settings/workflow#/settings/callback) page, set Callback URL and select Events.![Callback](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6633031261/p181787.png)

   For manual review, to receive the [CreateAuditComplete](/intl.en-US/Developer Guide/Event notification/Events/CreateAuditComplete.md) event notification, you must select the **Create Audit Completed** event.
   



