# Configure a CNAME record on Xinnet

After you add a domain name in the ApsaraVideo VOD console, ApsaraVideo VOD assigns a canonical name \(CNAME\) to the domain name. You must add a CNAME record to map the domain name to the CNAME. This way, ApsaraVideo VOD forwards requests destined for the domain name to CDN nodes. This topic describes how to configure a CNAME record on Xinnet.

1.  Obtain the CNAME assigned to the domain name for CDN.

    1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

    2.  In the left-side navigation pane, choose **Configuration Management \> CDN Configuration \> Domain Names**.

    3.  On the Domain Names page, move the pointer over the View icon, and copy the CNAME of the domain name for CDN.

        ![Copy the CNAME](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8761888061/p182210.png)

2.  Add a CNAME record.

    1.  Log on to the [DNS console of Xinnet](https://console.xinnet.com/hy/index.html#/account).

    2.  Find the domain name that you want to manage, navigate to the Manage DNS page, and then click Add Record.

    3.  Set the required parameters.

        **Note:** Each domain name for CDN has one CNAME. The CNAME of a primary domain name cannot be used by a second-level domain name. If you need to accelerate a second-level domain name, you must add the domain name to Alibaba Cloud CDN and resolve it to the corresponding CNAME. You can also add a wildcard domain name to Alibaba Cloud CDN because the CNAME of a wildcard domain name can be used by a second-level domain name.

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
    4.  Click **Submit**.

        After the CNAME record takes effect, CDN acceleration is automatically enabled for the domain name.

        **Note:**

        -   After you add a CNAME record, it immediately takes effect. After you modify a CNAME record, the modifications take effect within 72 hours.
        -   After you add a CNAME record, the system updates the status in the console about 10 minutes later. During the update, you may be prompted to add a CNAME record. Ignore this message.
3.  Check whether the CNAME record has taken effect.

    1.  Open the Command Prompt in Windows.

    2.  Run the ping command to ping the domain name for CDN. If the CNAME in the output matches the CNAME assigned to the domain name for CDN in the Alibaba Cloud CDN console, the CDN service is enabled for the domain name.

        ![Check the effectiveness of the CNAME record](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7423839951/p66693.png)


