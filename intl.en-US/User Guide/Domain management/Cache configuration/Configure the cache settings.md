# Configure the cache settings

You can create cache expiration rules to define the time to live \(TTL\) value of static resources. You can also specify a priority for each cache expiration rule. This improves the cache hit rate of Content Delivery Network \(CDN\) nodes. After a resource expires, it is automatically deleted from the CDN node and re-cached on the CDN node from the origin server. This topic describes cache expiration rules for resources on CDN nodes and how to create a cache expiration rule.

## Features

-   If you have not set a cache expiration rule on your origin server or CDN nodes, the CDN nodes use the default TTL value of 3,600 seconds to expire cached resources. You can modify the TTL value after you add a domain name for CDN. The amount of back-to-origin traffic and the fees incurred vary based on the TTL value. We recommend that you set a TTL value based on your business requirements. A small TTL value may cause CDN nodes to frequently redirect requests to the origin server and increase the amount of network traffic that is consumed by the origin server.
-   If an origin server has a cache expiration rule configured, the cache expiration rule on the CDN node has a higher priority than the cache expiration rule that is configured on the origin server. If an origin server has no cache expiration rule configured, you can set a cache expiration rule by directory or by file name extension. You can set a full-path cache expiration rule.
-   A CDN node may remove the cached files before they expire if they are not frequently updated.
-   If a client request carries the If-Match header and the response from the origin server carries the ETag header, the CDN node directly returns the requested resources to the client when the value of the If-Match header is the same as the value of the ETag header. When the value of the If-Match header is different from the value of the ETag header, the CDN node retrieves the latest version of the requested resource from the origin server and then returns it to the client. At the same time, the resources that are cached on the CDN node are replaced by the retrieved version. The matching rule between the If-Match header and the ETag header has a higher priority than the cache expiration rule that is configured on CDN nodes.

When you update a resource file on your origin server, we recommend that you include the version number in the name of the update file instead of using the same name as the existing resource file. For example, you can name two update files img-v1.0.jpg and img-v2.1.jpg. You can then set a cache expiration rule for the resource file. The following figure shows the cache expiration rule for resources on CDN nodes.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7953888061/p172535.png)

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Click **Cache**.

6.  Click the **Cache Validity** tab and then click **Add**.

    ![Cache expiration time](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7953888061/p181616.png)

7.  To configure a cache rule, set the Type parameter to **Folder** or **File Extension**.

    ![Add](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7953888061/p181618.png)

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Type**|    -   Folder: specifies the resources that are cached in the specified directory.
    -   Filename Extension: specifies the resources that are cached in files with the specified file name extensions. |
    |**Address**|    -   If you select Folder, enter a single path that starts with a slash \(/\), for example, /directory/aaa. You can enter a full directory.
    -   If you set Type to File Extension, use commas \(,\) to separate multiple file name extensions, for example, `JPG,TXT`. |
    |**Validity Period**|The TTL value for the cached resources. A CDN node can cache resources for up to three years. We recommend that you set this parameter based on the following rules:     -   Specify a TTL value of one month or longer for static files such as images and applications that are not frequently updated.
    -   Specify a TTL value based on your actual workloads for static files such as JavaScript and CSS files that are frequently updated.
    -   Specify a TTL value of 0 seconds to disable caching for dynamic files such as PHP, JSP, and ASP files. |
    |**Weight**|The priority of the cache expiration rule. **Note:**

    -   The value must be an integer from 1 to 99. A higher value specifies a higher priority. A rule with a higher priority prevails over rules with lower priorities.
    -   We recommend that you do not set the same priority for different rules. If different rules have the same priority value, one of these rules is applied at random.
    -   After a cache expiration rule takes effect, other rules are not applied.
For example, if you set the following rules for `example.aliyun.com`, Rule 1 is preferentially applied over the other two rules:

    -   Rule 1: the Type parameter is set to File Extension, the Address parameter is set to jpg,png, the Validity Period parameter is set to one month, and the Weight parameter is set to 90.
    -   Rule 2: the Type parameter is set to Folder, the Address parameter is set to /www/dir/aaa, the Validity Period parameter is set to 1 hour, and the Weight parameter is set to 70.
    -   Rule 3: the Type parameter is set to Folder, the Address parameter is set to /www/dir/aaa/example.php, the Validity Period parameter is set to 0 seconds, and the Weight parameter is set to 80. |

8.  Click **OK**.


