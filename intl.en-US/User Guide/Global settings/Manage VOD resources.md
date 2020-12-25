# Manage VOD resources

ApsaraVideo VOD allows you to store VOD resources by using OSS buckets. You do not need to activate Object Storage Service \(OSS\). A VOD environment is built after videos are uploaded, stored, transcoded, edited, and published.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **Media Management** \> **Storage**.

    Object Storage Service \(OSS\) provides a dedicated bucket for you to store VOD resources. You can upload media resources to the bucket and manage the resources without the need to configure the bucket. The default storage region is China \(Shanghai\). ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6550888061/p172485.png)

    You can also specify another region to store VOD resources.![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6550888061/p172486.png)

4.  Click **Manage** in the **Actions** column.

    ![Manage VOD resources](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6550888061/p173687.png)

5.  In the Permissions section, click **Modify**. In the Modify dialog box, modify the read and write permissions of the bucket.

    By default, Read-write Permission is set to Private Read and Write. This ensures the security of your VOD resources. You can specify this parameter based on your needs.

    Buckets are provided by OSS. For more information, see [What is OSS?](/intl.en-US/Product Introduction/What is OSS?.md)

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6550888061/p172487.png)

    The following table describes the values of read and write permissions.

    |Permission Type|Description|
    |---------------|-----------|
    |Private Read and Write|Only the bucket owner and authorized RAM users can read, write, and delete the objects in the bucket. Other users cannot access the objects in the bucket without authorization.|
    |Public Read and Private Write|Only the bucket owner and authorized RAM users can write and delete the objects in the bucket. Everyone \(including anonymous users\) can read the objects in the bucket.|
    |Public Read and Write|All users \(including anonymous users\) can read, write, and delete the objects in the bucket. The bucket owner must pay all the fees incurred by these operations.|

6.  Set the back-to-origin domain name.

    If multiple domain names are configured for an OSS bucket, click **Set as Default** in the Origin Domain Name section of the bucket details page. This ensures that playback callbacks are sent to the default domain name.

    For information about how to add a back-to-origin domain name, see [Domain Verification]().

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6550888061/p172488.png)


