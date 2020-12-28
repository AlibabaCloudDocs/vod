# Parameter filtering

If a request URL contains a question mark \(?\) that is followed by parameters, you can enable the parameter filtering feature to increase the cache hit ratio and content delivery efficiency. This topic describes how to configure parameter filtering.

## Overview

The parameter filtering feature of Alibaba Cloud CDN can retain or ignore parameters.

-   Ignore parameters

    A Content Delivery Network \(CDN\) node caches a unique version of the requested resource for each URL.

    After parameter filtering is disabled, the requested resource can be retrieved only if the parameters that follow the question mark \(?\) in the URL are an exact match of the parameters in the previously visited URL. Exact matches can increase the request accuracy. For example, the first time when `http://www.abc.com/1.jpg` is visited, the resource is not cached on CDN nodes. Therefore, the requested resource is retrieved from the origin server. When `http://www.abc.com/1.jpg? test1` is visited, the parameters that follow the question mark \(?\) must be exactly matched because parameter filtering is disabled. As a result, CDN nodes cannot return the resource of `http://www.abc.com/1.jpg`. Instead, CDN nodes must retrieve the requested resource of `http://www.abc.com/1.jpg?test1` from the origin server.

-   Retain parameters

    Most request URLs contain parameters. If the parameters do not need to be prioritized, you can enable parameter filtering to ignore the parameters so that you can retrieve resources from CDN nodes. This can improve the cache hit ratio and delivery efficiency.

    If a parameter contains important information such as the file version, we recommend that you specify the parameter as a retained parameter. You can specify at most 10 retained parameters. If a request URL contains a retained parameter, the CDN node retrieves resources from the origin server based on the URL with the retained parameter.

    Parameter filtering is used to ignore parameters that follow question marks \(?\) in request URLs. This increases the cache hit ratio. For example, the first time when `http://www.abc.com/1.jpg` is visited, the resource is not cached on CDN nodes. Therefore, the requested resource is retrieved from the origin server. When `http://www.abc.com/1.jpg?test1` is visited, the parameters that follow the question mark \(?\) are ignored because parameter filtering is enabled. Although the URL is not an exact match, the resource of `http://www.abc.com/1.jpg` that is cached on CDN nodes can be retrieved.


1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, click **Configuration Management**.

3.  Choose **CDN Configuration** \> **Domain Names**.

4.  On the Domain Names page, select the domain name that you want to configure, and click **Configure** in the Actions column.

    ![Click Configure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2585068061/p180549.png)

5.  Click **Performance Optimization**.

6.  Click **Modify**.

    ![Parameter filtering](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4344888061/p181763.png)

7.  Turn on **Filter Parameters** and specify the retained parameters.

    ![Configuration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4344888061/p181765.png)

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Filter Parameters**|The switch of the parameter filtering feature. After this feature is enabled, the parameters that follow the question mark \(?\) in a request URL are ignored. This increases the cache hit ratio.|
    |**Retention Parameters**|The parameters that you want to retain. You can specify at most 10 retained parameters. Separate parameters with commas \(,\). For example, for the `http://www.abc.com/a.jpg?x` URL, you can set `x` as a retained parameter.|

8.  Click **OK**.


