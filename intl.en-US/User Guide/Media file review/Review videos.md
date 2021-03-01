# Review videos

ApsaraVideo VOD provides the automated review and manual review features for you to review uploaded files. Before you publish videos, you can review the videos to ensure that the video content is compliant. You can bring inappropriate videos offline before they are published. This avoids or minimizes the adverse effects of these videos.

## Terms

-   Automated review: You can configure automated review templates on the Review Settings page. For more information, see [Configure an automated review template](/intl.en-US/User Guide/Media file review/Configure a machine review template.md).The automated review feature is supported only in the Singapore and China \(Shanghai\) regions. To use the automated review feature in the Singapore region, you must [submit a ticket](https://ticket-intl.console.aliyun.com).

-   Manual review: Manual reviews are performed by personnel. These reviews have a higher priority than automated reviews.

## Procedure

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Review** \> **Content Moderation**.

3.  On the To Be Reviewed page, select the video that you want to review.

    You can filter videos by upload date. For example, you can select **All** or **Custom Time**. You can also filter videos by video name or video ID.

4.  Start a review.

    1.  Start an automated review.

        -   Click **Automated Review** in the Actions column of an unreviewed video. The video is reviewed based on the default review template. If you have configured no review templates, the preset template is used. For information about how to configure a review template, see [Configure an automated review template](/intl.en-US/User Guide/Media file review/Configure a machine review template.md).
        -   Click **Re-review** in the Actions column of a video that failed to pass a review. The video is reviewed based on the default review template. If you have configured no review templates, the preset template is used. For information about how to configure a review template, see [Configure an automated review template](/intl.en-US/User Guide/Media file review/Configure a machine review template.md).
        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8150888061/p172468.png)

    2.  Wait until the automated review is complete.

        -   **Under Review** is displayed in the Machine Review Status column of the video that is being reviewed for the first time.
        -   **Re-review** is displayed in the Machine Review Status column of the video that is being reviewed again.
        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9150888061/p172471.png)

    3.  View the review status after the automated review is complete.

        If **Successful review** is displayed in the Machine Review Status column, the automated review is complete.

    1.  Start a manual review.

        To perform a manual review, use one of the following methods:

        -   Click **Human review** in the Actions column of a video. View the video snapshots that appear and click **Passed** or **Blocked** as needed.
        -   Click **Details** in the Actions column of a video. On the Video review details page, preview the video and click **Passed** or **Blocked** as needed. You can also view the automated review results and manual review results on the Video review details page.
        -   On the To Be Reviewed page, select one or more videos and click **Passed** or **Blocked** at the bottom of the page to manually review the selected videos at a time.
        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9150888061/p172473.png)

    2.  View the review status after the manual review is complete.

        If **Reviewed** is displayed in the Human Review Status column and **Passed** or **Blocked** is displayed in the Final Review Result column, the review is complete.


