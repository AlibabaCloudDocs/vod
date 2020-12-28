# Configure a CNAME record in Alibaba Cloud DNS

After you add a domain name to Alibaba Cloud CDN, Alibaba Cloud CDN assigns a CNAME to the domain name. To enable the CDN service for the domain name, you must add a CNAME record to map the domain name to the CNAME. This way, requests destined for the domain name for CDN can be redirected to the CDN nodes that are nearest to the clients. This topic describes how to configure a CNAME record for a domain name in Alibaba Cloud DNS.

1.  Obtain the CNAME assigned to the domain name for CDN.

    1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

    2.  In the left-side navigation pane, choose **Configuration Management \> CDN Configuration \> Domain Names**.

    3.  On the Domain Names page, move the pointer over the View icon, and copy the CNAME of the domain name for CDN.

        ![Copy the CNAME](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8761888061/p182210.png)

2.  Add a CNAME record for the accelerated domain name.

    The following procedure uses the Alibaba Cloud DNS console as an example to describe how to configure a CNAME record for the accelerated domain name. You can perform similar operations in other DNS services such as DNSPod, Xinnet, and GoDaddy to configure a CNAME record for the accelerated domain name.

    1.  Log on to the [Alibaba Cloud DNS console](https://dc.console.aliyun.com/dns).

    2.  On the **Manage DNS** page, select the domain name that you want to manage, and then click **Configure** in the Actions column.

    3.  Click **Add Record**.

        **Note:** Each domain name for CDN has one CNAME. The CNAME of a primary domain name cannot be used by the second-level domain name. If you need to accelerate a second-level domain name, you must add the domain name to Alibaba Cloud CDN and resolve it to its CNAME. You can also add a wildcard domain name to Alibaba Cloud CDN because the CNAME of a wildcard domain name can be used by a second-level domain name.

        ![Add a record](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7526528061/p64412.png)

        -   Type: Select `CNAME - Canonical name` from the drop-down list.
        -   Host: Enter the prefix of the domain name for CDN.

            |Domain name for CDN|Host|
            |:------------------|:---|
            |`testcdn.aliyun.com`|`testcdn`|
            |`www.aliyun.com`|`www`|
            |`aliyun.com`|`@`|
            |`*.aliyun.com`|`*`|

        -   ISP Line: Use the default value.
        -   Value: Enter the CNAME assigned to the domain name for CDN.
        -   TTL: TTL stands for Time To Live. It limits the lifespan or lifetime of data in a computer or network. Use the default value.
    4.  Click **Confirm**.

        After the CNAME record takes effect, CDN acceleration is automatically enabled for the domain name.

        **Note:**

        -   After you add a CNAME record, it immediately takes effect. After you modify a CNAME record, the modifications take effect within 72 hours.
        -   After you add a CNAME record, the system updates the status in the console about 10 minutes later. Before the update, you may be prompted to add a CNAME record. Ignore the message.
3.  Check whether the CNAME record has taken effect.

    1.  Open the Command Prompt in Windows.

    2.  Run the ping command to ping the domain name for CDN. If the CNAME in the output matches the CNAME assigned to the domain name for CDN in the Alibaba Cloud CDN console, the CDN service is enabled for the domain name.

        ![Check the effectiveness of the CNAME record](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7423839951/p66693.png)


