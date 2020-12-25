# Manage video categories

ApsaraVideo VOD allows you to categorize videos so that you can efficiently retrieve and manage videos.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **Media Management** \> **Categories**.

4.  On the **Audio and Video / Image Category** tab of the Categories page, click **Add Level 1 Category**.

    By default, the category tree is empty. You can modify category trees based on your business requirements.

    **Note:** A maximum of three levels of categories can be added in each category tree and a maximum of 100 categories can be added in each level.

    You can also use keyboard shortcuts to add or delete a parent category or child category.

    -   Enter: adds a same-level category.
    -   Alt+Enter: adds a category. A maximum of three levels are supported.
    -   Delete: deletes a category.
    You can also manage categories by calling API operations. For more information, see [Add categories](/intl.en-US/API Reference/Media management/Media Category/AddCategory.md).

5.  On the **Short Video Material Category** tab of the Categories page, move the pointer over the first-level category, and click the **Add** icon.

    MV, Face Sticker, Dynamic Sticker, Subtitle, and Font are default first-level categories. These categories cannot be modified. You can create a category tree for each first-level category.

    ![Short Video Material Category tab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8850888061/p173850.png)

    **Note:** A maximum of two levels of categories can be added in each category tree and a maximum of 100 categories can be added in each level.

    You can also use keyboard shortcuts to add or delete a parent category or child category.

    -   Enter: adds a same-level category.
    -   Alt+Enter: adds a child category. A maximum of two levels are supported.
    -   Delete: deletes a category.

After you create a classification tree, you can use it to manage videos in the following scenarios:

-   Select a category when you upload a video or modify the category on the video details page.
-   In the video list, query videos by specifying the **Category** parameter.

