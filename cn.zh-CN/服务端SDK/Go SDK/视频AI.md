视频AI 
=========================

本篇文档提供了Go SDK视频AI模块相关功能的API调用示例。包含提交AI作业、查询AI作业、添加AI模板、修改AI模板、删除AI模板、查询AI模板、查询设置默认AI模板等。

初始化客户端 {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
--------------------------------------------

使用前请先初始化客户端，请参见[初始化](/cn.zh-CN/服务端SDK/Go SDK/初始化.md)。

提交AI作业 {#h2--ai-div-id-submitaijob-div-2}
-----------------------------------------

调用SubmitAIJob接口，完成提交AI作业功能。
接口参数和返回字段请参见[SubmitAIJob](/cn.zh-CN/服务端API/视频AI/提交AI作业.md)。调用示例如下： {#h2--ai-div-id-submitaijob-div-2}
------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        // AI类型，多个用逗号分隔；请确保已开通该类型AI服务
        request.Types = "AIVideoCover,AIVideoCensor"
    
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



查询AI作业 {#h2--ai-div-id-listaijob-div-3}
---------------------------------------

调用ListAIJob接口，完成查询AI作业功能。
接口参数和返回字段请参见[ListAIJob](/cn.zh-CN/服务端API/视频AI/查询AI作业.md)。调用示例如下： {#h2--ai-div-id-listaijob-div-3}
------------------------------------------------------------------------------------------------------------------------------------------------------------

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



添加AI模板 {#h2--ai-div-id-addaitemplate-div-4}
-------------------------------------------

调用AddAITemplate接口，完成添加AI模板功能。
接口参数和返回字段请参见[AddAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/添加AI模板.md)。调用示例如下： {#h2--ai-div-id-addaitemplate-div-4}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
    
        // 设置模板类型，以智能审核模板为例
        request.TemplateType = "AIMediaAudit"
        // 设置模板名称
        request.TemplateName = "My AI Template"
    
        // 设置模板详细配置
        auditItem := []string{"terrorism", "porn"}
        auditRange := []string{"video", "image-cover", "text-title"}
        auditContent := []string{"screen"}
        templateConfig := map[string]interface{}{"AuditItem": auditItem, "AuditRange": auditRange,
            "AuditContent": auditContent, "AuditAutoBlock": "no"}
    
        jsonConfig, err := json.Marshal(templateConfig)
        if err != nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.TemplateConfig = string(jsonConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.AddAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err != nil {
            panic(err)
        }
    
        response, err := MyAddAITemplate(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TemplateId)
    }



删除AI模板 {#h2--ai-div-id-deleteaitemplate-div-5}
----------------------------------------------

调用DeleteAITemplate接口，完成删除AI模板功能。
接口参数和返回字段请参见[DeleteAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/删除AI模板.md)。调用示例如下： {#h2--ai-div-id-deleteaitemplate-div-5}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyDeleteAITemplate(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



修改AI模板 {#h2--ai-div-id-updateaitemplate-div-6}
----------------------------------------------

调用UpdateAITemplate接口，完成修改AI模板功能。
接口参数和返回字段请参见[UpdateAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/修改AI模板.md)。调用示例如下： {#h2--ai-div-id-updateaitemplate-div-6}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
    
        // 设置模板ID
        request.TemplateId = "2a0aadb19e187a58f296e2aeb2ad****"
        // 设置模板名称
        request.TemplateName = "New AI Template Name"
    
        // 设置模板详细配置
        auditItem := []string{"terrorism", "porn"}
        auditRange := []string{"video", "image-cover"}
        auditContent := []string{"screen"}
        templateConfig := map[string]interface{}{"AuditItem": auditItem, "AuditRange": auditRange,
            "AuditContent": auditContent, "AuditAutoBlock": "yes"}
    
        jsonConfig, err := json.Marshal(templateConfig)
        if err != nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.TemplateConfig = string(jsonConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.UpdateAITemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err != nil {
            panic(err)
        }
    
        response, err := MyUpdateAITemplate(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



查询AI模板 {#h2--ai-div-id-getaitemplate-div-7}
-------------------------------------------

调用GetAITemplate接口，完成查询AI模板功能。
接口参数和返回字段请参见[GetAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板.md)。调用示例如下： {#h2--ai-div-id-getaitemplate-div-7}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyGetAITemplate(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TemplateInfo)
    }



查询AI模板列表 {#h2--ai-div-id-listaitemplate-div-8}
----------------------------------------------

调用ListAITemplate接口，完成查询AI模板列表功能。
接口参数和返回字段请参见[ListAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询AI模板列表.md)。调用示例如下： {#h2--ai-div-id-listaitemplate-div-8}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyListAITemplate(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TemplateInfoList)
    }



设置默认AI模板 {#h2--ai-div-id-setdefaultaitemplate-div-9}
----------------------------------------------------

调用SetDefaultAITemplate接口，完成设置默认AI模板功能。
接口参数和返回字段请参见[SetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/设置默认AI模板.md)。调用示例如下： {#h2--ai-div-id-setdefaultaitemplate-div-9}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MySetDefaultAITemplate(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



查询默认AI模板 {#h2--ai-div-id-getdefaultaitemplate-div-10}
-----------------------------------------------------

调用GetDefaultAITemplate接口，完成查询默认AI模板功能。
接口参数和返回字段请参见[GetDefaultAITemplate](/cn.zh-CN/服务端API/视频AI/AI模板/查询默认AI模板.md)。调用示例如下： {#h2--ai-div-id-getdefaultaitemplate-div-10}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
        if err != nil {
            panic(err)
        }
    
        response, err := MyGetDefaultAITemplate(client)
        if err != nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TemplateInfo)
    }


