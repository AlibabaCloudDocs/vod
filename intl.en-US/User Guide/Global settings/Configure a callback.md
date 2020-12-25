# Configure a callback

ApsaraVideo for VOD immediately notifies you of the progress and status of each processed video in real time. For example, videos are uploaded and transcoded.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **Media Processing** \> **Callback**.

4.  On the Callback page, click **Modify**.

    ![Click Modify](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2080888061/p182662.png)

5.  In the Callback dialog box, specify the required parameters, and click **OK**.

    Valid values of Callback Method:

    -   HTTP Request

        Specify a callback URL based on your needs. This parameter cannot exceed 256 bytes in length. Select events.

    -   MNS Queue

        Select a region, queue, and events.

    **Note:** After the callback events you selected are processed, ApsaraVideo for VOD notifies you by pushing events to a specified queue. For more information about how to implement this notification, see [MNS queues](/intl.en-US/Developer Guide/Event notification/Instructions for use.md).

    ![Callback dialog box](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2080888061/p182671.png)


