Media fingerprinting 
=========================================

This topic provides examples on how to use the API operations of the media fingerprinting module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to submit media fingerprinting jobs, query media fingerprinting jobs, and query media fingerprinting results.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Submit a media fingerprinting job {#h2--dna-div-id-submitaijob-div-2}
---------------------------------------------------------------------

You can call the SubmitAIJob operation to submit a media fingerprinting job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--dna-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MySubmitAIJob(client *vod.Client) (response *vod.SubmitAIJobResponse, err error) {
        request := vod.CreateSubmitAIJobRequest()
        // The ID of the video.
        request.MediaId = "<VideoId>"
        // The AI type. Set the value to AIMediaDNA.
        request.Types = "AIMediaDNA"
    
        request.AcceptFormat = "JSON"
    
        return client.SubmitAIJob(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySubmitAIJob(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, job := range response.AIJobList.AIJob {
            fmt.Printf("%s: %s\n", job.Type, job.JobId)
        }
    }



Query media fingerprinting jobs {#h2--dna-div-id-listaijob-div-3}
-----------------------------------------------------------------

You can call the ListAIJob operation to query media fingerprinting jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--dna-div-id-listaijob-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyListAIJob(client *vod.Client) (response *vod.ListAIJobResponse, err error) {
        request := vod.CreateListAIJobRequest()
        // The ID of the AI job. Separate multiple IDs with commas (,).
        request.JobIds = "JobId1,JobId2"
    
        request.AcceptFormat = "JSON"
    
        return client.ListAIJob(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyListAIJob(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, job := range response.AIJobList.AIJob {
            fmt.Printf("%s: %s %s\n", job.JobId, job.Status, job.Data)
        }
    }



Query media fingerprinting results {#h2--dna-div-id-getmediadnaresult-div-4}
----------------------------------------------------------------------------

You can call the GetMediaDNAResult operation to query media fingerprinting results.
For more information about the request and response parameters of this operation, see [GetMediaDNAResult](). Example: {#h2--dna-div-id-getmediadnaresult-div-4}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetMediaDNAResult(client *vod.Client) (response *vod.GetMediaDNAResultResponse, err error) {
        request := vod.CreateGetMediaDNAResultRequest()
        // The ID of the video.
        request.MediaId = "<VideoId>"
    
        request.AcceptFormat = "JSON"
    
        return client.GetMediaDNAResult(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetMediaDNAResult(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }


