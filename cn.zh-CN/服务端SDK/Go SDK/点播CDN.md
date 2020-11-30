点播CDN 
==========================

本篇文档提供了Go SDK点播CDN模块相关功能的API调用示例。包含预热缓存、刷新缓存、查询刷新和预热状态、查询刷新预热次数限制和余量、查询流量数据、查询网络带宽、下载域名日志。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/Go SDK/初始化.md)。

预热缓存 {#h2--div-id-preloadvodobjectcaches-div-2}
-----------------------------------------------

调用PreloadVodObjectCaches接口，完成预热缓存功能。
接口参数和返回字段请参见[PreloadVodObjectCaches](/cn.zh-CN/服务端API/点播CDN/刷新预热/预热缓存.md)。调用示例如下： 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyPreloadVodObjectCaches(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        fmt.Printf("PreloadTaskId: %s\n", response.PreloadTaskId)
    }



刷新缓存 {#h2--div-id-refreshvodobjectcaches-div-3}
-----------------------------------------------

调用RefreshVodObjectCaches接口，完成刷新缓存功能。
接口参数和返回字段请参见[RefreshVodObjectCaches](/cn.zh-CN/服务端API/点播CDN/刷新预热/刷新缓存.md)。调用示例如下： 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyRefreshVodObjectCaches(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        fmt.Printf("RefreshTaskId: %s\n", response.RefreshTaskId)
    }



查询刷新和预热状态 {#h2--div-id-describevodrefreshtasks-div-4}
-----------------------------------------------------

调用DescribeVodRefreshTasks接口，完成查询刷新和预热状态功能。
接口参数和返回字段请参见[DescribeVodRefreshTasks](/cn.zh-CN/服务端API/点播CDN/刷新预热/查询刷新和预热状态.md)。调用示例如下： 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyDescribeVodRefreshTasks(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        for _, task := range response.Tasks.Task {
            fmt.Printf("%s: %s %s\n", task.ObjectPath, task.Status, task.Process)
        }
    }



查询刷新预热次数限制和余量 {#h2--div-id-describevodrefreshquota-div-5}
---------------------------------------------------------

调用DescribeVodRefreshQuota接口，完成查询刷新预热次数限制和余量功能。
接口参数和返回字段请参见[DescribeVodRefreshQuota](/cn.zh-CN/服务端API/点播CDN/刷新预热/查询刷新预热次数限制和余量.md)。调用示例如下： 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyDescribeVodRefreshQuota(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        fmt.Printf("PreloadQuota %s, PreloadRemain %s\n", response.PreloadQuota, response.PreloadRemain)
        fmt.Printf("UrlQuota %s, UrlRemain %s\n", response.UrlQuota, response.UrlRemain)
    }



查询流量数据 {#h2--div-id-describevoddomaintrafficdata-div-6}
-------------------------------------------------------

调用DescribeVodDomainTrafficData接口，完成查询流量数据功能。
接口参数和返回字段请参见[DescribeVodDomainTrafficData](/cn.zh-CN/服务端API/点播CDN/数据监控/查询流量数据.md)。调用示例如下： 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyDescribeVodDomainTrafficData(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        for _, item := range response.TrafficDataPerInterval.DataModule {
            fmt.Printf("%s: DomesticValue %s bytes, OverseasValue %s bytes\n",
                item.TimeStamp, item.DomesticValue, item.OverseasValue)
        }
    }



查询网络带宽 {#h2--div-id-describevoddomainbpsdata-div-7}
---------------------------------------------------

调用DescribeVodDomainBpsData接口，完成查询网络带宽功能。
接口参数和返回字段请参见[DescribeVodDomainBpsData](/cn.zh-CN/服务端API/点播CDN/数据监控/查询网络带宽.md)。调用示例如下： 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyDescribeVodDomainBpsData(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Printf("RequestId: %s\n", response.RequestId)
        for _, item := range response.BpsDataPerInterval.DataModule {
            fmt.Printf("%s: Value %s bps, OverseasValue %s bps\n",
                item.TimeStamp, item.Value, item.OverseasValue)
        }
    }



下载域名日志 {#h2--div-id-describevoddomainlog-div-8}
-----------------------------------------------

调用DescribeVodDomainLog接口，完成下载域名日志功能。
接口参数和返回字段请参见[DescribeVodDomainLog](/cn.zh-CN/服务端API/点播CDN/日志管理/下载域名日志.md)。调用示例如下： 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyDescribeVodDomainLog(client)
        if err != nil {
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


