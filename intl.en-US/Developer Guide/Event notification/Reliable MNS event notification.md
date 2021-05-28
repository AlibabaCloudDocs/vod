# Reliable MNS event notification

Alibaba Cloud Message Service \(MNS\) is a distributed messaging service that features scalability, high efficiency, reliability, security, and availability. This topic describes the precautions, configuration process, and message consumption of reliable MNS event notifications.

-   MNS provide queues to support a large number of concurrent access requests from multiple producers and consumers. After a message is pulled from a queue, the message cannot be pulled again for a specified duration of time. A message is invisible for a period of time after it is consumed. If you do not manually delete the message, it can be consumed again. For more information, see [What is MNS?]()
-   ApsaraVideo VOD supports event notifications for multiple storage regions. You can configure the callback methods and callback URLs for event notifications for each region. You can upload videos to different storage regions. After a video is processed \(for example, uploaded or transcoded\), ApsaraVideo VOD notifies you of the processing results based on the callback configurations for the regions and pushes messages to your MNS queues.

## Precautions

-   When the MNS callback method is used, if a message cannot be pushed to an MNS queue because ApsaraVideo VOD is not authorized to access MNS, if the MNS endpoint is not a public endpoint, or if the queue name is incorrect, ApsaraVideo VOD retries the push two more times. ApsaraVideo VOD attempts to push the message to the queue a maximum of three times. If the message still fails to be pushed to the queue, ApsaraVideo VOD discards the message.
-   Recommended regions for message queues:
    -   If your video is stored in a mainland China region, we recommend that you push the message to a queue in the **China \(Shanghai\)** region. If you push the message to a queue in a region other than **China \(Shanghai\)**, you may experience a short delay.
    -   If your video is stored in a region such as Singapore or Indonesia that is outside mainland China, we recommend that you create or use a message queue in that region.

        For example, if your video is stored in the India \(Mumbai\) region, you must create or use a queue in the **India \(Mumbai\)** region.


## Configure the reliable MNS event notification

1.  Log on to the [Alibaba Cloud Management Console](https://home.console.aliyun.com) and go to the [Cloud Resource Access Authorization](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunVODDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//vod.console.aliyun.com/%22%2C%20%22Service%22%3A%20%22VOD%22%7D) page to authorize ApsaraVideo VOD to access your cloud resources. Click **Confirm Authorization Policy** in the lower part of the page.

    ![Cloud Resource Access Authorization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9466301161/p178869.png)

2.  Log on to the [MNS console](https://mns.console.aliyun.com/?spm=a2c4g.11186623.2.19.20d83502Ek9Nnu) to create a queue or use an existing queue. For more information, see [t1835614.md\#]().

    **Note:** If your video is stored in a mainland China region, we recommend that you select **China \(Shanghai\)** from the drop-down list.

3.  Call the [SetMessageCallback](/intl.en-US/API Reference/Global configurations/Event notifications/SetMessageCallback.md) operation to configure the event notification.

    -   The `MnsEndpoint` parameter specifies the public endpoint of the queue. You can obtain the endpoint by clicking **Get Endpoint** in the upper-right corner of the Queues page.
    -   The `EventTypeList` parameter specifies the event type. For more information, see the "Event types" section in [Overview](/intl.en-US/Developer Guide/Event notification/Overview.md).
4.  After you complete the event notification configurations, log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/#/overview) and upload a video to trigger an event notification.

5.  When the conditions for generating a callback event are met, ApsaraVideo VOD pushes a callback message to the queue that you specified. In the MNS console, click **Receive Message** in the Action column corresponding to the queue and view the message in the Receive Message dialog box.


## Message consumption

After you complete the configurations, you can use code to consume messages.

-   For information about how to consume messages by using Java code, see [Manage queues]().
-   For information about how to consume messages by using Python code, see [Manage queues]().
-   For information about how to consume messages by using C\# code, see [Manage queues]().
-   For information about how to consume messages by using PHP code, see [Manage queues]().
-   For other languages, you can call the [ReceiveMessage]() operation to receive messages and the [DeleteMessage]() operation to delete messages. For more information, see [Call MNS APIs]().

MNS queues support a large number of concurrent access requests from multiple producers and consumers. After a message is pulled from a queue, the message cannot be pulled again within a specified period of time. A message is invisible for a period of time after it is consumed. You must manually delete the message. Otherwise, the message can be consumed again.

