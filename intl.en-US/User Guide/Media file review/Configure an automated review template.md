# Configure an automated review template

ApsaraVideo VOD allows you to configure automated review templates. Automated review templates that applicable to your business can facilitate video review.

## Procedure

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Review** \> **Settings**.

3.  On the Review Settings page, click the **Review Configuration** tab. In the **Process** section, click **Modify**. In the Review Process dialog box, select a review process and click **OK**.

    Two review processes are available: Review After Publish and Review Before Publish. The default process is Review After Publish.

    ![Review Process dialog box](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5050888061/p173499.png)

4.  In the **Intelligent Review** section of the **Review Configuration** tab, click **Modify**. In the Configure Intelligent Review dialog box, select an automated review template and click **OK**.

    You can create an automated review template on the **Add Intelligent Review Template** page.

    ![Configure Intelligent Review dialog box](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5050888061/p173515.png)


## Create an automated review template

You can use one of the following methods to go to the **Add Intelligent Review Template** page.

-   In the **Intelligent Review** section of the **Review Configuration** tab, click **Modify**. In the **Configure Intelligent Review** dialog box, click **Add New Template**.

    ![Method 1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5050888061/p173529.png)

-   On the **Review Template** tab of the **Review Setting** page, click **Add**.

    ![Method 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5050888061/p173533.png)


The following table describes the parameters on the **Add Intelligent Review Template** page.

|Parameter|Description|
|---------|-----------|
|Template Name|Specify the name of your template to identify the template.|
|Review Type|The review types include pornography detection, terrorism detection, ad violation detection, logo detection, undesirable content detection, and audio anti-spam.-   The results of pornography detection include the following categories: porn, sexy, and normal.
-   The results of terrorism detection include the following categories: blood and gore, explosion, outfit, logo, weapon, politics, violence, crowd, parade, car crash, flag, location, and others.
-   The results of ad violation detection include the following categories: politics, porn, abuse, terrorism, prohibited content, junk content, spam, psoriasis ads, QR code, mini program code, other ads, and normal.
-   The results of log detection include the following categories: trademark, controlled logo, and normal.
-   The results of undesirable content detection include the following categories: picture-in-picture \(PiP\), smoking, streaming during driving, normal, and no image such as black screen and white screen.
-   The results of audio anti-spam include the following categories: junk information, ads, politics, terrorism, abuse, porn, spam, violation, custom, and normal. For example, you can set custom keywords.

**Note:** The automated review feature in the Singapore region supports only the pornography, terrorism, and undesirable content detection. |
|Review Scope|Valid values: Cover, Name, and Video.**Note:**

-   The number of video thumbnails cannot exceed five.
-   The size of the video title and a bullet message cannot exceed 128 bytes.
-   The duration of the video cannot exceed 6 hours. |
|Review Content|Valid value: Image.|
|Auto Block|If you enable this feature, videos that contain illicit content will be automatically blocked. Enabling this feature may result in high risks. Proceed with caution.|

![Add Intelligent Review Template page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5050888061/p173645.png)

