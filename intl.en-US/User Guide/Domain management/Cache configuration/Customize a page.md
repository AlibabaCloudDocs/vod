# Customize a page

You can customize different pages to redirect to when your web requests fail. When the request to access a web page fails, you are redirected to the custom page. This topic describes how to customize an error page.

Alibaba Cloud provides two types of error pages for the status codes: default page and custom page. The 404 status code is used as an example to describe the differences between a default page and a custom page.

-   Default page: When the HTTP response includes the 404 status code, the server returns the default 404 Not Found page.
-   Custom page: When the HTTP response includes the 404 status code, the server returns the custom page. You must specify a full URL for the custom page.

**Note:**

-   You can join the NotFound project by using the default pages for the 404 status code that are provided by Alibaba Cloud. Default pages for the 404 status code are considered as Alibaba Cloud public resources and are free of charge.
-   Custom pages are considered as personal resources and you are charged based on the specified billing rules.
-   For more information about the reason why 404 pages are returned, see [Why does the 404 Not Found page appear?](https://www.alibabacloud.com/help/doc-detail/27132.html)

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Click **Cache**. Then, click the **Custom Error Pages** tab and then **Add**.

    ![Add custom pages](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9653888061/p181519.png)

6.  Select an error code, enter a custom URL, and then click **OK**.

    ![Add](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9653888061/p181521.png)

    If you set the error code to 404, Alibaba Cloud provides default pages for the 404 status code. You can select **Join NotFound Project**. Then, click **OK**. Default pages for the 404 status code are considered as Alibaba Cloud public resources and are free of charge.

    ![Default pages for the 404 status code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9653888061/p181524.png)


