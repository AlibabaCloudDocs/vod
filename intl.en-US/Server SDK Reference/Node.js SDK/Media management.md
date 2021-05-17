Media management 
=====================================

This topic provides examples on how to use the API operations of the media management module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to search for media asset information, modify video information, and query source file information. You can also query and delete videos and images.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Search for media asset information {#h2--div-id-searchmedia-div-2}
------------------------------------------------------------------

You can call the SearchMedia operation to search for media asset information.
For more information about the request and response parameters of this operation, see [SearchMedia](/intl.en-US/API Reference/Media asset management/Media asset search/SearchMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("SearchMedia", {
        Fields: 'Title,CoverURL,Status',
        Match: "Status in ('Normal','Checking') and CreationTime = ('2018-07-01T08:00:00Z','2018-08-01T08:00:00Z')",
        PageNo: 1,
        PageSize: 10,
        SearchType: 'video',
        SortBy: 'CreationTime:Desc'
    }, {}).then(function (response) {
        console.log("Total = " + response.Total);
        console.log("ScrollToken = " + response.ScrollToken);
        if (response.MediaList && response.MediaList && response.MediaList.length > 0){
            for (var i=0; i<response.MediaList.length; i++){
                console.log("MediaId = " + response.MediaList[i].MediaId);
                console.log("MediaType = " + response.MediaList[i].MediaType);
                console.log("CreationTime = " + response.MediaList[i].CreationTime);
                console.log("Title = " + response.MediaList[i].Video.Title);
                console.log("CoverURL = " + response.MediaList[i].Video.CoverURL);
                console.log("Status = " + response.MediaList[i].Video.Status);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query a video {#h2--div-id-getvideoinfo-div-3}
----------------------------------------------

You can call the GetVideoInfo operation to query details about a video.
For more information about the request and response parameters of this operation, see [GetVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfo.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("GetVideoInfo", {
        VideoId: 'VideoId'
    }, {}).then(function (response) {
        if (response.Video){
            console.log("Title = " + response.Video.Title);
            console.log("Description = " + response.Video.Description);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query videos {#h2--div-id-getvideoinfos-div-4}
----------------------------------------------

You can call the GetVideoInfos operation to query videos.
For more information about the request and response parameters of this operation, see [GetVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfos.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("GetVideoInfos", {
        VideoIds: 'Video1,Video2'
    }, {}).then(function (response) {
        if (response.VideoList && response.VideoList.length > 0){
            console.log("===== exist video infos : =====");
            for (var i=0; i<response.VideoList.length; i++) {
                var video = response.VideoList[i];
                console.log("VideoId = " + video.VideoId);
                console.log("Title = " + video.Title);
                console.log("Description = " + video.Description);
                console.log("Tags = " + video.Tags);
                console.log("CreationTime = " + video.CreationTime);
            }
        }
        if (response.NonExistVideoIds && response.NonExistVideoIds.length > 0){
            console.log("===== nonexistent videoIds : =====");
            for (var i=0; i<response.NonExistVideoIds.length; i++) {
                console.log("VideoId = " + response.NonExistVideoIds[i]);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify the information about a video {#h2--div-id-updatevideoinfo-div-5}
------------------------------------------------------------------------

You can call the UpdateVideoInfo operation to modify the information about a video.
For more information about the request and response parameters of this operation, see [UpdateVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfo.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("UpdateVideoInfo", {
        VideoId: 'VideoId',
        Title: 'new Title',
        Description: 'new Description',
        Tags: 'new Tag1,new Tag2'
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify the information about videos {#h2--div-id-updatevideoinfos-div-6}
------------------------------------------------------------------------

You can call the UpdateVideoInfos operation to modify the information about videos.
For more information about the request and response parameters of this operation, see [UpdateVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfos.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    var updateContent = [{
        VideoId: 'VideoId1',
        Title: 'new Title',
        Tags: 'new Tag1,new Tag2'
    },{
        VideoId: 'VideoId2',
        Title: 'new Title',
        Tags: 'new Tag1,new Tag2'
    }];
    client.request("UpdateVideoInfos", {
        UpdateContent: JSON.stringify(updateContent)
    }, {}).then(function (response) {
        if (response.NonExistVideoIds && response.NonExistVideoIds.length > 0){
            console.log("===== nonexistent videoIds : =====");
            for (var i=0; i<response.NonExistVideoIds.length; i++) {
                console.log("VideoId = " + response.NonExistVideoIds[i]);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete videos {#h2--div-id-deletevideo-div-7}
---------------------------------------------

You can call the DeleteVideo operation to delete videos.
For more information about the request and response parameters of this operation, see [DeleteVideo](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteVideo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("DeleteVideo", {
        VideoIds: 'Video1,Video2'
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query source file information (including the file URL) {#h2--div-id-getmezzanineinfo-div-}
------------------------------------------------------------------------------------------

You can call the GetMezzanineInfo operation to query source file information.
For more information about the request and response parameters of this operation, see [GetMezzanineInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetMezzanineInfo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("GetMezzanineInfo", {
        VideoId: 'VideoId',
        AuthTimeout: 3600   // The expiration time of the file URL.
    }, {}).then(function (response) {
        if (response.Mezzanine){
            console.log('Mezzanine.VideoId = ' + response.Mezzanine.VideoId);
            console.log('Mezzanine.FileURL = ' + response.Mezzanine.FileURL);
            console.log('Mezzanine.Width = ' + response.Mezzanine.Width);
            console.log('Mezzanine.Height = ' + response.Mezzanine.Height);
            console.log('Mezzanine.Size = ' + response.Mezzanine.Size);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query videos by using filter conditions {#h2--div-id-getvideolist-div-8}
------------------------------------------------------------------------

You can call the GetVideoList operation to query videos by using filter conditions.
For more information about the request and response parameters of this operation, see [GetVideoList](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoList.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("GetVideoList", {
        StartTime: '2018-12-28T06:00:00Z',
        EndTime: '2018-12-28T14:00:00Z',
        PageNo: 1,
        PageSize: 2
    }, {}).then(function (response) {
        // The total number of videos that are returned based on the filter conditions
        console.log('Total = ' + response.Total);
        if (response.VideoList && response.VideoList.Video && response.VideoList.Video.length > 0){
            for (var i=0; i<response.VideoList.Video.length; i++){
                var video = response.VideoList.Video[i];
                console.log('Title = ' + video.Title);
                console.log('Description = ' + video.Description);
                console.log('Tags = ' + video.Tags);
                console.log('CreationTime = ' + video.CreationTime);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete a media stream {#h2--div-id-deletestream-div-9}
------------------------------------------------------

You can call the DeleteStream operation to delete a media stream.
For more information about the request and response parameters of this operation, see [DeleteStream](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteStream.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("DeleteStream", {
        VideoId: 'VideoId',
        JobIds: 'JobId1,JobId2'
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete source files {#h2--div-id-deletemezzanines-div-10}
---------------------------------------------------------

You can call the DeleteMezzanines operation to delete source files.
For more information about the request and response parameters of this operation, see [DeleteMezzanines](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteMezzanines.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("DeleteMezzanines", {
        VideoIds: 'VideoId',
        Force: false
    }, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Modify the information about images {#h2--div-id-updateimageinfos-div-11}
-------------------------------------------------------------------------

You can call the UpdateImageInfos operation to modify the information about images.
For more information about the request and response parameters of this operation, see [UpdateImageInfos](/intl.en-US/API Reference/Media asset management/Image management/UpdateImageInfos.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    var updateContent = [{
        ImageId: 'ImageId1',
        Title: 'new title',
        Tags: 'new Tag1,new Tag2'
    },{
        ImageId: 'ImageId2',
        Title: 'new title',
        Tags: 'new Tag1,new Tag2'
    }];
    client.request("UpdateImageInfos", {
        UpdateContent: JSON.stringify(updateContent)
    }, {}).then(function (response) {
        if (response.NonExistImageIds && response.NonExistImageIds.ImageId && response.NonExistImageIds.ImageId.length > 0) {
            console.log("======nonexistent ImageIds : ======");
            console.log('ImageId = ' + response.NonExistImageIds.ImageId);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Query an image {#h2--div-id-getimageinfo-div-12}
------------------------------------------------

You can call the GetImageInfo operation to query details about an image.
For more information about the request and response parameters of this operation, see [GetImageInfo](/intl.en-US/API Reference/Media asset management/Image management/GetImageInfo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    client.request("GetImageInfo", {
        ImageId: 'ImageId1'
    }, {}).then(function (response) {
        if (response.ImageInfo) {
            console.log('ImageId = ' + response.ImageInfo.ImageId);
            console.log('Title = ' + response.ImageInfo.Title);
            console.log('CreationTime = ' + response.ImageInfo.CreationTime);
            console.log('FileURL = ' + response.ImageInfo.Mezzanine.FileURL);
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Delete images {#h2--div-id-deleteimage-div-13}
----------------------------------------------

You can call the DeleteImage operation to delete images.
For more information about the request and response parameters of this operation, see [DeleteImage](/intl.en-US/API Reference/Media asset management/Image management/DeleteImage.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>', '<Your AccessKeySecret>');
    
    // Delete an image file based on ImageURL.
    var paras = {
        DeleteImageType: 'ImageURL',
        ImageURLs: 'http://sample.aliyun.com/cover.jpg'
    };
    // Delete image files based on ImageId.
    // var paras = {
    //     DeleteImageType: 'ImageId',
    //     ImageIds: 'ImageId1,ImageId2'
    // };
    // Delete image files based on VideoId and ImageType.
    // var paras = {
    //     DeleteImageType: 'VideoId',
    //     VideoId: 'http://sample.aliyun.com/cover.jpg',
    //     ImageType: 'SpriteSnapshot'
    // };
    client.request("DeleteImage", paras, {}).then(function (response) {
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


