# Configure the priority level of an origin server

Alibaba Cloud CDN supports the following types of back-to-origin domain names: Object Storage Service \(OSS\) domain names, IP addresses, and custom domain names. If you set the origin site type to IP or Origin Domain Name, you can specify one or more IP addresses or domain names. Then set the priority for each IP address or domain name.

If you set Origin Site to IP or Origin Domain Name, you can specify one or more IP addresses or domain names. Then set the priority for each IP address or domain name. The priorities of IP addresses or domain names are **Primary** and **Secondary**. **Primary** indicates a higher priority than **Secondary**.

If multiple origin servers are configured, Alibaba Cloud CDN forwards requests to the origin server whose priority is Primary. If the primary origin server fails the health check three consecutive times, Alibaba Cloud CDN forwards requests to the origin server whose priority is Secondary. If the primary origin server passes a subsequent health check, the system marks the origin server as available and restores the priority of this origin server to Primary. If you set the same priority for all origin servers, Alibaba Cloud CDN automatically forwards requests to the origin servers based on the round robin scheme.

Layer 4 health checks are performed on origin servers. Probes are sent every 2.5 seconds.

**Note:**

Only IP addresses and custom domain names have priorities. You can select an origin server type and priority level based on your needs. If you set Origin Site to OSS Domain Name, priorities are not supported.

If multiple primary or secondary origins exist, one of them can be accessed based on probability. For example, if you have configured three origin servers and initiated 90 requests, Alibaba Cloud CDN forwards 30 requests to each origin server.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  In the left-side navigation pane, click **Basic Configuration**. In the **Origin Information** section, click **Modify**.

    ![Click Modify](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0951888061/p184328.png)

6.  In the Origin dialog box, set Origin Site, Port, and IP or Domain Name.

    ![Origin dialog box](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0951888061/p184329.png)

    -   If you set Origin Site to IP or Origin Domain Name, you are charged based on the Internet traffic.

    -   If you set Origin Site to OSS Domain Name, Alibaba Cloud CDN forwards requests to the specified OSS bucket and you are charged based on the internal data transfer. For more information, see [OSS pricing](https://cn.aliyun.com/price/product?spm=a2c4g.11186623.2.1.fd0XwH#/oss/detail).

    -   If you set Origin Site to Origin Domain Name and specify the endpoint of an OSS bucket, you are charged based on the Internet traffic.

7.  Click **OK**.


Set a custom port

After you configure a whitelist, you can set a custom port. Valid values of a custom port number: 0 to 65535.

-   If you set the redirect type of the static or dynamic origin protocol policy to **Follow**, you cannot set a custom port.
-   If you set the back-to-origin protocol policy to **Follow** by calling API operations, make sure that the origin protocol and custom port are operational.
-   If you enable the HTTP or HTTPS origin protocol and customize a port, your origin server returns the requested resources based on the port settings. This occurs regardless of other settings specified in the Alibaba Cloud CDN console.

