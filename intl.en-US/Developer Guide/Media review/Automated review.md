Automated review 
=====================================

The automated review feature can help you accurately identify the risky and illegal content in video, audio, and image files, and their thumbnails and titles from multiple dimensions. You can configure automated review templates and standards to meet various business requirements. This topic describes the scenarios and usage of the automated review feature.

Features 
-----------------------------

The automated review feature is implemented based on a large amount of labeled data and deep learning algorithms. This feature reviews media files from multiple dimensions such as voice, text, and vision. It can accurately identify illegal and non-compliant content such as pornography, terrorism, ads, QR codes, logos, undesirable content, and audio spam in videos and their thumbnails and titles. 
**Note**

The automated review feature in the Singapore region supports only the pornography, terrorism, and undesirable content detection.

The following table describes the review types supported by the automated review feature.


|          Review type          |                                                                                      Description                                                                                      |                                                              Category of review results                                                              |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pornography detection         | Detects whether media files contain pornographic or sexy content.                                                                                                                     | Normal, porn, and sexy.                                                                                                                              |
| Terrorism                     | Detects whether media files contain terrorism or political content.                                                                                                                   | Normal, blood and gore, explosion, outfit, logo, weapon, politics, violence, crowd, parade, car crash, flag, and location.                           |
| Ad violation detection        | Detects whether video and image files contain ads or illegal text.                                                                                                                    | Normal, politics, porn, abuse, terrorism, prohibited content, junk content, spam, psoriasis ads, QR code, mini program code, and other ads.          |
| Undesirable content detection | Detects whether video and image files contain undesirable scenes, such as the black screen, black edges, dark images, picture-in-picture (PiP), smoking, or streaming during driving. | Normal, PiP, smoking, streaming during driving, and no image such as black screen or white screen.                                                   |
| Logo detection                | Detects whether video and image files contain logos, such as TV station logos or trademarks.                                                                                          | Normal, controlled logo, and trademark.                                                                                                              |
| Audio anti-spam               | Detects whether audio and video files contain audio junk information, such as ads, political content, or terrorism content.                                                           | Normal, junk information, ads, politics, terrorism, abuse, porn, spam, violation, custom, and meaningless. For example, you can set custom keywords. |



Scenarios 
------------------------------

* **UGC review** 

  The automated review feature can be used to detect illegal content and quality issues in a large amount of user-generated content (UGC). This can reduce the workload of manual review.
  

* **On-demand content review** 

  The automated review feature can be used to detect terrorism and political content in on-demand videos based on the latest political news. This can significantly reduce illegal content.
  




Usage 
--------------------------

For more information about the prerequisites, see [Video AI]().

To use the automated review feature in the Singapore region, you must [submit a ticket](https://ticket-intl.console.aliyun.com/#/ticket/createIndex).

* **Submit an automated review job** 

  You can submit an automated review job by using the API or SDK to review the video, audio, and image files that are uploaded to ApsaraVideo VOD. For video and audio files, you can call the [SubmitAIMediaAuditJob]() operation. For image files, you can call the [SubmitAIImageAuditJob]() operation.
  




<!-- -->

* **Manage automated review templates** 

  When you submit an automated review job, you can specify an automated review template for the job to configure the review process.
  1. You can call the [AddAITemplate]() operation to create a template, the [DeleteAITemplate]() operation to delete a template, the [UpdateAITemplate]() operation to modify a template, the [GetAITemplate]() operation to query the information about a template, and the [ListAITemplate]() operation to query the information about all templates.

     
  
  2. If you do not specify an automated review template for an automated review job, the default template is used. You can call the [SetDefaultAITemplate]() operation to specify a custom automated review template as the default template. You can also call the [GetDefaultAITemplate]() operation to query the information about the current default template.

     
  

  




<!-- -->

* **Receive callback messages** 

  After an automated review job is complete, a callback message that contains the review results will be sent to the specified URL. For more information, see [AIMediaAuditComplete](/intl.en-US/Developer Guide/Event notification/Events/AIMediaAuditComplete.md).
  




<!-- -->

* **Call API operations to query review results** 

  1. After an automated review job is complete, you can call the [GetAIMediaAuditJob]() operation to obtain the review results.

     
  
  2. After an automated review job is complete, you can call the [GetMediaAuditResult]() operation to obtain the summary of the review results.

     
  
  3. After an automated review job is complete, you can call the [GetMediaAuditResultDetail]() operation to obtain the details of the review results.

     
  
  4. After an automated review job is complete, you can call the [GetMediaAuditResultTimeline]() operation to obtain the points in time of the detected illegal content.

     
  
  5. After an automated review job is complete, you can call the [GetMediaAuditAudioResultDetail]() operation to obtain the details of the audio review results.

     
  

  



**Notice**

ApsaraVideo VOD stores the images that are cited in the automated review results free of charge for **two weeks** . After two weeks, the images are automatically deleted.
