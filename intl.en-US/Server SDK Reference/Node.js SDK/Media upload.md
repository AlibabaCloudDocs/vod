Media upload 
=================================

This topic provides examples on how to use the API operations of the media upload module. The API operations are encapsulated in ApsaraVideo VOD SDK for Node.js. You can call the API operations to create upload URLs and credentials and register media assets. You can also upload media files by using a source file URL.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Node.js SDK/Initialization.md).

Create a URL and a credential for uploading videos {#h2--div-id-createuploadvideo-div-2}
----------------------------------------------------------------------------------------

You can call the CreateUploadVideo operation to create a URL and a credential for uploading videos.
For more information about the request and response parameters of this operation, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("CreateUploadVideo", {
        Title: 'this is a sample',
        FileName: 'filename.mp4'
    }, {}).then(function (response) {
        console.log('VideoId = ' + response.VideoId);
        console.log('UploadAddress = ' + response.UploadAddress);
        console.log('UploadAuth = ' + response.UploadAuth);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Refresh the credential for uploading videos {#h2--div-id-refreshuploadvideo-div-3}
----------------------------------------------------------------------------------

You can call the RefreshUploadVideo operation to refresh the credential for uploading videos.
For more information about the request and response parameters of this operation, see [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("RefreshUploadVideo", {
        VideoId: 'VideoId'
    }, {}).then(function (response) {
        console.log('UploadAddress = ' + response.UploadAddress);
        console.log('UploadAuth = ' + response.UploadAuth);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Create a URL and a credential for uploading images {#h2--div-id-createuploadimage-div-4}
----------------------------------------------------------------------------------------

You can call the CreateUploadImage operation to create a URL and a credential for uploading images.
For more information about the request and response parameters of this operation, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("CreateUploadImage", {
        ImageType: 'cover',
        ImageExt: 'jpg'
    }, {}).then(function (response) {
        console.log('ImageId = ' + response.ImageId);
        console.log('ImageURL = ' + response.ImageURL);
        console.log('UploadAddress = ' + response.UploadAddress);
        console.log('UploadAuth = ' + response.UploadAuth);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Create a URL and a credential for uploading attached media assets {#h2--div-id-createuploadattachedmedia-div-5}
---------------------------------------------------------------------------------------------------------------

You can call the CreateUploadAttachedMedia operation to create a URL and a credential for uploading attached media assets.
For more information about the request and response parameters of this operation, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    client.request("CreateUploadAttachedMedia", {
        BusinessType: 'watermark',
        MediaExt: 'gif',
        Title: 'this is a sample'
    }, {}).then(function (response) {
        console.log('MediaId = ' + response.MediaId);
        console.log('MediaURL = ' + response.MediaURL);
        console.log('UploadAddress = ' + response.UploadAddress);
        console.log('UploadAuth = ' + response.UploadAuth);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Upload media files by using a source file URL {#h2-url-div-id-uploadmediabyurl-div-6}
-------------------------------------------------------------------------------------

You can call the UploadMediaByURL operation to upload media files by using a source file URL.
For more information about the request and response parameters of this operation, see [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    var url = 'http://xxxx.mp4';
    var uploadMetadatas = [{
        SourceUrl: url,
        Title: 'upload by url sample'
    }];
    client.request("UploadMediaByURL", {
        UploadURLs: url,
        UploadMetadatas: JSON.stringify(uploadMetadatas)
    }, {}).then(function (response) {
        console.log('UploadJobs = ');
        console.log(response.UploadJobs);
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });



Register media assets {#h2--div-id-registermedia-div-7}
-------------------------------------------------------

You can call the RegisterMedia operation to register media assets.
For more information about the request and response parameters of this operation, see [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    // Call example
    var client = initVodClient('<Your AccessKeyId>','<Your AccessKeySecret>');
    
    var url = 'http://192.168.0.0/16.mp4';
    var registerMetadatas = [{
        FileURL: url,
        Title: 'this is a sample'
    }];
    client.request("RegisterMedia", {
        RegisterMetadatas: JSON.stringify(registerMetadatas)
    }, {}).then(function (response) {
        if (response.FailedFileURLs && response.FailedFileURLs.length > 0){
            for (var i=0; i<response.FailedFileURLs.length; i++) {
                console.log('FailedFileURL = ' + response.FailedFileURLs[i]);
            }
        }
        if (response.RegisteredMediaList && response.RegisteredMediaList.length > 0){
            for (var i=0; i<response.RegisteredMediaList.length; i++) {
                console.log('MediaId = ' + response.RegisteredMediaList[i].MediaId);
                console.log('FileURL = ' + response.RegisteredMediaList[i].FileURL);
                console.log('NewRegister = ' + response.RegisteredMediaList[i].NewRegister);
            }
        }
        console.log('RequestId = ' + response.RequestId);
    }).catch(function (response) {
        console.log('ErrorCode = ' + response.data.Code);
        console.log('ErrorMessage = ' + response.data.Message);
        console.log('RequestId = ' + response.data.RequestId);
    });


