Video editing 
==================================

This topic provides examples on how to use the API operations of the video editing module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to create, modify, and delete online editing projects. You can also query details about an online editing project, configure materials for an online project, and create a video assembly task.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Create a video assembly task based on a timeline {#h2--div-id-produceeditingprojectvideo-div-2}
-----------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on a timeline.

The timeline method is most commonly used to assemble videos. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example:
**Note**

For more examples on how to assemble videos based on timelines, see [Video assembly](/intl.en-US/Developer Guide/Online editing/Overview.md).

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func ProduceEditingVideoByTimeline(client *vod.Client) (response *vod.ProduceEditingProjectVideoResponse, err error) {
        request := vod.CreateProduceEditingProjectVideoRequest()
    
        // set timeline, this sample shows how to merge two videos
        videoTrackClips := []map[string]interface{}{}
        videoTrackClip1 := map[string]interface{}{"MediaId": "<VideoId1>"}
        videoTrackClip2 := map[string]interface{}{"MediaId": "<VideoId2>"}
        videoTrackClips = append(videoTrackClips, videoTrackClip1, videoTrackClip2)
        videoTrack := map[string]interface{}{"VideoTrackClips": videoTrackClips}
        videoTracks := []map[string]interface{}{}
        videoTracks = append(videoTracks, videoTrack)
        timeline := map[string]interface{}{"VideoTracks": videoTracks}
        jsonTimeline, err := json.Marshal(timeline)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.Timeline = string(jsonTimeline)
    
        // set media metadata
        mediaMetadata := map[string]interface{}{"Title": "editing sample title", "Description": "editing sample description",
            "Tags": "Tag1,Tag2"}
        jsonMeta, err := json.Marshal(mediaMetadata)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.MediaMetadata = string(jsonMeta)
    
        // set produce config
        /*
        produceConfig := map[string]interface{}{"TemplateGroupId": "<templateGroupId>"}
        jsonConfig, err := json.Marshal(produceConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.ProduceConfig = string(jsonConfig)
        */
    
        request.AcceptFormat = "JSON"
    
        return client.ProduceEditingProjectVideo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := ProduceEditingVideoByTimeline(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.MediaId)
    }



Create a video assembly task based on an online editing project {#h2--div-id-produceeditingprojectvideoprojectid-div-3}
-----------------------------------------------------------------------------------------------------------------------

You can call the ProduceEditingProjectVideo operation to create a video assembly task based on an online editing project.
If you have high requirements for online editing and management, we recommend that you use this method. For more information about the request and response parameters of this operation, see [ProduceEditingProjectVideo](/intl.en-US/API Reference/Online editing/ProduceEditingProjectVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func ProduceEditingVideoByProject(client *vod.Client) (response *vod.ProduceEditingProjectVideoResponse, err error) {
        request := vod.CreateProduceEditingProjectVideoRequest()
    
        // set ProjectId
        request.ProjectId = "<ProjectId>"
    
        // set media metadata
        mediaMetadata := map[string]interface{}{"Title": "editing sample title", "Description": "editing sample description",
            "Tags": "Tag1,Tag2"}
        jsonMeta, err := json.Marshal(mediaMetadata)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.MediaMetadata = string(jsonMeta)
    
        // set produce config
        /*
        produceConfig := map[string]interface{}{"TemplateGroupId": "<templateGroupId>"}
        jsonConfig, err := json.Marshal(produceConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.ProduceConfig = string(jsonConfig)
        */
    
        request.AcceptFormat = "JSON"
    
        return client.ProduceEditingProjectVideo(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := ProduceEditingVideoByProject(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.MediaId)
    }



Create an online editing project {#h2--div-id-addeditingproject-div-4}
----------------------------------------------------------------------

You can call the AddEditingProject operation to create an online editing project.
For more information about the request and response parameters of this operation, see [AddEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/AddEditingProject.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyAddEditingProject(client *vod.Client) (response *vod.AddEditingProjectResponse, err error) {
        request := vod.CreateAddEditingProjectRequest()
    
        // set timeline, this sample shows how to merge two videos
        videoTrackClips := []map[string]interface{}{}
        videoTrackClip1 := map[string]interface{}{"MediaId": "<VideoId1>"}
        videoTrackClip2 := map[string]interface{}{"MediaId": "<VideoId2>"}
        videoTrackClips = append(videoTrackClips, videoTrackClip1, videoTrackClip2)
        videoTrack := map[string]interface{}{"VideoTrackClips": videoTrackClips}
        videoTracks := []map[string]interface{}{}
        videoTracks = append(videoTracks, videoTrack)
        timeline := map[string]interface{}{"VideoTracks": videoTracks}
        jsonTimeline, err := json.Marshal(timeline)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.Timeline = string(jsonTimeline)
    
        // set project metadata
        request.Title = "editing project title"
        request.Description = "editing project description"
    
        request.AcceptFormat = "JSON"
    
        return client.AddEditingProject(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyAddEditingProject(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Println(response.Project.ProjectId)
    }



Modify an online editing project {#h2--div-id-updateeditingproject-div-5}
-------------------------------------------------------------------------

You can call the UpdateEditingProject operation to modify an online editing project.
For more information about the request and response parameters of this operation, see [UpdateEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/UpdateEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyUpdateEditingProject(client *vod.Client) (response *vod.UpdateEditingProjectResponse, err error) {
        request := vod.CreateUpdateEditingProjectRequest()
    
        // set projectId
        request.ProjectId = "<ProjectId>"
    
        // set timeline, this sample shows how to merge two videos
        videoTrackClips := []map[string]interface{}{}
        videoTrackClip1 := map[string]interface{}{"MediaId": "<VideoId1>"}
        videoTrackClip2 := map[string]interface{}{"MediaId": "<VideoId2>"}
        videoTrackClips = append(videoTrackClips, videoTrackClip1, videoTrackClip2)
        videoTrack := map[string]interface{}{"VideoTrackClips": videoTrackClips}
        videoTracks := []map[string]interface{}{}
        videoTracks = append(videoTracks, videoTrack)
        timeline := map[string]interface{}{"VideoTracks": videoTracks}
        jsonTimeline, err := json.Marshal(timeline)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.Timeline = string(jsonTimeline)
    
        // set project metadata
        request.Title = "new editing project title"
        request.Description = "new editing project description"
    
        request.AcceptFormat = "JSON"
    
        return client.UpdateEditingProject(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateEditingProject(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Delete an online editing project {#h2--div-id-deleteeditingproject-div-6}
-------------------------------------------------------------------------

You can call the DeleteEditingProject operation to delete an online editing project.
For more information about the request and response parameters of this operation, see [DeleteEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/DeleteEditingProject.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDeleteEditingProject(client *vod.Client) (response *vod.DeleteEditingProjectResponse, err error) {
        request := vod.CreateDeleteEditingProjectRequest()
        request.ProjectIds = "ProjectId1,ProjectId2"
    
        request.AcceptFormat = "JSON"
    
        return client.DeleteEditingProject(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteEditingProject(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Query an online editing project {#h2--div-id-geteditingproject-div-7}
---------------------------------------------------------------------

You can call the GetEditingProject operation to query details about an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProject.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetEditingProject(client *vod.Client) (response *vod.GetEditingProjectResponse, err error) {
        request := vod.CreateGetEditingProjectRequest()
        request.ProjectId = "<ProjectId>"
    
        request.AcceptFormat = "JSON"
    
        return client.GetEditingProject(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetEditingProject(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Printf("%s: %s\n", response.Project.Title, response.Project.Timeline)
    }



Search for online editing projects {#h2--div-id-searcheditingproject-div-8}
---------------------------------------------------------------------------

You can call the SearchEditingProject operation to search for online editing projects.
For more information about the request and response parameters of this operation, see [SearchEditingProject](/intl.en-US/API Reference/Online editing/Project management for online editing/SearchEditingProject.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MySearchEditingProject(client *vod.Client) (response *vod.SearchEditingProjectResponse, err error) {
        request := vod.CreateSearchEditingProjectRequest()
        request.Title = "<Title Keywords>"
        request.StartTime = "2018-10-11T12:00:00Z"
        request.EndTime =  "2018-12-25T12:00:00Z"
        request.PageNo = "1"
        request.PageSize = "10"
    
        request.AcceptFormat = "JSON"
    
        return client.SearchEditingProject(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySearchEditingProject(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, project := range response.ProjectList.Project {
            fmt.Printf("%s: %s\n", project.ProjectId, project.Title)
        }
    }



Configure materials for an online editing project {#h2--div-id-seteditingprojectmaterials-div-9}
------------------------------------------------------------------------------------------------

You can call the SetEditingProjectMaterials operation to configure materials for an online editing project.
For more information about the request and response parameters of this operation, see [SetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/SetEditingProjectMaterials.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MySetEditingProjectMaterials(client *vod.Client) (response *vod.SetEditingProjectMaterialsResponse, err error) {
        request := vod.CreateSetEditingProjectMaterialsRequest()
        request.ProjectId = "<ProjectId>"
        // The IDs of the materials. Separate multiple IDs with commas (,). The materials include media assets, videos, images, and attached media assets.
        request.MaterialIds = "VideoId,ImageId"
    
        request.AcceptFormat = "JSON"
    
        return client.SetEditingProjectMaterials(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySetEditingProjectMaterials(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Query the materials of an online editing project {#h2--div-id-geteditingprojectmaterials-div-10}
------------------------------------------------------------------------------------------------

You can call the GetEditingProjectMaterials operation to query the materials of an online editing project.
For more information about the request and response parameters of this operation, see [GetEditingProjectMaterials](/intl.en-US/API Reference/Online editing/Project management for online editing/GetEditingProjectMaterials.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetEditingProjectMaterials(client *vod.Client) (response *vod.GetEditingProjectMaterialsResponse, err error) {
        request := vod.CreateGetEditingProjectMaterialsRequest()
        request.ProjectId = "<ProjectId>"
        request.Type = "video"
    
        request.AcceptFormat = "JSON"
    
        return client.GetEditingProjectMaterials(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetEditingProjectMaterials(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, material := range response.MaterialList.Material {
            fmt.Printf("%s: %s\n", material.MaterialId, material.Title)
        }
    }


