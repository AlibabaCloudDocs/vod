# Data monitoring

ApsaraVideo VOD provides the data monitoring feature. You can use this feature to monitor resources and real-time bandwidth and traffic.

Data monitoring supports resource monitoring and real-time monitoring.

## Procedure

1.  Log on to the [ApsaraVideo VOD console](https://vod.console.aliyun.com/).

2.  In the left-side navigation pane, find **Data Center**.

    1.  Choose **Data Monitoring** \> **Resource Monitoring** to go to the Resource Monitoring page.

        ![Resource Monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8184888061/p179378.png)

        You can view the details about the following metrics by domain, region, Internet service provider \(ISP\), time granularity, and time period. The time granularity can be 5 minutes or 1 hour. The time period can be today, yesterday, last seven days, last 30 days, or a custom period.

        |Item|Metric|
        |----|------|
        |Traffic Bandwidth|Bandwidth and traffic|
        |Back-to-origin Statistics|Back-to-origin bandwidth and back-to-origin traffic|
        |Number of Visits|The number of requests and the number of queries per second \(QPS\)|
        |Hit Rate|N/A|
        |HTTP Code|5xx codes, 4xx codes, 3xx codes, and 2xx codes|

        The data that is shown in the line chart of resource monitoring slightly differs from the billing data. For example, a 30-day line chart of resource statistics is plotted at 14,400-second intervals. The billing data is plotted at 300-second intervals. The line chart does not take all points into account and can be used to show the bandwidth trend. The billing data is more fine-grained and can be used to calculate the actual bandwidth usage.

        **Note:** You cannot select a specified region or ISP for the hit ratio.

    2.  Choose **Data Monitoring** \> **Real-time Monitoring** to go to the Real-time Monitoring page.

        ![Real-time Monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8184888061/p179386.png)

        You can view the details about the following metrics by domain, region, ISP, and time period. The time period can be the last hour, the last 6 hours, the last 12 hours, or a custom time period.

        |Item|Metric|
        |----|------|
        |Basic Date|Bandwidth, traffic, the number of requests, and QPS|
        |Back-to-origin Traffic|Back-to-origin traffic and back-to-origin bandwidth|
        |Quality Monitoring|Request hit ratio, byte hit ratio, 5xx codes, 4xx codes, 3xx codes, and 2xx codes|


