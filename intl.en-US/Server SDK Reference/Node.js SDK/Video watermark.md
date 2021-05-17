Video watermark 
====================================

This topic provides examples on how to use the API operations of the video watermark module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to create, modify, delete, and query watermarks. You can also specify a watermark as the default one.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Create a watermark {#h2--div-id-addwatermark-div-2}
---------------------------------------------------

You can call the AddWatermark operation to create a watermark.
For more information about the request and response parameters of this operation, see [AddWatermark](/intl.en-US/API Reference/Media processing/Video watermark/AddWatermark.md). Example:
**Note**
* For more information about how to obtain the upload URL and credential, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md).


* For more information about how to upload a watermark file to an Object Storage Service (OSS) bucket, see [Upload OSS objects](/intl.en-US/API Reference/Media upload/Upload OSS objects.md).


 {#h2--div-id-addwatermark-div-2}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // The position configurations of an image watermark.
    var watermarkConfig = {
        Dx: '8',   // The horizontal offset of the watermark on the output video.
        Dy: '8',   // The vertical offset of the watermark on the output video.
        Width: '55',  // The width of the watermark on the output video.
        Height: '55',  // The height of the watermark on the output video.
        ReferPos: 'BottomRight',  // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner.
        // The timeline of the watermark display. You can specify the start time and duration for the watermark display.
        Timeline: {
            Start: '2',  // The start time for the watermark display.
            Duration: 'ToEND'  // The duration for the watermark display.
        }
    };
    // The position configurations of a text watermark.
    // var watermarkConfig = {
    //     Content: 'testwatermark',  // The text to use as the watermark.
    //     FontName: 'SimSun',  // The font to use for the watermark.
    //     FontSize: 25,  // The font size to use for the watermark.
    //     FontColor: 'Black',  // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000.
    //     FontAlpha: '0.2',    // The transparency to use for the watermark.
    //     BorderColor: 'White',  // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff.
    //     BorderWidth: 1,  // The stroke width to use for the watermark.
    //     Top: 20,  // The distance between the upper-left vertex of the watermark and the upper edge of the output video.
    //     Left: 15  // The distance between the upper-left vertex of the watermark and the left edge of the output video.
    // };
    
    client.request("AddWatermark", {
        Name: 'addwatermark',  // The name of the watermark.
        // Obtain the URL of the watermark file that is stored in an OSS bucket. If you want to create an image watermark, you must specify the URL of the watermark file. The OSS bucket that stores the watermark file must reside in the same region as the region where the video is stored.
        // For example, if a video is stored in the China (Shanghai) region, it can use only a watermark file that is stored in the same region.
        FileUrl: 'http://test-bucket.oss-cn-shanghai.aliyuncs.com/watermark/test.png',
        WatermarkConfig: JSON.stringify(watermarkConfig),
        Type: 'Image'
    }, {}).then(function (response) {
        if (response.WatermarkInfo){
            // The ID of the watermark.
            console.log('WatermarkId = ' + response.WatermarkInfo.WatermarkId);
            // The position and effect configurations of the watermark.
            console.log('WatermarkConfig = ' + response.WatermarkInfo.WatermarkConfig);
            // The URL of the watermark file. If you want to create a text watermark, leave this parameter empty.
            console.log('FileUrl = ' + response.WatermarkInfo.FileUrl);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify a watermark {#h2--div-id-updatewatermark-div-3}
------------------------------------------------------

You can call the UpdateWatermark operation to modify a watermark.
For more information about the request and response parameters of this operation, see [UpdateWatermark](/intl.en-US/API Reference/Media processing/Video watermark/UpdateWatermark.md). Example: {#h2--div-id-updatewatermark-div-3}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    // The position configurations of an image watermark.
    var watermarkConfig = {
        Dx: '8',   // The horizontal offset of the watermark on the output video.
        Dy: '8',   // The vertical offset of the watermark on the output video.
        Width: '55',  // The width of the watermark on the output video.
        Height: '55',  // The height of the watermark on the output video.
        ReferPos: 'BottomRight',  // The approximate position of the watermark relative to the output video. The watermark can be in the upper-left corner, upper-right corner, lower-left corner, or lower-right corner.
        // The timeline of the watermark display. You can specify the start time and duration for the watermark display.
        Timeline: {
            Start: '2',  // The start time for the watermark display.
            Duration: 'ToEND'  // The duration for the watermark display.
        }
    };
    // The position configurations of a text watermark.
    // var watermarkConfig = {
    //     Content: 'testwatermark',  // The text to use as the watermark.
    //     FontName: 'SimSun',  // The font to use for the watermark.
    //     FontSize: 25,  // The font size to use for the watermark.
    //     FontColor: 'Black',  // The font color to use for the watermark. You can specify a color name or RGB color code, such as #000000.
    //     FontAlpha: '0.2',    // The transparency to use for the watermark.
    //     BorderColor: 'White',  // The stroke color to use for the watermark. You can specify a color name or RGB color code, such as #ffffff.
    //     BorderWidth: 1,  // The stroke width to use for the watermark.
    //     Top: 20,  // The distance between the upper-left vertex of the watermark and the upper edge of the output video.
    //     Left: 15  // The distance between the upper-left vertex of the watermark and the left edge of the output video.
    // };
    
    client.request("UpdateWatermark", {
        WatermarkId: 'WatermarkId',
        Name: 'updatewatermark',  // The name of the watermark.
        WatermarkConfig: JSON.stringify(watermarkConfig)
    }, {}).then(function (response) {
        if (response.WatermarkInfo){
            // The ID of the watermark.
            console.log('WatermarkId = ' + response.WatermarkInfo.WatermarkId);
            // The position and effect configurations of the watermark.
            console.log('WatermarkConfig = ' + response.WatermarkInfo.WatermarkConfig);
            // The URL of the watermark file. If you want to modify a text watermark, leave this parameter empty.
            console.log('FileUrl = ' + response.WatermarkInfo.FileUrl);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete a watermark {#h2--div-id-deletewatermark-div-4}
------------------------------------------------------

You can call the DeleteWatermark operation to delete a watermark.
For more information about the request and response parameters of this operation, see [DeleteWatermark](/intl.en-US/API Reference/Media processing/Video watermark/DeleteWatermark.md). Example: {#h2--div-id-deletewatermark-div-4}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("DeleteWatermark", {
        WatermarkId: 'WatermarkId'
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query watermarks {#h2--div-id-listwatermark-div-5}
--------------------------------------------------

You can call the ListWatermark operation to query watermarks.
For more information about the request and response parameters of this operation, see [ListWatermark](/intl.en-US/API Reference/Media processing/Video watermark/ListWatermark.md). Example: {#h2--div-id-listwatermark-div-5}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("ListWatermark", {}, {}).then(function (response) {
        if (response.WatermarkInfos && response.WatermarkInfos.length > 0){
            for (var i=0; i<response.WatermarkInfos.length; i++){
                // The ID of the watermark.
                console.log('WatermarkId = ' + response.WatermarkInfos[i].WatermarkId);
                // The position and effect configurations of the watermark.
                console.log('WatermarkConfig = ' + response.WatermarkInfos[i].WatermarkConfig);
                // The URL of the watermark file. If you want to query text watermarks, leave this parameter empty.
                console.log('FileUrl = ' + response.WatermarkInfos[i].FileUrl);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query a watermark {#h2--div-id-getwatermark-div-6}
--------------------------------------------------

You can call the GetWatermark operation to query details about a watermark.
For more information about the request and response parameters of this operation, see [GetWatermark](/intl.en-US/API Reference/Media processing/Video watermark/GetWatermark.md). Example: {#h2--div-id-getwatermark-div-6}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("GetWatermark", {
        WatermarkId: 'WatermarkId'
    }, {}).then(function (response) {
        if (response.WatermarkInfo){
            // The ID of the watermark.
            console.log('WatermarkId = ' + response.WatermarkInfo.WatermarkId);
            // The position and effect configurations of the watermark.
            console.log('WatermarkConfig = ' + response.WatermarkInfo.WatermarkConfig);
            // The URL of the watermark file. If you want to query details about a text watermark, leave this parameter empty.
            console.log('FileUrl = ' + response.WatermarkInfo.FileUrl);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Specify a watermark as the default one {#h2--div-id-setdefaultwatermark-div-7}
------------------------------------------------------------------------------

You can call the SetDefaultWatermark operation to specify a watermark as the default one.
For more information about the request and response parameters of this operation, see [SetDefaultWatermark](/intl.en-US/API Reference/Media processing/Video watermark/SetDefaultWatermark.md). Example: {#h2--div-id-setdefaultwatermark-div-7}
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("SetDefaultWatermark", {
        WatermarkId: 'WatermarkId'
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


