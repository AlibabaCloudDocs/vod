Intelligent review 
=======================================

Intelligent review allows you to accurately identify videos, thumbnails, and titles. You can use the console or call API operations to configure review templates. Then, you can use the review templates to perform intelligent review. This topic describes the scenarios and usage of the intelligent review feature.

Features 
-----------------------------

Intelligent review is implemented based on a large amount of labeled data and a large number of deep learning algorithms. This feature can accurately identify illegal and non-compliant content such as pornography, terrorism, and politically sensitive content in videos, thumbnails, and titles.This feature can also identify illegal and non-compliant content from multiple dimensions such as voice, text, and vision.

* Identify pornographic content

  Identify pornographic and sexual content in video thumbnails, video titles, and video content from multiple dimensions such as voice, text, and vision by using AI technologies.
  

* Identify terrorism and politically sensitive content

  Identify weapons, characters, clothing, gore, smoke, light, and symbols to determine whether content violates content regulations. This can help reduce the risks of non-compliant content for your business.
  

* Identify advertisements and QR codes

  Identify texts, watermarks, and QR codes in videos to detect advertisements placed by micronets and advertisements inserted into videos.
  

* Identify non-compliant scenarios

  Identify non-compliant scenarios such as picture-in-picture, meaningless images, and smoking. An independent model is trained for each scenario. This resolves the mutual interference issue that occurs when a single model is trained to detect non-compliant scenarios in different scenario categories. This also improves the precision and recall of identification.
  




Usage 
--------------------------

**Notice**

Before you use the intelligent review service, make sure that you complete the [preparations](/intl.en-US/Developer Guide/Media review/Overview.md).

* By using the API or SDK

  1. For a video that is uploaded to the media library in ApsaraVideo VOD, you can submit an intelligent review job by using the API or SDK. For more information, see [SubmitAIMediaAuditJob]().

     
  
  2. After the intelligent review job is complete, an event notification is sent to the specified callback URL. This event notifies you of the job result. For more information, see [AIMediaAuditComplete](/intl.en-US/Developer Guide/Event notification/Events/AIMediaAuditComplete.md). You can also query the job result by calling API operations. For more information, see [GetAIMediaAuditJob]().

     
  
  3. Query results

     * After intelligent review is complete, you can query the review result summary by calling API operations. For more information, see [GetMediaAuditResult]().

       
     
     * After intelligent review is complete, you can query the review result details by calling API operations. For more information, see [GetMediaAuditResultDetail]().

       
     
     * After intelligent review is complete, you can query the review result timeline by calling API operations. For more information, see [GetMediaAuditResultTimeline]().

       
     

     
     **Notice**

     ApsaraVideo VOD stores images cited in the intelligent review result free of charge for **two weeks** . After two weeks, the images are automatically deleted.
     
  

  




<!-- -->

* By using the console

  1. On the **[Add Intelligent Review Template](https://vod.console.aliyun.com/settings/transcode/add#/check/setting/template/add)** page in the ApsaraVideo VOD console, create an intelligent review template.

     
  
  2. On the **[Review Settings](https://vod.console.aliyun.com/settings/transcode/add#/check/setting)** page, configure the template that is used to review.

     
  
  3. On the To Be Reviewed page, click **Start Review** on the right side of the video to start automated review.

     
  

  

  You can also add an automated review node to a workflow. Then, you can use the workflow to complete automated review when you upload files.
  



