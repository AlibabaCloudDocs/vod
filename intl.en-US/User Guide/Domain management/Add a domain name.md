# Add a domain name

If you want to use ApsaraVideo VOD to accelerate the delivery of content on a specific website, you must add the domain name that you want to accelerate and specify the website as the origin server. This topic describes how to add a domain name to ApsaraVideo VOD.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, click **Add Domain Name**.

    ![Click Add Domain Name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6551888061/p182101.png)

5.  On the Add Domain Name page, specify the **Domain Name**, **Type**, **Port**, and **Acceleration Region** parameters.

    ![Set the domain name parameters](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6551888061/p182103.png)

    |Parameter|Value|Description|
    |---------|-----|-----------|
    |**Domain Name**|None|Enter the domain name that you want to accelerate, for example, `example.com`. Note the following information:

    -   You can use a subdomain name as the domain name for CDN, for example, `cdntest.example.com`.
    -   ApsaraVideo VOD does not support wildcard domain names, for example, `example.example.com`.
    -   You cannot add duplicate domain names to ApsaraVideo VOD. If a **DomainAlreadyExist** error is displayed, check whether the domain name is added to other cloud services such as ApsaraVideo Live, Dynamic Route for CDN, Secure CDN, or video surveillance system. You can also [submit a ticket](https://selfservice.console.aliyun.com/ticket/createIndex).
    -   You can add a maximum of 20 domain names to ApsaraVideo VOD for each Alibaba Cloud account. To increase the quota, [submit a ticket](https://selfservice.console.aliyun.com/ticket/createIndex).
    -   Content that is served from the domain must comply with the limits of ApsaraVideo VOD. For more information, see [Domain verification]().
**Note:** The specified subdomain names must belong to the same Alibaba Cloud account. When you add a domain name, Alibaba Cloud CDN verifies the ownership of the domain name. If the specified subdomain names belong to different accounts, an error message appears. For technical support from Alibaba Cloud, [submit a ticket](https://selfservice.console.aliyun.com/ticket/createIndex). |
    |Type|**OSS Domain Name**|Select a default bucket for ApsaraVideo VOD.|
    |**Port**|None|Select a port based on your business requirements.

    -   Port 80

Allows you to access resources over HTTP.

    -   Port 443

Allows you to access resources over HTTPS. |
    |**Acceleration Region**|**Mainland China \(ICP Filing Required\)**|If you select **Mainland China \(ICP Filing Required\)**, you must apply for an Internet content provider \(ICP\) license from the Ministry of Industry and Information Technology \(MIIT\). For more information, see [Apply for an Internet Content Provider \(ICP\) number for an accelerated domain name](/intl.en-US/Product Introduction/Limits.md).|
    |**Global \(ICP Filing Required\)**|If you select **Global \(ICP Filing Required\)**, you must apply for an ICP license from MIIT. For more information, see [Apply for an Internet Content Provider \(ICP\) number for an accelerated domain name](/intl.en-US/Product Introduction/Limits.md).|
    |**Outside Mainland China \(ICP Filing Not Required\)**|If you select **Outside Mainland China \(ICP Filing Not Required\)**, you do not need to apply for an ICP license from MIIT.|

6.  Click **Submit**.

    ![Success message](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6551888061/p182109.png)

    After your domain name is approved, you can view the domain name on the **Domain Names** page in the ApsaraVideo VOD console. If the domain name is in the Enabled state, the domain name is added to ApsaraVideo VOD.

    **Note:**

    -   If the review of your domain name is urgent, [submit a ticket](https://selfservice.console.aliyun.com/ticket/createIndex).
    -   If the origin server is an ECS instance or an OSS bucket, less time is required to verify the ownership of the domain name.
    -   After a domain name is added to ApsaraVideo VOD, Alibaba Cloud CDN assigns a canonical name \(CNAME\) to the domain name. The Alibaba Cloud CDN service takes effect only after you configure a CNAME record for the domain name. For more information, see [Configure a CNAME record in Alibaba Cloud DNS](/intl.en-US/User Guide/Domain management/CNAME configuration/Configure CNAME on HICHINA and Alibaba Cloud DNS.md).

