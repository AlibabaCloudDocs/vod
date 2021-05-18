Manual review 
==================================

ApsaraVideo VOD provides the manual review service. To review videos for short videos, media, and video platforms, we recommend that you use the Automated review feature before you use the manual review service. This topic describes how to use the manual review service and how to view the review history.

Usage 
--------------------------

You can use the manual review service in the ApsaraVideo VOD console or by calling API operations.
**Notice**

Before you use the manual review service, make sure that you complete the preparations for media review. For more information, see [Preparations for media review](~~100662~~).

* Operations in the console

  * On the **[To Be Reviewed](https://vod.console.aliyun.com/settings/workflow#/check/video)** page, you can use the manual review service. For more information, see [Review videos](/intl.en-US/User Guide/Media file review/Review videos.md).

    
  
  * You can review a single video or review multiple videos at a time.

    
  
  * The review result can be sent to the callback URL in callback mode. For more information, see [CreateAuditComplete](/intl.en-US/Developer Guide/Event notification/Events/CreateAuditComplete.md).

    
  

  

  ![Manual review](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6563401161/p181840.png)
  

* API operations or SDKs

  * You can call the [CreateAudit](/intl.en-US/API Reference/Content Moderation/Manual Audit/CreateAudit.md) operation to perform manual review.

    
  
  * The review result can be sent to the callback URL in callback mode. For more information, see [CreateAuditComplete](/intl.en-US/Developer Guide/Event notification/Events/CreateAuditComplete.md).

    
  

  




View the review history 
--------------------------------------------

* After a video is reviewed by using the manual review service, the manual review status of the video becomes **Review** . To view the review details of the video, click **Details** for the video on the **To Be Reviewed** page. To view the manual review history of the video, click **Human Review Details** .

  ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6563401161/p178349.jpg)![History](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6563401161/p181846.png)
  

* You can also call the [GetAuditHistor](/intl.en-US/API Reference/Content Moderation/Manual Audit/GetAuditHistory.md) operation to query the manual review history.

  



