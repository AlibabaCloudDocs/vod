# IP address blacklist or whitelist

An IP address blacklist or whitelist is used to identify and filter users. This helps you restrict access to Content Delivery Network \(CDN\) nodes and improve service security. This topic describes how to configure an IP address blacklist or whitelist.

-   If an IP address blacklist is configured, the IP addresses in the blacklist are not allowed to access CDN nodes.
-   If an IP address whitelist is configured, only IP addresses in the whitelist are allowed to access CDN nodes.

**Note:**

-   IP blacklists and whitelists support IPv6 addresses. Letters in IPv6 addresses must be uppercase, for example, 2001:DB8:0:23:8:800:200C:417A and 2001:0DB8:0000:0023:0008:0800:200C:417A. The representation of an IPv6 address must not be shortened. For example, 2001:0DB8::0008:0800:200C:417A is not supported.
-   Both IP blacklists and whitelists support Classless Inter-Domain Routing \(CIDR\) blocks. For example, in the 192.168.0.0/24 CIDR block, /24 indicates that the first 24 bits in the subnet mask are the network bits. The remaining 8 bits are host bits. The number of host bits is calculated based on the following formula: 32 - 24 = 8. You can connect 254 hosts to the subnet. The number of hosts is calculated based on the following formula: 2^8 - 2 = 254. Therefore, 192.168.0.0/24 represents IP addresses from 192.168.0.1 to 192.168.0.254.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Click **Resource Access Control**.

6.  Click the **IP Address Blacklists/Whitelists** tab and then **Modify**.

    ![Modify](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8934888061/p181720.png)

7.  Set the **Type** and **Rules** parameters and click **OK** to complete the configuration.

    ![Configuration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8934888061/p181721.png)

    The following table describes the blacklist and whitelist.


