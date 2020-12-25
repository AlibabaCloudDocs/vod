# Manage workflows

Workflows apply when you process multiple tasks of media files. You can transcode, review, and attach tags to media files. You can also check duplicate video content, create snapshots, and create frame animations. Serial configuration and parallel configuration are supported based on original files. This topic describes how to manage workflows.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **Media Processing** \> **Workflows**.

4.  On the Workflows page, click **Add Workflow**.

    ![Click Add Workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5980888061/p183044.png)

5.  Configure a workflow topology.

    -   Specify the **Workflow Name** parameter.
    -   Add a workflow.

        Click the **Add** icon to add a workflow.

        ![Add a workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5980888061/p183050.png)

    -   Delete a workflow.

        Click the Delete icon to delete a workflow. If you delete a parent node, all of its child nodes are deleted, as shown in the following figure.

        Before you delete a parent node

        ![Before you delete a parent node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5980888061/p183054.png)

        After you delete a parent node

        ![After you delete a parent node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6980888061/p183055.png)

    -   Modify a workflow.

        Click the Edit icon to modify a workflow.

        ![Modify a workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6980888061/p183058.png)

        -   Parent node

            In the dialog box that appears, modify the **Node Name** parameter and template settings, and then click **OK**. The following figure uses Review as an example.

            ![Parent node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6980888061/p183059.png)

        -   Child node

            In the dialog box that appears, modify the **Node Name** parameter and template settings. In addition, you need to specify the **Performs Conditional** parameter. By default, this parameter is set to **All Conditions**. Then, click **OK**. The following figure uses Transcode as an example.

            ![Child node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6980888061/p183064.png)

6.  Click **Confirm**.

    Workflows can be used to upload media files.


