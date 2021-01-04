Snapshot template 
======================================

This topic provides examples on how to use the API operations of the snapshot template module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to create, delete, modify, and query snapshot templates.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Create a snapshot template {#h2--div-id-addvodtemplate-div-2}
-------------------------------------------------------------

You can call the AddVodTemplate operation to create a snapshot template.
For more information about the request and response parameters of this operation, see [AddVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/AddVodTemplate.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyAddVodTemplate(client *vod.Client) (response *vod.AddVodTemplateResponse, err error) {
        request := vod.CreateAddVodTemplateRequest()
    
        // The name of the template.
        request.Name = "Sample Snapshot Template"
        // The type of the template. Set the value to Snapshot.
        request.TemplateType = "Snapshot"
    
        // The configurations of the snapshot template.
        snapshotConfig := map[string]interface{}{"Count": 50, "Interval": 1, "SpecifiedOffsetTime": 0, "Width": 200,
            "Height": 200, "FrameType": "normal"}
        templateConfig := map[string]interface{}{"SnapshotConfig": snapshotConfig, "SnapshotType": "NormalSnapshot"}
    
        /*
        // Optional. The configurations of the image sprites. The configurations must be based on those of common snapshots.
        spriteSnapshotConfig := map[string]interface{}{"CellWidth": 120, "CellHeight": 68, "Columns": 3, "Lines": 10,
            "Padding": 20, "Margin": 50, "KeepCellPic": "keep", "Color": "tomato"}
        snapshotConfig["SpriteSnapshotConfig"] = spriteSnapshotConfig
        templateConfig["SnapshotType"] = "SpriteSnapshot"
        */
    
        jsonConfig, err := json.Marshal(templateConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.TemplateConfig = string(jsonConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.AddVodTemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyAddVodTemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.VodTemplateId)
    }



Modify a snapshot template {#h2--div-id-updatevodtemplate-div-3}
----------------------------------------------------------------

You can call the UpdateVodTemplate operation to modify a snapshot template.
For more information about the request and response parameters of this operation, see [UpdateVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/UpdateVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyUpdateVodTemplate(client *vod.Client) (response *vod.UpdateVodTemplateResponse, err error) {
        request := vod.CreateUpdateVodTemplateRequest()
    
        request.VodTemplateId = "c0825c5f4c4a43af56abf9826b2d****"
        // The name of the template.
        request.Name = "New Snapshot Template Name"
    
        // The configurations of the template that you want to modify.
        snapshotConfig := map[string]interface{}{"Count": 50, "Interval": 1, "SpecifiedOffsetTime": 0, "Width": 200,
            "Height": 200, "FrameType": "normal"}
        templateConfig := map[string]interface{}{"SnapshotConfig": snapshotConfig, "SnapshotType": "NormalSnapshot"}
    
        jsonConfig, err := json.Marshal(templateConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.TemplateConfig = string(jsonConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.UpdateVodTemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateVodTemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Delete a snapshot template {#h2--div-id-deletevodtemplate-div-4}
----------------------------------------------------------------

You can call the DeleteVodTemplate operation to delete a snapshot template.
For more information about the request and response parameters of this operation, see [DeleteVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/DeleteVodTemplate.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyDeleteVodTemplate(client *vod.Client) (response *vod.DeleteVodTemplateResponse, err error) {
        request := vod.CreateDeleteVodTemplateRequest()
        request.VodTemplateId = "<TemplateId>"
    
        request.AcceptFormat = "JSON"
    
        return client.DeleteVodTemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteVodTemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Query snapshot templates {#h2--div-id-listvodtemplate-div-5}
------------------------------------------------------------

You can call the ListVodTemplate operation to query snapshot templates.
For more information about the request and response parameters of this operation, see [ListVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/ListVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyListVodTemplate(client *vod.Client) (response *vod.ListVodTemplateResponse, err error) {
        request := vod.CreateListVodTemplateRequest()
        // The type of the template. Set the value to Snapshot.
        request.TemplateType = "Snapshot"
    
        request.AcceptFormat = "JSON"
    
        return client.ListVodTemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyListVodTemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, template := range response.VodTemplateInfoList {
            fmt.Printf("%s: %s %s\n", template.VodTemplateId, template.Name, template.TemplateConfig)
        }
    }



Query a snapshot template {#h2--div-id-getvodtemplate-div-6}
------------------------------------------------------------

You can call the GetVodTemplate operation to query details about a snapshot template.
For more information about the request and response parameters of this operation, see [GetVodTemplate](/intl.en-US/API Reference/Media processing/Snapshot Template/GetVodTemplate.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyGetVodTemplate(client *vod.Client) (response *vod.GetVodTemplateResponse, err error) {
        request := vod.CreateGetVodTemplateRequest()
        request.VodTemplateId = "<TemplateId>"
    
        request.AcceptFormat = "JSON"
    
        return client.GetVodTemplate(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetVodTemplate(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Printf("%s: %s\n", response.VodTemplateInfo.Name, response.VodTemplateInfo.TemplateConfig)
    }


