视频DNA 
==========================

本篇文档提供了Go SDK视频DNA模块相关功能的API调用示例。包含提交视频DNA作业、查询视频DNA作业、获取视频DNA结果。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/intl.zh-CN/服务端SDK/Go SDK/初始化.md)。

提交视频DNA作业 {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------

调用SubmitAIJob接口，完成提交视频DNA作业功能。

接口参数和返回字段请参见[SubmitAIJob]()。调用示例如下：

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MySubmitAIJob(client *vod.Client) (response *vod.SubmitAIJobResponse, err error) {
        request := vod.CreateSubmitAIJobRequest()
        // 视频ID
        request.MediaId = "<VideoId>"
        // 设置AI类型，类型为固定值 AIMediaDNA
        request.Types = "AIMediaDNA"
    
        request.AcceptFormat = "JSON"
    
        return client.SubmitAIJob(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err != nil {
            panic(err)
        }
    
        response, err := MySubmitAIJob(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, job := range response.AIJobList.AIJob {
            fmt.Printf("%s: %s\n", job.Type, job.JobId)
        }
    }



查询视频DNA作业 {#h2--dna-div-id-listaijob-div-3}
-------------------------------------------

调用ListAIJob接口，完成查询视频DNA作业功能。

接口参数和返回字段请参见[ListAIJob]()。调用示例如下：

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyListAIJob(client *vod.Client) (response *vod.ListAIJobResponse, err error) {
        request := vod.CreateListAIJobRequest()
        // 视频AI作业ID，多个用逗号分隔
        request.JobIds = "JobId1,JobId2"
    
        request.AcceptFormat = "JSON"
    
        return client.ListAIJob(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err != nil {
            panic(err)
        }
    
        response, err := MyListAIJob(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, job := range response.AIJobList.AIJob {
            fmt.Printf("%s: %s %s\n", job.JobId, job.Status, job.Data)
        }
    }



获取视频DNA结果 {#h2--dna-div-id-getmediadnaresult-div-4}
---------------------------------------------------

调用GetMediaDNAResult接口，完成获取视频DNA结果功能。

接口参数和返回字段请参见[GetMediaDNAResult]()。调用示例如下：

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetMediaDNAResult(client *vod.Client) (response *vod.GetMediaDNAResultResponse, err error) {
        request := vod.CreateGetMediaDNAResultRequest()
        // 视频ID
        request.MediaId = "<VideoId>"
    
        request.AcceptFormat = "JSON"
    
        return client.GetMediaDNAResult(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err != nil {
            panic(err)
        }
    
        response, err := MyGetMediaDNAResult(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }


