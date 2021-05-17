Transcoding template 
=========================================

This topic provides examples on how to use the API operations of the transcoding template module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to create, modify, delete, and query transcoding template groups. You can also specify a transcoding template group as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Create a transcoding template group {#h2--div-id-addtranscodetemplategroup-div-2}
---------------------------------------------------------------------------------

You can call the AddTranscodeTemplateGroup operation to create a transcoding template group.
For more information about the request and response parameters of this operation, see [AddTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/AddTranscodeTemplateGroup.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "encoding/json"
    )
    
    func MyAddTranscodeTemplateGroup(client *vod.Client) (response *vod.AddTranscodeTemplateGroupResponse, err error) {
        request := vod.CreateAddTranscodeTemplateGroupRequest()
    
        request.Name = "SampleTranscodeTemplateGroup"
    
        transcodeTemplateList := BuildTranscodeTemplateList()
        jsonTranscodeConfig, err := json.Marshal(transcodeTemplateList)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.TranscodeTemplateList = string(jsonTranscodeConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.AddTranscodeTemplateGroup(request)
    }
    
    // Build the configurations of the transcoding template.
    func BuildTranscodeTemplateList() (transcodeTemplateList []map[string]interface{}) {
    
        transcodeTemplate := map[string]interface{}{}
    
        // The name of the template.
        transcodeTemplate["TemplateName"] = "MP4-for-Low-Definition"
    
        // The definition.
        transcodeTemplate["Definition"] = "LD"
    
        // The configurations of video stream transcoding.
        videoConfig := map[string]interface{}{"Width": 640, "Bitrate": 400, "Fps": 25, "Remove": false, "Codec": "H.264", "Gop": "250"}
        transcodeTemplate["Video"] = videoConfig
    
        // The configurations of audio stream transcoding.
        audioConfig := map[string]interface{}{"Codec": "AAC", "Bitrate": "64", "Channels": "2", "Samplerate": "32000"}
        transcodeTemplate["Audio"] = audioConfig
    
        // The container for encapsulation.
        container := map[string]interface{}{"Format": "mp4"}
        transcodeTemplate["Container"] = container
    
        // The configurations of conditional transcoding.
        condition := map[string]interface{}{"IsCheckReso": false, "IsCheckResoFail": false, "IsCheckVideoBitrate": false,
            "IsCheckVideoBitrateFail": false, "IsCheckAudioBitrate": false, "IsCheckAudioBitrateFail": false}
        transcodeTemplate["TransConfig"] = condition
    
        /*
        // The configurations of HTTP Live Streaming (HLS) encryption.
        encryptSetting := map[string]interface{}{"EncryptType": "Private"}
        transcodeTemplate["EncryptSetting"] = encryptSetting
        */
    
        // The IDs of associated watermarks.
        watermarkIdList := []string{"USER_DEFAULT_WATERMARK"}
        //watermarkIdList = append(watermarkIdList, "<WatermarkId>")
        transcodeTemplate["WatermarkIds"] = watermarkIdList
    
        transcodeTemplateList = append(transcodeTemplateList, transcodeTemplate)
    
        return transcodeTemplateList
    }
    
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyAddTranscodeTemplateGroup(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.TranscodeTemplateGroupId)
    }



Modify a transcoding template group {#h2--div-id-updatetranscodetemplategroup-div-3}
------------------------------------------------------------------------------------

You can call the UpdateTranscodeTemplateGroup operation to modify a transcoding template group.
For more information about the request and response parameters of this operation, see [UpdateTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/UpdateTranscodeTemplateGroup.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
        "encoding/json"
    )
    
    func MyUpdateTranscodeTemplateGroup(client *vod.Client) (response *vod.UpdateTranscodeTemplateGroupResponse, err error) {
        request := vod.CreateUpdateTranscodeTemplateGroupRequest()
    
        request.TranscodeTemplateGroupId = "<TranscodeTemplateGroupId>"
    
        // Optional. The name of the template group.
        request.Name = "new-SampleTranscodeTemplateGroup"
    
        // Optional. The configurations of the template group.
        transcodeTemplateList := BuildNewTranscodeTemplateList()
        jsonTranscodeConfig, err := json.Marshal(transcodeTemplateList)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.TranscodeTemplateList = string(jsonTranscodeConfig)
    
        request.AcceptFormat = "JSON"
    
        return client.UpdateTranscodeTemplateGroup(request)
    }
    
    // Build the configurations of the transcoding template.
    func BuildNewTranscodeTemplateList() (transcodeTemplateList []map[string]interface{}) {
    
        transcodeTemplate := map[string]interface{}{}
    
        // Required. The ID of the transcoding template.
        transcodeTemplate["TranscodeTemplateId"] = "<TranscodeTemplateId>"
    
        // The following parameters are optional:
    
        // The name of the new template. You must specify this parameter if you want to modify the name of the template.
        transcodeTemplate["TemplateName"] = "new-MP4-for-High-Definition"
    
        // The configurations of video stream transcoding.
        videoConfig := map[string]interface{}{"Width": 640, "Bitrate": 500, "Fps": 60, "Remove": false, "Codec": "H.264", "Gop": "250"}
        transcodeTemplate["Video"] = videoConfig
    
        // The configurations of audio stream transcoding.
        audioConfig := map[string]interface{}{"Codec": "AAC", "Bitrate": "128", "Channels": "2", "Samplerate": "32000"}
        transcodeTemplate["Audio"] = audioConfig
    
        // The container for encapsulation.
        container := map[string]interface{}{"Format": "mp4"}
        transcodeTemplate["Container"] = container
    
        // The configurations of conditional transcoding.
        condition := map[string]interface{}{"IsCheckReso": false, "IsCheckResoFail": false, "IsCheckVideoBitrate": false,
            "IsCheckVideoBitrateFail": false, "IsCheckAudioBitrate": false, "IsCheckAudioBitrateFail": false}
        transcodeTemplate["TransConfig"] = condition
    
        /*
        // The configurations of HLS encryption.
        encryptSetting := map[string]interface{}{"EncryptType": "Private"}
        transcodeTemplate["EncryptSetting"] = encryptSetting
        */
    
        // The IDs of associated watermarks.
        watermarkIdList := []string{"USER_DEFAULT_WATERMARK"}
        //watermarkIdList = append(watermarkIdList, "<WatermarkId>")
        transcodeTemplate["WatermarkIds"] = watermarkIdList
    
        transcodeTemplateList = append(transcodeTemplateList, transcodeTemplate)
    
        return transcodeTemplateList
    }
    
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateTranscodeTemplateGroup(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Query transcoding template groups {#h2--div-id-listtranscodetemplategroup-div-4}
--------------------------------------------------------------------------------

You can call the ListTranscodeTemplateGroup operation to query transcoding template groups.
For more information about the request and response parameters of this operation, see [ListTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/ListTranscodeTemplateGroup.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyListTranscodeTemplateGroup(client *vod.Client) (response *vod.ListTranscodeTemplateGroupResponse, err error) {
        request := vod.CreateListTranscodeTemplateGroupRequest()
    
        request.AcceptFormat = "JSON"
    
        return client.ListTranscodeTemplateGroup(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyListTranscodeTemplateGroup(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        for _, item := range response.TranscodeTemplateGroupList {
            fmt.Printf("%s: %s\n", item.TranscodeTemplateGroupId, item.Name)
        }
    }



Query a transcoding template group {#h2--div-id-gettranscodetemplategroup-div-5}
--------------------------------------------------------------------------------

You can call the GetTranscodeTemplateGroup operation to query details about a transcoding template group.
For more information about the request and response parameters of this operation, see [GetTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/GetTranscodeTemplateGroup.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyGetTranscodeTemplateGroup(client *vod.Client) (response *vod.GetTranscodeTemplateGroupResponse, err error) {
        request := vod.CreateGetTranscodeTemplateGroupRequest()
        request.TranscodeTemplateGroupId = "<TranscodeTemplateGroupId>"
    
        request.AcceptFormat = "JSON"
    
        return client.GetTranscodeTemplateGroup(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetTranscodeTemplateGroup(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        for _, item := range response.TranscodeTemplateGroup.TranscodeTemplateList {
            fmt.Printf("%s: %s\n", item.TranscodeTemplateId, item.TemplateName)
        }
    }



Specify a transcoding template group as the default one {#h2--div-id-setdefaulttranscodetemplategroup-div-6}
------------------------------------------------------------------------------------------------------------

You can call the SetDefaultTranscodeTemplateGroup operation to specify a transcoding template group as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/SetDefaultTranscodeTemplateGroup.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MySetDefaultTranscodeTemplateGroup(client *vod.Client) (response *vod.SetDefaultTranscodeTemplateGroupResponse, err error) {
        request := vod.CreateSetDefaultTranscodeTemplateGroupRequest()
        request.TranscodeTemplateGroupId = "<TranscodeTemplateGroupId>"
    
        request.AcceptFormat = "JSON"
    
        return client.SetDefaultTranscodeTemplateGroup(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySetDefaultTranscodeTemplateGroup(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Delete a transcoding template group {#h2--div-id-deletetranscodetemplategroup-div-7}
------------------------------------------------------------------------------------

You can call the DeleteTranscodeTemplateGroup operation to delete a transcoding template group.
For more information about the request and response parameters of this operation, see [DeleteTranscodeTemplateGroup](/intl.en-US/API Reference/Media processing/Transcoding template/DeleteTranscodeTemplateGroup.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "fmt"
    )
    
    func MyDeleteTranscodeTemplateGroup(client *vod.Client) (response *vod.DeleteTranscodeTemplateGroupResponse, err error) {
        request := vod.CreateDeleteTranscodeTemplateGroupRequest()
        request.TranscodeTemplateGroupId = "<TranscodeTemplateGroupId>"
    
        request.AcceptFormat = "JSON"
    
        return client.DeleteTranscodeTemplateGroup(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteTranscodeTemplateGroup(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }


