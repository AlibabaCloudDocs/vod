# Configure an origin host

If you want to customize the domain name of the server to which CDN initiates back-to-origin requests, you must configure the domain name type of the origin host. The available domain name types for an origin host are domain name for CDN, origin domain name, and custom domain name.

An origin host is the domain name of the origin server to which CDN initiates back-to-origin requests. If your origin server is shared by multiple services, you can use an origin host in your back-to-origin requests to distinguish different services.

**Note:** If your origin server is bound to multiple domain names or servers, you must specify the domain name to which the back-to-origin requests are sent. Otherwise, the back-to-origin process fails.

## Differences between an origin server and an origin host:

-   An origin server determines the specific IP address to which CDN initiates back-to-origin requests.
-   An origin host determines the requested domain associated with a specific IP address to which CDN initiates back-to-origin requests.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  In the left-side navigation pane of the domain name details page, click **Back-to-Origin**.

6.  In the Origin Host section, click **Modify**. In the Origin Host dialog box, turn on **Origin Host**, select a domain name type, and then click **OK**.

    ![Select a domain name type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7781888061/p180550.png)

    |Parameter|Description|
    |---------|-----------|
    |**CDN**|The domain name that you want to accelerate by using CDN. Users can access this domain name, for example, `cdntest.com`. If you set the domain name type of the origin host to **CDN**, the domain name of the origin host is specified as a domain name to accelerate, for example, `cdntest.com`.|
    |**Origin**|The domain name of the origin server. When CDN requests resources from the origin, CDN must access this domain name, for example, `origin.com`. If you set the domain name type of the origin host to **Origin**, the domain name of the origin host is specified as the origin domain name, for example, `origin.com`.|
    |**Custom**|If you set the domain name type of the origin host to **Custom**, the domain name of the origin host is specified as a custom domain name that you specify. If your origin server is bound to multiple domain names, you must specify a specific domain name. Otherwise, CDN fails to request resources from the origin server.|

7.  Click **OK**.


## Example

|Origin server type|Feature status|Domain name|Description|
|------------------|--------------|-----------|-----------|
|Site domain|By default, the Origin Host switch is turned off.|Domain name for CDN:`cdntest.com`

The address of the origin server:

`origin.com`

|-   If you set the domain name type to **CDN**, the domain name of the origin host is `cdntest.com`.
-   If you set the domain name type to **Origin**, the domain name of the origin host is `origin.com`.
-   If you set the domain name type to **Custom**, the domain name of the origin host is the domain name that you specify. |
|IP address|By default, the Origin Host switch is turned off.|Domain name for CDN:`cdntest.com`

The address of the origin server:

`1.1.1.1`

|-   If you set the domain name type to **CDN**, the domain name of the origin host is `cdntest.com`.
-   If you set the domain name type to **Custom**, the domain name of the origin host is the domain name that you specify.

**Note:** The address of the origin server is an IP address. Therefore, the **Origin** option for the domain name type is unavailable. |
|OSS domain|By default, the Origin Host switch is turned on.|Domain name for CDN:`cdntest.com`

The address of the origin server:

`test.oss-cn-hangzhou.aliyuncs.com`

|-   If you set the domain name type to **CDN**, the domain name of the origin host is `cdntest.com`.
-   If you set the domain name type to **Origin**, the domain name of the origin host is `test.oss-cn-hangzhou.aliyuncs.com`.
-   If you set the domain name type to **Custom**, the domain name of the origin host is the custom domain name that you specify.

**Note:** Default settings:

Domain name type: Origin

Address of the origin server: `test.oss-cn-hangzhou.aliyuncs.com` |

