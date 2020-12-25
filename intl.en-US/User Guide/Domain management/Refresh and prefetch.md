# Refresh and prefetch

ApsaraVideo VOD provides the refresh and prefetch features. You can use the refresh feature to force Content Delivery Network \(CDN\) nodes to retrieve the latest resources from origin servers. You can use the prefetch feature to fetch frequently requested resources during off-peak hours. This improves the efficiency of resource access. This topic describes how to configure the refresh and prefetch features.

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Refresh and Push** to go to the Refresh and Push page.

4.  On the **Refresh Cache** tab, you can configure the refresh or prefetch parameters as needed.

    ![Refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6774888061/p183294.png)

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Operation**|Supported operations:     -   **Refresh**

After resources are updated on the origin server, you can refresh the URLs of the resources. Then, the system automatically clears the data of the resources that are cached on CDN nodes. When you visit the refreshed URLs, the latest resources from the origin server are retrieved. The retrieved resources are also cached on CDN nodes.

    -   **Push**

You can prefetch frequently requested resources or less frequently visited CDN domains during off-peak hours to increase the cache hit ratio. |
    |**Object**|Supported objects:     -   **Folder**

This option is available only when you set the **Operation** parameter to **Refresh**.

    -   **URL**

This option is available when you set the **Operation** parameter to **Refresh** or **Push**. |
    |**URL**|If you want to refresh multiple URLs or prefetch multiple resources based on URLs, enter only one URL on each line. When you enter URLs, take note of the following points:     -   Refresh resources based on the directory of CDN nodes

Each URL must start with `http://` or `https://`, and end with a forward slash \(`/`\).

You can refresh up to 100 directories per day by using one Alibaba Cloud account. A maximum of 100 refresh requests can be submitted at a time.

    -   Refresh resources based on URLs

Each URL must start with `http://` or `https://`.

You can refresh up to 2,000 URLs per day by using one Alibaba Cloud account. A maximum of 1,000 refresh requests can be submitted at a time.

    -   Prefetch resources based on URLs

Each URL must start with `http://` or `https://`.

You can prefetch up to 500 URLs per day by using one Alibaba Cloud account. A maximum of 100 prefetch requests can be submitted at a time. |

5.  Click **Submit**.

6.  Click the **Records** tab.

    You can view the detailed information of refresh and prefetch records, including the object, type, time, status, and progress of each operation.


