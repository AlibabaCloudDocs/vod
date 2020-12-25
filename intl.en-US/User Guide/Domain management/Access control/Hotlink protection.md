# Hotlink protection

Hotlink protection requires you to configure a referer whitelist or blacklist to identify and filter users. This helps you restrict access to Content Delivery Network \(CDN\) nodes and improve service security. This topic describes how to configure referer-based hotlink protection.

Hotlink protection uses an HTTP referer header to track request sources and identify requests.

Hotlink protection provides a referer whitelist or a referer blacklist. After a user sends a request to a CDN node, the node authenticates the user identity based on the preset referer whitelist or blacklist. If the request passes the authentication, the user can access the requested resources. If the request fails the authentication, a 403 HTTP response code is returned.

**Note:**

-   Hotlink protection is optional. This feature is disabled by default.
-   The blacklist and whitelist are mutually exclusive and cannot be enabled at the same time.
-   After you configure hotlink protection, wildcard domains are automatically supported. For example, if you enter `a.com`, the domain that takes effect is `*.a.com`. Hotlink protection takes effect on all domains that match \*.a.com.
-   You can specify whether to allow requests with an empty referer header to access resources. If you allow the access, users can directly access resources by entering the resource URL in the address bar of a browser.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Click **Resource Access Control**.

6.  Click the **Referer-based Anti-Leech** tab and then **Modify**.

    ![Modify configurations](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1593888061/p181673.png)

7.  Set the **Method** parameter, enter referers, and then click **OK**.

    ![Configuration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2593888061/p181675.png)

    The following table describes the types of referer-based hotlink protection.

    |Type|Description|
    |----|-----------|
    |**Blacklist**|All requests that are sent from domains in the blacklist to access resources are denied.|
    |**Whitelist**|Only requests that are sent from domains in the whitelist to access resources are allowed. Requests from other domains are denied.|


