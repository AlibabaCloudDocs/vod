Forcible redirect 
======================================

You can use the forcible redirect feature to redirect the original requests from a client to edge nodes as HTTP or HTTPS requests. This topic describes how to configure the forcible redirect feature.

Prerequisites 
----------------------------------

An HTTPS certificate is configured before you configure the forcible redirect feature. For more information, see [Enable HTTPS secure acceleration](/intl.en-US/User Guide/Domain management/Set HTTPS security acceleration/Enable HTTPS secure acceleration.md).

Feature description 
----------------------------------------

If you have enabled HTTP secure acceleration for domain names for CDN, you can forcibly redirect the original requests from users by customizing the redirect type.

Assume that you set the Redirection parameter to **HTTP -\> HTTPS** . When a client initiates an HTTP request, the server returns a 301 response to redirect the request to the HTTPS version of the web page. The following figure shows an example.

![Example](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7583888061/p181993.png)

Procedure 
------------------------------

1. Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

   

2. In the left-side navigation pane of the ApsaraVideo VOD console, find **Configuration Management** .

   

3. Choose **CDN Configuration \> Domain Names** . The Domain Names page appears.

   

4. Find the domain name that you want to configure and click **Configure** .![Select a domain name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7583888061/p181835.png)

   

5. Click **HTTPS** . Then, click **Modify** in the **Forced Redirection** section **.** 

   ![Forced Redirection](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7583888061/p181990.png)
   

6. Select a **redirect type** .

   ![Redirect type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7583888061/p181991.png)The following table describes the redirect types.
   

   | Redirect type  |                                                  Description                                                  |
   |----------------|---------------------------------------------------------------------------------------------------------------|
   | Default        | Both HTTP and HTTPS requests are supported.                                                                   |
   | HTTPS -\> HTTP | The requests from a client to edge nodes are forcibly redirected as HTTP requests.                            |
   | HTTP -\> HTTPS | The requests from a client to edge nodes are forcibly redirected as HTTPS requests to ensure access security. |

   

7. Click **OK** .

   

   



