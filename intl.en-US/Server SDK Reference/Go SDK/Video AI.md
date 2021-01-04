Video AI 
=============================

This topic provides examples on how to use the API operations of the video AI module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to submit or query AI jobs, specify an AI template as the default one, and query the default AI template. You can also create, delete, modify, and query AI templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Submit an AI job {#h2--ai-div-id-submitaijob-div-2}
---------------------------------------------------

You can call the SubmitAIJob operation to submit an AI job.
For more information about the request and response parameters of this operation, see [SubmitAIJob](). Example: {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        // The AI type. Separate multiple types with commas (,). Make sure that this AI type is enabled.
        request.Types = "AIVideoCover,AIVideoCensor"
    
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



Query AI jobs {#h2--ai-div-id-listaijob-div-3}
----------------------------------------------

You can call the ListAIJob operation to query AI jobs.
For more information about the request and response parameters of this operation, see [ListAIJob](). Example: {#h2--ai-div-id-listaijob-div-3}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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



Create an AI template {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------

You can call the AddAITemplate operation to create an AI template.
For more information about the request and response parameters of this operation, see [AddAITemplate](). Example: {#h2--ai-div-id-addaitemplate-div-4}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "encoding/json"
    )
    
    func MyAddAITemplate(client *vod.Client) (response *vod.AddAITemplateResponse, err error) {
        request := vod.CreateAddAITemplateRequest()
    
        // The template type. For this example, specify an automated review template.
        request.TemplateType = "AIMediaAudit"
        // The name of the template.
        request.TemplateName = "My AI Template"
    
        // The detailed configurations of the template.
        auditItem := []string{"terrorism", "porn"}
        auditRange := []string{"video", "image-cover", "text-title"}
        auditContent := []string{"screen"}
        templateConfig := map[string]interface{}{"AuditItem": auditItem, "AuditRange": auditRange,
            "AuditContent": auditContent, "AuditAutoBlock": "no"}
    
        jsonConfig, err := json.Marshal(templateConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.TemplateConfig = string(jsonConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.AddAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyAddAITemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TemplateId)
    }



Delete an AI template {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------

You can call the DeleteAITemplate operation to delete an AI template.
For more information about the request and response parameters of this operation, see [DeleteAITemplate](). Example: {#h2--ai-div-id-deleteaitemplate-div-5}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDeleteAITemplate(client *vod.Client) (response *vod.DeleteAITemplateResponse, err error) {
        request := vod.CreateDeleteAITemplateRequest()
        request.TemplateId = "<TemplateId>"
    
        request.AcceptFormat = "JSON"
    
        return client.DeleteAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteAITemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Modify an AI template {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------

You can call the UpdateAITemplate operation to modify an AI template.
For more information about the request and response parameters of this operation, see [UpdateAITemplate](). Example: {#h2--ai-div-id-updateaitemplate-div-6}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "encoding/json"
    )
    
    func MyUpdateAITemplate(client *vod.Client) (response *vod.UpdateAITemplateResponse, err error) {
        request := vod.CreateUpdateAITemplateRequest()
    
        // The ID of the template.
        request.TemplateId = "2a0aadb19e187a58f296e2aeb2ad****"
        // The name of the template.
        request.TemplateName = "New AI Template Name"
    
        // The detailed configurations of the template.
        auditItem := []string{"terrorism", "porn"}
        auditRange := []string{"video", "image-cover"}
        auditContent := []string{"screen"}
        templateConfig := map[string]interface{}{"AuditItem": auditItem, "AuditRange": auditRange,
            "AuditContent": auditContent, "AuditAutoBlock": "yes"}
    
        jsonConfig, err := json.Marshal(templateConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.TemplateConfig = string(jsonConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.UpdateAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateAITemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Query an AI template {#h2--ai-div-id-getaitemplate-div-7}
---------------------------------------------------------

You can call the GetAITemplate operation to query details about an AI template.
For more information about the request and response parameters of this operation, see [GetAITemplate](). Example: {#h2--ai-div-id-getaitemplate-div-7}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    
    func MyGetAITemplate(client *vod.Client) (response *vod.GetAITemplateResponse, err error) {
        request := vod.CreateGetAITemplateRequest()
        request.TemplateId = "<TemplateId>"
    
        request.AcceptFormat = "JSON"
    
        return client.GetAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetAITemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TemplateInfo)
    }



Query AI templates {#h2--ai-div-id-listaitemplate-div-8}
--------------------------------------------------------

You can call the ListAITemplate operation to query AI templates.
For more information about the request and response parameters of this operation, see [ListAITemplate](). Example: {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyListAITemplate(client *vod.Client) (response *vod.ListAITemplateResponse, err error) {
        request := vod.CreateListAITemplateRequest()
        request.TemplateType = "AIMediaAudit"
    
        request.AcceptFormat = "JSON"
    
        return client.ListAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyListAITemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TemplateInfoList)
    }



Specify an AI template as the default one {#h2--ai-div-id-setdefaultaitemplate-div-9}
-------------------------------------------------------------------------------------

You can call the SetDefaultAITemplate operation to specify an AI template as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultAITemplate](). Example: {#h2--ai-div-id-setdefaultaitemplate-div-9}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MySetDefaultAITemplate(client *vod.Client) (response *vod.SetDefaultAITemplateResponse, err error) {
        request := vod.CreateSetDefaultAITemplateRequest()
        request.TemplateId = "<TemplateId>"
    
        request.AcceptFormat = "JSON"
    
        return client.SetDefaultAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySetDefaultAITemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Query the default AI template {#h2--ai-div-id-getdefaultaitemplate-div-10}
--------------------------------------------------------------------------

You can call the GetDefaultAITemplate operation to query details about the default AI template.
For more information about the request and response parameters of this operation, see [GetDefaultAITemplate](). Example: {#h2--ai-div-id-getdefaultaitemplate-div-10}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetDefaultAITemplate(client *vod.Client) (response *vod.GetDefaultAITemplateResponse, err error) {
        request := vod.CreateGetDefaultAITemplateRequest()
        request.TemplateType = "AIMediaAudit"
    
        request.AcceptFormat = "JSON"
    
        return client.GetDefaultAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetDefaultAITemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TemplateInfo)
    }


