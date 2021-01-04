Video watermark 
====================================

This topic provides examples on how to use the API operations of the video watermark module. The API operations are encapsulated in ApsaraVideo VOD SDK for Go. You can call the API operations to create, modify, delete, and query watermarks. You can also specify a watermark as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

Create a watermark {#h2--div-id-addwatermark-div-2}
---------------------------------------------------

You can call the AddWatermark operation to create a watermark.
For more information about the request and response parameters of this operation, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/AddWatermark.md). Example:
**Note**
* For more information about how to query the upload URL and credential, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).


* For more information about how to upload a watermark file to an Object Storage Service (OSS) bucket, see [Upload OSS objects](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).


 {#h2--div-id-addwatermark-div-2}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyAddWatermark(client *vod.Client) (response *vod.AddWatermarkResponse, err error) {
        request := vod.CreateAddWatermarkRequest()
    
        request.Name = "watermark-sample"
    
        // If you want to create an image watermark, you must specify the URL of the watermark file. The OSS bucket that stores the watermark file must reside in the same region as the region where the video is stored. For example, if a video is stored in the China (Shanghai) region, it can use only a watermark file that is stored in the same region.
        request.FileUrl = "http://sample.oss-cn-shanghai.aliyuncs.com/watermark/test.png"
    
        // Example on how to configure a text watermark:
        request.Type = "Text"
        // The watermark configurations, including the text, font, font size, font color, and transparency to use for the watermark.
        watermarkConfig := map[string]interface{}{"Content": "watermark Text", "FontName": "SimSun", "FontSize": 25,
            "FontColor": "Black", "FontAlpha": 0.2, "BorderColor": "White", "BorderWidth": 1, "Top": 20, "Left": 15}
        jsonConfig, err := json.Marshal(watermarkConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.WatermarkConfig = string(jsonConfig)
    
        /* 
        // Example on how to configure an image watermark:
        request.Type = "Image"
        // The start time and duration for the watermark display.
        timeline := map[string]interface{}{"Start": 2, "Duration": "ToEND"}
        // The position configurations of the watermark.
        watermarkConfig := map[string]interface{}{"Dx": 8, "Dy": 8, "Width": 55, "Height": 55, "ReferPos": "BottomRight", "Timeline": timeline}
        jsonConfig, err := json.Marshal(watermarkConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.WatermarkConfig = string(jsonConfig)
        */
    
        request.AcceptFormat = "JSON"
    
        return client.AddWatermark(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyAddWatermark(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Printf("%s: %s\n", response.WatermarkInfo.WatermarkId, response.WatermarkInfo.WatermarkConfig)
    }



Modify a watermark {#h2--div-id-updatewatermark-div-3}
------------------------------------------------------

You can call the UpdateWatermark operation to modify a watermark.
For more information about the request and response parameters of this operation, see [UpdateWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/UpdateWatermark.md). Example:
**Notice**
If you want to call this operation to modify the file URL of an image watermark, you must create a watermark. {#h2--div-id-updatewatermark-div-3}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyUpdateWatermark(client *vod.Client) (response *vod.UpdateWatermarkResponse, err error) {
        request := vod.CreateUpdateWatermarkRequest()
    
        request.WatermarkId = "5a5abf8e458a9d5c97dea86e686cdf18"
        request.Name = "new-watermark-name"
    
        // Example on how to modify a text watermark:
        // The watermark configurations, including the text, font, font size, font color, and transparency to use for the watermark.
        watermarkConfig := map[string]interface{}{"Content": "New watermark Text", "FontName": "SimSun", "FontSize": 25,
            "FontColor": "Black", "FontAlpha": 0.2, "BorderColor": "White", "BorderWidth": 1, "Top": 20, "Left": 15}
        jsonConfig, err := json.Marshal(watermarkConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.WatermarkConfig = string(jsonConfig)
    
        /*
        // Example on how to configure an image watermark:
        // The start time and duration for the watermark display.
        timeline := map[string]interface{}{"Start": 2, "Duration": "ToEND"}
        // The position configurations of the watermark.
        watermarkConfig := map[string]interface{}{"Dx": 8, "Dy": 8, "Width": 55, "Height": 55, "ReferPos": "BottomRight",
            "Timeline": timeline}
        jsonConfig, err := json.Marshal(watermarkConfig)
        if err ! = nil {
            fmt.Println("json.Marshal failed:", err)
            return
        }
        request.WatermarkConfig = string(jsonConfig)
        */
    
        request.AcceptFormat = "JSON"
    
        return client.UpdateWatermark(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyUpdateWatermark(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        fmt.Printf("%s: %s\n", response.WatermarkInfo.WatermarkId, response.WatermarkInfo.WatermarkConfig)
    }



Delete a watermark {#h2--div-id-deletewatermark-div-4}
------------------------------------------------------

You can call the DeleteWatermark operation to delete a watermark.
For more information about the request and response parameters of this operation, see [DeleteWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/DeleteWatermark.md). Example: {#h2--div-id-deletewatermark-div-4}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyDeleteWatermark(client *vod.Client) (response *vod.DeleteWatermarkResponse, err error) {
        request := vod.CreateDeleteWatermarkRequest()
        request.WatermarkId = "<WatermarkId>"
    
        request.AcceptFormat = "JSON"
    
        return client.DeleteWatermark(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyDeleteWatermark(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }



Query watermarks {#h2--div-id-listwatermark-div-5}
--------------------------------------------------

You can call the ListWatermark operation to query watermarks.
For more information about the request and response parameters of this operation, see [ListWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/ListWatermark.md). Example: {#h2--div-id-listwatermark-div-5}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyListWatermark(client *vod.Client) (response *vod.ListWatermarkResponse, err error) {
        request := vod.CreateListWatermarkRequest()
    
        request.AcceptFormat = "JSON"
    
        return client.ListWatermark(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyListWatermark(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        for _, watermark := range response.WatermarkInfos {
            fmt.Printf("%s: %s %s\n", watermark.WatermarkId, watermark.Name, watermark.WatermarkConfig)
        }
    }



Query a watermark {#h2--div-id-getwatermark-div-6}
--------------------------------------------------

You can call the GetWatermark operation to query details about a watermark.
For more information about the request and response parameters of this operation, see [GetWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/GetWatermark.md). Example: {#h2--div-id-getwatermark-div-6}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MyGetWatermark(client *vod.Client) (response *vod.GetWatermarkResponse, err error) {
        request := vod.CreateGetWatermarkRequest()
        request.WatermarkId = "<WatermarkId>"
    
        request.AcceptFormat = "JSON"
    
        return client.GetWatermark(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MyGetWatermark(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
        watermark := response.WatermarkInfo
        fmt.Printf("%s: %s %s\n", response.WatermarkInfo.WatermarkId, watermark.Name, watermark.WatermarkConfig)
    }



Specify a watermark as the default one {#h2--div-id-setdefaultwatermark-div-7}
------------------------------------------------------------------------------

You can call the SetDefaultWatermark operation to specify a watermark as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video Watermark/SetDefaultWatermark.md). Example: {#h2--div-id-setdefaultwatermark-div-7}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    package main
    
    import (
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/services/vod"
        "192.168.0.0/16/aliyun/alibaba-cloud-sdk-go/sdk/auth/credentials"
        "encoding/json"
        "fmt"
    )
    
    func MySetDefaultWatermark(client *vod.Client) (response *vod.SetDefaultWatermarkResponse, err error) {
        request := vod.CreateSetDefaultWatermarkRequest()
        request.WatermarkId = "<WatermarkId>"
    
        request.AcceptFormat = "JSON"
    
        return client.SetDefaultWatermark(request)
    }
    
    func main() {
        client, err := InitVodClient("<accessKeyId>", "<accessKeySecret>")
        if err ! = nil {
            panic(err)
        }
    
        response, err := MySetDefaultWatermark(client)
        if err ! = nil {
            panic(err)
        }
    
        fmt.Println(response.GetHttpContentString())
        fmt.Println(response.RequestId)
    }


