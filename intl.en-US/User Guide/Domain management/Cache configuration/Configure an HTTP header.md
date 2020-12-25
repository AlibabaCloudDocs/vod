# Configure an HTTP header

You can define the operation parameters of an HTTP transaction by configuring an HTTP header. This topic describes how to create an HTTP header.

HTTP headers are components of the header section of request and response messages that are transmitted over HTTP. HTTP headers define the resources that are being requested and the behavior of clients or servers.

**Note:**

-   The configurations of the HTTP header for a domain name for Content Delivery Network \(CDN\) affect how a client program responds to all the requests that are destined for the domain name. The client program can be a browser. The header configurations do not affect the cache server.
-   You are not allowed to configure HTTP headers for wildcard domain names.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Click **Cache**.

6.  Click the **HTTP Header** tab. Then, click **Add**.

    ![Add an HTTP header](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6263888061/p181565.png)

7.  Set the **Parameter** and **Value** parameters and click **OK**.

    ![Add](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6263888061/p181590.png)

    The following table describes the parameters.

    |Parameter|Description|Example|
    |:--------|:----------|-------|
    |Content-Type|Specifies the type of the content that is returned to the client program.|image|
    |Cache-Control|Specifies the cache policy that the client program follows for requests and responses.|no-cache|
    |Content-Disposition|Specifies the default file name that is provided by the client program when the requested content is saved as a file.|123.txt|
    |Content-Language|Specifies the language of the intended audience for the content that is returned to the client program.|zh-CN|
    |Expires|Specifies the expiration time of the content that is returned to the client program.|Wed, 21 Oct 2015 07:28:00 GMT|
    |Access-Control-Allow-Origin|Specifies the origins from which cross-origin requests are allowed.|\* **Note:** You can enter `*` to specify all the domain names. You can also enter a full domain name, such as `www.aliyun.com`. |
    |Access-Control-Allow-Headers|Specifies the fields that are allowed in cross-origin requests.|X-Custom-Header|
    |Access-Control-Allow-Methods|Specifies the request methods that are allowed for cross-origin requests.|POST and GET**Note:** To add the POST and GET methods together, separate them with a comma \(,\). |
    |Access-Control-Max-Age|Specifies the time to live \(TTL\) during which the response can be cached for a preflight request that is initiated by the client program for a particular resource. Unit: seconds.|600|
    |Access-Control-Expose-Headers|Specifies the headers that can be exposed as part of the response.|Content-Length|


