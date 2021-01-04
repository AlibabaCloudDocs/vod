VOD CDN 
============================

This topic provides examples on how to use the API operations of the VOD CDN module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to preload and refresh caches, query the refresh and preload statuses, query traffic data and network bandwidth, and query the logs of domain names. You can also query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Preload caches {#h2--div-id-preloadvodobjectcaches-div-2}
---------------------------------------------------------

You can call the PreloadVodObjectCaches operation to preload caches.
For more information about the request and response parameters of this operation, see [PreloadVodObjectCaches](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/PreloadVodObjectCaches.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "strings"
    )
    
    func MyPreloadVodObjectCaches(client *vod.Client) (response *vod.PreloadVodObjectCachesResponse, err error) {
        request := vod.CreatePreloadVodObjectCachesRequest()
        objectPath := []string{"http://test.com/fd.mp4", "http://test.com/ld.mp4"}
        request.ObjectPath = strings.Join(objectPath, "\n")
    
        request.AcceptFormat = "JSON"
    
        return client.PreloadVodObjectCaches(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyPreloadVodObjectCaches(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        fmt.Printf("PreloadTaskId: %s\n", response.PreloadTaskId)
    }



Refresh caches {#h2--div-id-refreshvodobjectcaches-div-3}
---------------------------------------------------------

You can call the RefreshVodObjectCaches operation to refresh caches.
For more information about the request and response parameters of this operation, see [RefreshVodObjectCaches](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/RefreshVodObjectCaches.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "strings"
    )
    
    func MyRefreshVodObjectCaches(client *vod.Client) (response *vod.RefreshVodObjectCachesResponse, err error) {
        request := vod.CreateRefreshVodObjectCachesRequest()
        objectPath := []string{"http://test.com/fd.mp4", "http://test.com/ld.mp4"}
        request.ObjectPath = strings.Join(objectPath, "\n")
    
        request.AcceptFormat = "JSON"
    
        return client.RefreshVodObjectCaches(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyRefreshVodObjectCaches(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        fmt.Printf("RefreshTaskId: %s\n", response.RefreshTaskId)
    }



Query the refresh and preload statuses {#h2--div-id-describevodrefreshtasks-div-4}
----------------------------------------------------------------------------------

You can call the DescribeVodRefreshTasks operation to query the refresh and preload statuses.
For more information about the request and response parameters of this operation, see [DescribeVodRefreshTasks](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/DescribeRefreshTasks.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDescribeVodRefreshTasks(client *vod.Client) (response *vod.DescribeVodRefreshTasksResponse, err error) {
        request := vod.CreateDescribeVodRefreshTasksRequest()
        request.DomainName = "test.com"
        request.ObjectType = "preload"
    
        request.AcceptFormat = "JSON"
    
        return client.DescribeVodRefreshTasks(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDescribeVodRefreshTasks(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        for _, task := range response.Tasks.Task {
            fmt.Printf("%s: %s %s\n", task.ObjectPath, task.Status, task.Process)
        }
    }



Query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations {#h2--div-id-describevodrefreshquota-div-5}
------------------------------------------------------------------------------------------------------------------------------------------------------

You can call the DescribeVodRefreshQuota operation to query the maximum and currently allowed numbers of URLs and directories for refresh and preload operations.
For more information about the request and response parameters of this operation, see [DescribeVodRefreshQuota](/intl.en-US/API Reference/VoD CDN/Refresh and Preheating/DescribeVodRefreshQuota.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDescribeVodRefreshQuota(client *vod.Client) (response *vod.DescribeVodRefreshQuotaResponse, err error) {
        request := vod.CreateDescribeVodRefreshQuotaRequest()
    
        request.AcceptFormat = "JSON"
    
        return client.DescribeVodRefreshQuota(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDescribeVodRefreshQuota(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        fmt.Printf("PreloadQuota %s, PreloadRemain %s\n", response.PreloadQuota, response.PreloadRemain)
        fmt.Printf("UrlQuota %s, UrlRemain %s\n", response.UrlQuota, response.UrlRemain)
    }



Query traffic data {#h2--div-id-describevoddomaintrafficdata-div-6}
-------------------------------------------------------------------

You can call the DescribeVodDomainTrafficData operation to query traffic data.
For more information about the request and response parameters of this operation, see [DescribeVodDomainTrafficData](/intl.en-US/API Reference/VoD CDN/Data Monitoring/DescribeVodDomainTrafficData.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDescribeVodDomainTrafficData(client *vod.Client) (response *vod.DescribeVodDomainTrafficDataResponse, err error) {
        request := vod.CreateDescribeVodDomainTrafficDataRequest()
        request.DomainName = "test.com"
        request.StartTime = "2019-01-15T15:59:59Z"
        request.EndTime = "2019-01-20T15:59:58Z"
    
        request.AcceptFormat = "JSON"
    
        return client.DescribeVodDomainTrafficData(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDescribeVodDomainTrafficData(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        for _, item := range response.TrafficDataPerInterval.DataModule {
            fmt.Printf("%s: DomesticValue %s bytes, OverseasValue %s bytes\n",
                item.TimeStamp, item.DomesticValue, item.OverseasValue)
        }
    }



Query network bandwidth {#h2--div-id-describevoddomainbpsdata-div-7}
--------------------------------------------------------------------

You can call the DescribeVodDomainBpsData operation to query network bandwidth.
For more information about the request and response parameters of this operation, see [DescribeVodDomainBpsData](/intl.en-US/API Reference/VoD CDN/Data Monitoring/DescribeVodDomainBpsData.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDescribeVodDomainBpsData(client *vod.Client) (response *vod.DescribeVodDomainBpsDataResponse, err error) {
        request := vod.CreateDescribeVodDomainBpsDataRequest()
        request.DomainName = "test.com"
        request.StartTime = "2019-01-15T15:59:59Z"
        request.EndTime = "2019-01-20T15:59:58Z"
    
        request.AcceptFormat = "JSON"
    
        return client.DescribeVodDomainBpsData(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDescribeVodDomainBpsData(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        for _, item := range response.BpsDataPerInterval.DataModule {
            fmt.Printf("%s: Value %s bps, OverseasValue %s bps\n",
                item.TimeStamp, item.Value, item.OverseasValue)
        }
    }



Query the logs of a domain name {#h2--div-id-describevoddomainlog-div-8}
------------------------------------------------------------------------

You can call the DescribeVodDomainLog operation to query the logs of a domain name.
For more information about the request and response parameters of this operation, see [DescribeVodDomainLog](/intl.en-US/API Reference/VoD CDN/Log Management/DescribeVodDomainLog.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDescribeVodDomainLog(client *vod.Client) (response *vod.DescribeVodDomainLogResponse, err error) {
        request := vod.CreateDescribeVodDomainLogRequest()
        request.DomainName = "vod-test1.cn-shanghai.192.168.0.0/16"
        request.StartTime = "2019-01-15T15:59:59Z"
        request.EndTime = "2019-01-20T15:59:58Z"
        request.PageNumber = "1"
        request.PageSize = "300"
    
        request.AcceptFormat = "JSON"
    
        return client.DescribeVodDomainLog(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDescribeVodDomainLog(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        logDetail := response.DomainLogDetails.DomainLogDetail[0]
        fmt.Printf("TotalLogCount: %d\n", logDetail.PageInfos.Total)
        for _, item := range logDetail.LogInfos.LogInfoDetail {
            fmt.Printf("%s: LogSize %d bytes, LogDownloadPath\n  %s\n",
                item.StartTime, item.LogSize, item.LogPath)
        }
    }


