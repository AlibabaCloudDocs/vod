# Configure URL signing

Referer-based hotlink protection is not completely secure. We recommend that you use URL signing to protect resources on the origin server against illegal download and misuse.

## How it works

Alibaba Cloud CDN nodes work with the origin server to implement URL signing to protect resources on the origin server against hotlinking in a more secure and reliable way.

1.  The origin server provides a signed URL that contains authentication information.
2.  A user sends a request to a CDN node by using the signed URL.
3.  The CDN node verifies the authentication information in the signed URL to determine whether the request is valid. If the request is valid, the CDN node returns a success response. Otherwise, the CDN node denies the request.

**Note:** After a request URL is authenticated by a CDN node, special characters such as `equal signs (=)` and `plus signs (+)` in the URL are escaped.

## Procedure

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Click **Resource Access Control**.

6.  Click the **URL Authentication** tab. On the URL Authentication tab, click **Modify**.

    ![Modify](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9119339161/p181688.png)

7.  Turn on **URL Authentication**, configure the authentication information, and then click **OK**.

    ![Modify](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0219339161/p181693.png)

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Authentication Method**|ApsaraVideo VOD supports only type A signing to protect resources on the origin server.

**Note:** If a URL signing error occurs, a 403 error code is returned. In this case, you must re-calculate the signature.

    -   The MD5 value is wrong.

Example: `X-Tengine-Error:denied by req auth: invalid md5hash=de7bfdc915ced05e17380a149bd760be`

    -   The timestamp is wrong.

Example: `X-Tengine-Error:denied by req auth: expired timestamp=1439469547` |
    |**Primary Key**|Specify the primary key for the selected signing type.|
    |**Secondary Key**|Specify the secondary key for the selected signing type.|
    |**Default Validity Period**|Specify the default validity period for the signed URL. Unit: minutes.|
    |**Support Previewing**|If the preview feature is enabled, users can view only a specified duration of a video or audio file, such as the first 5 minutes. This feature is widely used in paid services, such as video or audio content that charges non-membership users a fee. For more information, see [t1959346.md\#](/intl.en-US/Best Practice/Configure the preview feature for VOD resources.md).|

8.  Generate a signed URL.

    In the **Generate Authentication URL** section, set the **Original URL** parameter and other authentication parameters.

    ![Generate a signed URL](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0219339161/p181697.png)

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Original URL**|Enter a complete URL, such as `https://www.aliyun.com`.|
    |**Authentication Method**|By default, type A signing is used.|
    |**Authentication Key**|Specify the authentication key as needed. The authentication key can be the primary key or the secondary key that you configured in the **URL Authentication** dialog box.|
    |**Validity Period**|Specify the validity period for the signed URL as needed. Unit: seconds. Example: 1800. **Note:** The default validity period is 30 minutes. If you need to specify a validity period of less than 30 minutes, set the **Validity Period** parameter to a negative value. For example, if you need to specify a validity period of 10 seconds, set the **Validity Period** parameter to -1790. |

9.  Click **Generate**.

    ![Generate](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0219339161/p181708.png)


