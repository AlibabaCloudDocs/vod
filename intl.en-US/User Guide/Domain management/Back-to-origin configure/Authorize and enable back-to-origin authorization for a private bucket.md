# Authorize and enable back-to-origin authorization for a private bucket

This topic describes how to enable back-to-origin authorization for a private bucket.

You must grant permissions to domain name for CDN and enable the Back-to-Origin of Private Bucket feature before the domain name can access a private OSS bucket. You can also use the referer-based hotlink protection and URL authentication features provided by ApsaraVideo VOD to ensure resource security.

**Note:**

-   After back-to-origin is authorized and enabled for a specific domain name for CDN, the domain name can access the resources in your private bucket. Proceed with caution. If the resources in the private bucket are not suitable to be used as the back-to-origin content of the CDN domain, do not authorize or enable the feature.
-   If your domain name for CDN uses a private bucket as its origin, do not disable the back-to-origin feature.
-   If your website is at risk of attacks, purchase the Anti-DDoS Pro service and do not authorize or enable back-to-origin of private buckets.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Grant permissions to the CDN domain name. If you have granted permissions, skip this step.

    1.  In the left-side navigation pane of the domain details page, click **Back-to-origin**. In the **Back-to-Origin of Private Bucket** section, click **Authorize**.

        ![Click Authorize](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7254319061/p180601.png)

    2.  Click **Confirm Authorization Policy**.

        ![Click Confirm Authorization Policy.](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7254319061/p180603.png)

6.  In the left-side navigation pane of the domain details page, click **Back-to-origin**. In the Back-to-Origin of Private Bucket section, turn on the **Back-to-Origin of Private Bucket** switch.

    ![Enable private bucket back-to-origin authorization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7254319061/p180606.png)


