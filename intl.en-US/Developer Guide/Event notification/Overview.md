Overview 
=============================

ApsaraVideo VOD supports the HTTP and MNS callback methods. This topic describes the event types, callback methods, callback configurations, callback protocols, and common callback parameters for event notifications. It also describes how to judge whether callbacks are successful, retries, and commonly asked questions.

Introduction 
---------------------------------

ApsaraVideo VOD supports event notifications for multiple storage regions. You can configure the callback methods and callback URLs for event notifications for each region. You can upload videos to different storage regions. After the videos are processed, ApsaraVideo VOD notifies you of the processing results based on the callback methods and callback URLs that you configured for the regions.

Event types 
--------------------------------

The following table describes the event types for which event notifications are provided in ApsaraVideo VOD.


|       **Event type**        |                                                            **Reference**                                                            |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| FileUploadComplete          | [FileUploadComplete](/intl.en-US/Developer Guide/Event notification/Events/FileUploadComplete.md)                   |
| ImageUploadComplete         | [ImageUploadComplete](/intl.en-US/Developer Guide/Event notification/Events/ImageUploadComplete.md)                 |
| StreamTranscodeComplete     | [StreamTranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/StreamTranscodeComplete.md)         |
| TranscodeComplete           | [TranscodeComplete](/intl.en-US/Developer Guide/Event notification/Events/TranscodeComplete.md)                     |
| SnapshotComplete            | [SnapshotComplete](/intl.en-US/Developer Guide/Event notification/Events/SnapshotComplete.md)                       |
| DynamicImageComplete        | [DynamicImageComplete](/intl.en-US/Developer Guide/Event notification/Events/DynamicImageComplete.md)               |
| AddLiveRecordVideoComplete  | [AddLiveRecordVideoComplete](/intl.en-US/Developer Guide/Event notification/Events/AddLiveRecordVideoComplete.md)   |
| LiveRecordVideoComposeStart | [LiveRecordVideoComposeStart](/intl.en-US/Developer Guide/Event notification/Events/LiveRecordVideoComposeStart.md) |
| UploadByURLComplete         | [UploadByURLComplete](/intl.en-US/Developer Guide/Event notification/Events/UploadByURLComplete.md)                 |
| CreateAuditComplete         | [CreateAuditComplete](/intl.en-US/Developer Guide/Event notification/Events/CreateAuditComplete.md)                 |
| VideoAnalysisComplete       | [VideoAnalysisComplete](/intl.en-US/Developer Guide/Event notification/Events/VideoAnalysisComplete.md)             |
| AttachedMediaUploadComplete | [AttachedMediaUploadComplete](/intl.en-US/Developer Guide/Event notification/Events/AttachedMediaUploadComplete.md) |
| ProduceMediaComplete        | [ProduceMediaComplete](/intl.en-US/Developer Guide/Event notification/Events/ProduceMediaComplete.md)               |
| DeleteMediaComplete         | [DeleteMediaComplete](/intl.en-US/Developer Guide/Event notification/Events/DeleteMediaComplete.md)                 |
| MediaBaseChangeComplete     | [MediaBaseChangeComplete](/intl.en-US/Developer Guide/Event notification/Events/MediaBaseChangeComplete.md)         |



Callback methods 
-------------------------------------

ApsaraVideo VOD provides the **HTTP callback** ( **HTTPS compatible** **)** and **MNS callback** methods to obtain event notifications.

* HTTP callback (HTTPS compatible):

  You must deploy an HTTP service to receive callback messages and configure a callback URL in the ApsaraVideo VOD console. When an event is generated, ApsaraVideo VOD sends an HTTP POST request to the configured callback URL. The specific event content is sent in the HTTP POST request body.
  

* MNS callback:

  You must [authorize ApsaraVideo VOD to access MNS](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunVODDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//vod.console.aliyun.com/%22%2C%20%22Service%22%3A%20%22VOD%22%7D). Then, you can log on to the [MNS console](https://mns.console.aliyun.com) and create a queue or use an existing queue and call API operations to configure event notifications. When an event is generated, ApsaraVideo VOD writes callback messages to the queue. For information about how to read the messages, see the MNS documentation. For more information, see [Reliable MNS event notification](/intl.en-US/Developer Guide/Event notification/Reliable MNS event notification.md).
  




Comparison between the HTTP and MNS callback methods 
-------------------------------------------------------------------------



| **Comparison item** |                                                                                                                                                                                        **HTTP callback**                                                                                                                                                                                        |                                                        **MNS callback**                                                        |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Reliability         | If the HTTP message receiving service is abnormal (for example, the service is interrupted or restarts), messages may be lost.                                                                                                                                                                                                                                                                  | MNS callbacks are **more reliable** than HTTP callbacks. Almost all MNS callbacks can succeed if they are configured properly. |
| Security            | In the HTTP callback method, all users can send callback requests to the specified callback URLs. However, you can use callback authentication to reject invalid requests and enhance the security of HTTP callbacks. For more information, see [HTTP callback authentication](/intl.en-US/Developer Guide/Event notification/HTTP callback authentication.md). | MNS callback is **more secure** because only authorized users can read and write message queues.                               |
| Convenience         | HTTP callbacks are **more convenient** than MNS callbacks because you need only to deploy a message receiving service to use HTTP callbacks.                                                                                                                                                                                                                                                    | To use MNS callbacks, you must activate and configure MNS, and develop and deploy an application to consume messages.          |



You can select the callback method to best suit your specific scenarios.

Callback configurations 
--------------------------------------------

Log on to the ApsaraVideo VOD console. In the left-side navigation pane, choose **Configuration Management** \> **Media Processing** \> **Callback** . On the Callback page, configure the callback URL, queue, and events. For more information, see [Callback](/intl.en-US/User Guide/Global settings/Configure a callback.md).
**Notice**

If you select AI Processing Completed, notifications are sent for all AI events such as AIMediaAuditComplete, AIMediaDNAComplete, and AIVideoTagComplete.

Callback protocols 
---------------------------------------

* HTTP callback

  * Request: HTTP POST requests are sent and the request body is in the JSON format. For the specific request body for each event, see the event description documentation.

    
  
  * Response: ApsaraVideo VOD ignores the body content of responses.

    
  

  

* MNS callback

  The callback message is in the JSON format. For the specific message body for each event, see the event description documentation.
  




Common callback parameters 
-----------------------------------------------



| **Parameter** | **Type** |                                                                                                                 **Description**                                                                                                                 |
|---------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| EventTime     | String   | The time when the event is generated. The time is displayed in the **yyyy-MM-ddTHH:mm:ssZ** format and in UTC.                                                                                                                                  |
| EventType     | String   | The event type.                                                                                                                                                                                                                                 |
| VideoId       | String   | The ID of the video.                                                                                                                                                                                                                            |
| Status        | String   | The processing state of the video. Valid values: * **success** : The video is processed.   * **fail** : The video failed to be processed.    |
| Extend        | String   | If the UserData parameter is specified in the upload or submit operations and contains the Extend field, user custom data is returned in pass-through mode when the callback is complete. The value of this field can be 512 bytes in length.   |



Callback judgment and retries 
--------------------------------------------------

* HTTP callback

  * After an HTTP callback request is sent, ApsaraVideo VOD checks the HTTP status code in the response returned by the HTTP message receiving service. If the HTTP status code is 200, ApsaraVideo VOD determines the callback as successful. If the HTTP status code is not 200 or if the callback times out when no response is received within **5 seconds** , ApsaraVideo VOD determines the callback as failed. ApsaraVideo VOD checks only the HTTP status code in responses and ignores the body content of the responses.

    
  
  * If the callback request cannot be sent due to incorrect configurations (for example, if the callback URL is incorrect or if the HTTP message receiving service is abnormal), ApsaraVideo VOD retries to send the callback request two more times. ApsaraVideo VOD attempts to send a callback request a maximum of **three times** . If the callback request still fails to be sent, ApsaraVideo VOD discards the request.

    
  

  

* MNS callback

  * When the MNS callback method is used, ApsaraVideo VOD determines that an MNS callback is successful when the message is pushed to the MNS queue.

    
  
  * If the message cannot be pushed to the queue due to incorrect configurations (for example, ApsaraVideo VOD is not authorized to access MNS, the MNS endpoint is not a public endpoint, or the queue name is incorrect), ApsaraVideo VOD retries the push two more times. ApsaraVideo VOD attempts to push the message to the queue a maximum of **three times** . If the message still fails to be pushed to the queue, ApsaraVideo VOD discards the message.

    
  

  



**Note**

When a callback fails, ApsaraVideo VOD retries the callback every **1 second** . If a maximum of three attempts fail, ApsaraVideo VOD stops retrying and discards the callback message. We recommend that you use MNS callbacks because they are more reliable than HTTP callbacks. Almost all MNS callbacks can succeed if they are configured properly.

FAQ 
------------------------

If you encounter any problems when you use the event notification feature, see [FAQ about event notification](/intl.en-US/FAQ/FAQ about event notifications.md).
