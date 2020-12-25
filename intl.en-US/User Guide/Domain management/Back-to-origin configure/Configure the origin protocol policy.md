# Configure the origin protocol policy

Assume that a client requests resources that are not cached on a Content Delivery Network \(CDN\) node. The node retrieves these resources from the origin server based on the origin protocol policy and caches these resources on the node. If the client sends an HTTP request to retrieve resources that are not cached on a CDN node, the node retrieves the requested resources from the origin server over HTTP. If the client sends an HTTPS request, the CDN node also retrieves the requested resources from the origin server over HTTPS.

**Note:** The origin must support port 80 and port 443. Otherwise, the back-to-origin process may fail.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  In the left-side navigation pane of the domain name details page, click **Back-to-Origin**. In the Use Request Protocol for Back-to-Source section, turn on the **Use Request Protocol for Back-to-Source** switch.

    ![Protocol for Back-to-Source switch](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1091888061/p180599.png)

    **Note:** The **Use Request Protocol for Back-to-Source** switch takes effect on dynamic and static resources. Alibaba Cloud CDN communicates with the origin server by using the specified dynamic origin protocol policy when Alibaba Cloud CDN requests dynamic resources.


