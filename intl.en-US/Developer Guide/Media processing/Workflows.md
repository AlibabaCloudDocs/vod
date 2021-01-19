Workflows 
==============================

ApsaraVideo VOD provides a variety of media processing capabilities, such as transcoding, snapshot taking, and automated review. To make media processing capabilities easier to use, ApsaraVideo VOD provides workflow capabilities that allow you to customize media processing workflows in the console. This topic describes the architecture, configuration, and usage of workflows.

Overview 
-----------------------------

Workflows are designed to streamline and instantiate most media processing features. You can customize workflows in advance to process videos in a one-stop manner instead of repeatedly calling API operations. Workflows also provide abundant condition judgment mechanisms. These mechanisms allow you to customize the conditions that trigger the next node, which facilitates flexible scenario-based media processing.

Architecture 
---------------------------------

**Workflow examples** 

* **"Review + Transcoding" serial workflow** 

  This workflow indicates a serial process where videos you upload are reviewed and then transcoded. For more information, see the ["Review + Transcoding" serial workflow](#section-54k-ze2-rch) section in this topic.![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4478301161/p178288.png)
  

* **"Review + Transcoding" parallel workflow** 

  This workflow indicates a process where videos you upload are reviewed and transcoded in parallel.

  ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4478301161/p178289.png)
  

* **"Mezzanine file distribution + Transcoding" parallel workflow** 

  This workflow indicates a process where the video mezzanine file you upload is distributed while it is being transcoded based on the transcoding nodes you configure.

  ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4478301161/p178290.png)
  




Procedure 
------------------------------

The following figure shows the procedure of a workflow.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4478301161/p178291.png)



Preparation: Configure a workflow in the console.

1. A user obtains an upload credential and specifies the workflow. ApsaraVideo VOD returns the upload credential.

   

2. The user initiates video upload.

   

3. After videos are uploaded, the workflow is triggered.

   

4. The workflow engine of ApsaraVideo VOD automatically performs media processing and video AI operations based on the workflow configuration.

   




Configuration methods 
------------------------------------------

You can configure workflows on the **[Workflows](https://vod.console.aliyun.com/settings/workflow/list#/settings/workflow/list)** page of the console.

Usage 
--------------------------

You can specify a workflow when you obtain an upload credential.
**Notice**

You can upload a video by using a workflow or an original template group, but you cannot use both of the methods. If you use a workflow to upload files by specifying the workflow ID, make sure that the ID is valid. For more information, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md).

**"Review + Transcoding" serial workflow** 
---------------------------------------------------------------

The "Review + Transcoding" serial workflow is used in the following example to show the configuration of a workflow. The workflow indicates that an uploaded video is reviewed first, and then transcoded if it passes the review.

1. Go to the **[Workflows](https://vod.console.aliyun.com/settings/workflow/list#/settings/workflow/list)** page of the ApsaraVideo VOD console.

   

2. Click **Add Workflow** . On the Add Workflow page, enter a workflow name.

   

3. Click the **+** icon to the right of Start and select Review. An automated review node is added.![Add a node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4478301161/p184620.png)

   

4. After the node is added, click the **Edit** icon to the right of Review. In the dialog box that appears, select a review template, and then click OK.![Add a review template](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4478301161/p184621.png)

   

5. Click the **+** icon to the right of Review and select Transcode to add a transcoding node after the review node.

   

6. After the node is added, click the **Edit** icon to the right of Transcode. In the dialog box that appears, configure Performs Conditional.

   **Notice**

   This parameter indicates the condition that the parent node must meet to trigger the current node.

   In this example, videos must pass the review before they can be transcoded. Therefore, Performs Conditional is set to Parent Node Approval Passed. You must also specify the transcoding template group that you want to use.
   ![Parent Node Approval Passed](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4478301161/p182112.png)

   The following table lists all conditions.
   

   |               Scenario               |              Condition               |                                                                                                  Description                                                                                                  |
   |--------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | The parent node is a Review node.    | All Conditions                       | The current node can be executed under all conditions.                                                                                                                                                        |
   | The parent node is a Review node.    | Parent Node Approval Passed          | The node is executed only if the video passes the review.                                                                                                                                                     |
   | The parent node is a Review node.    | Parent Node Audit Processing Failed  | The node is executed only if the video mezzanine file fails the review. Select this condition if you are aware that the source video file is damaged.                                                         |
   | The parent node is a Review node.    | Parent Node Video Violation Blocking | The node is executed only if the video fails the review and is blocked due to a violation. Select this condition if you want to transcode the blocked video into one with lower definition for manual review. |
   | The parent node is a Transcode node. | All Conditions                       | The current node can be executed under all conditions.                                                                                                                                                        |
   | The parent node is a Transcode node. | Parent Node Transcoding Succeeded    | The node is executed only if the video transcoding is complete.                                                                                                                                               |
   | The parent node is a Transcode node. | Parent Node Transcoding Failed       | The node is executed only if the video transcoding fails.                                                                                                                                                     |

   

7. After you configure the workflow, click **Confirm** to generate a workflow ID. Record the workflow ID for subsequent upload.![Workflow configured](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4478301161/p182113.png)

   




**"Review + Transcoding" parallel workflow** 
-----------------------------------------------------------------

To create a workflow that implements review and transcoding in parallel, you can click the + icon to the right of Start and select Review to create a Review node. Then, click the + icon to the right of Start again and select Transcode to create a Transcode node.
**Notice**

After the nodes are created, click the Edit icons to the right of the two nodes and select templates as described in the preceding example.
