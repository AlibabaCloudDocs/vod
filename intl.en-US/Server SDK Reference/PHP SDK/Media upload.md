Media upload 
=================================

This topic provides examples on how to use the API operations of the media upload module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to create upload URLs and credentials and register media assets. To upload complete media files, you can use the client to upload the files or use the server-side upload SDK for PHP to upload the files.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Create a URL and a credential for uploading videos {#h2--div-id-createuploadvideo-div-2}
----------------------------------------------------------------------------------------

You can call the CreateUploadVideo operation to create a URL and a credential for uploading videos.

For more information about the request and response parameters of this operation, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md). Example:

    /**
     * Create a URL and a credential for uploading videos.
     * @param client The client that is used to send requests.
     * @return CreateUploadVideoResponse The fields that must be contained in the response.
     */
    function createUploadVideo($client) {
        $request = new vod\CreateUploadVideoRequest();
        $request->setTitle("Sample Title");        
        $request->setFileName("videoFile.mov"); 
        $request->setDescription("Video Description");
        $request->setCoverURL("http://192.168.0.0/16/tps/TB1qnJ1PVXXXXXCXXXXXXXXXXXX-700-700.png"); 
        $request->setTags("tag1,tag2");
    
        $request->setAcceptFormat('JSON');
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $uploadInfo = createUploadVideo($client);
        var_dump($uploadInfo);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Update the credential for uploading videos {#h2--div-id-refreshuploadvideo-div-3}
---------------------------------------------------------------------------------

You can call the RefreshUploadVideo operation to update the credential for uploading videos.
For more information about the request and response parameters of this operation, see [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Update the credential for uploading videos.
     * @param client The client that is used to send requests.
     * @return RefreshUploadVideoResponse The fields that must be contained in the response.
     */
    function refreshUploadVideo($client, $videoId) {
        $request = new vod\RefreshUploadVideoRequest();
        $request->setVideoId($videoId);
        $request->setAcceptFormat('JSON');
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $refreshInfo = refreshUploadVideo($client, 'videoId');
        var_dump($refreshInfo);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Obtain a URL and a credential for uploading images {#h2--div-id-createuploadimage-div-4}
----------------------------------------------------------------------------------------

You can call the CreateUploadImage operation to obtain a URL and a credential for uploading images.
For more information about the request and response parameters of this operation, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Obtain a URL and a credential for uploading images.
     * @param client The client that is used to send requests.
     * @return CreateUploadImageResponse The fields that must be contained in the response.
     */
    function createUploadImage($client, $imageType, $imageExt) {
        $request = new vod\CreateUploadImageRequest();
        $request->setImageType($imageType);
        $request->setImageExt($imageExt);
        $request->setAcceptFormat('JSON');
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $imageInfo = createUploadImage($client, 'cover', 'jpg');
        var_dump($imageInfo);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Create a URL and a credential for uploading attached media assets {#h2--div-id-createuploadattachedmedia-div-5}
---------------------------------------------------------------------------------------------------------------

You can call the CreateUploadAttachedMedia operation to create a URL and a credential for uploading attached media assets.
For more information about the request and response parameters of this operation, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Create a URL and a credential for uploading attached media assets, such as watermarks and subtitles.
     * @param client The client that is used to send requests.
     * @return CreateUploadAttachedMediaResponse The fields that must be contained in the response.
     */
    function createUploadAttachedMedia($client) {
        $request = new vod\CreateUploadAttachedMediaRequest();
        $request->setBusinessType("watermark");
        $request->setMediaExt("gif");
        $request->setTitle("this is a sample");
    
        return $client->getAcsResponse($request);
    }
    
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = createUploadAttachedMedia($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Upload media files by using a source file URL {#h2-url-div-id-uploadmediabyurl-div-6}
-------------------------------------------------------------------------------------

You can call the UploadMediaByURL operation to upload media files by using a source file URL.
For more information about the request and response parameters of this operation, see [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Upload media files by using a source file URL.
     * @param client The client that is used to send requests.
     * @return UploadMediaByURLResponse URL The fields that must be contained in the response.
     */
    function uploadMediaByURL($client) {
        $request = new vod\UploadMediaByURLRequest();
        $url = "http://192.168.0.0/16/***.mp4";
        $request->setUploadURLs($url);
    
        $uploadMetadataList = array();
        $uploadMetadata = array();
        $uploadMetadata["SourceUrl"] = $url;
        $uploadMetadata["Title"] = "upload by url sample";
        $uploadMetadataList[] = $uploadMetadata;
        $request->setUploadMetadatas(json_encode($uploadMetadataList));
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = uploadMediaByURL($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Register media assets {#h2--div-id-registermedia-div-7}
-------------------------------------------------------

You can call the RegisterMedia operation to register media assets.
For more information about the request and response parameters of this operation, see [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Register media assets.
     * @param client The client that is used to send requests.
     * @return RegisterMediaResponse The fields that must be contained in the response.
     */
    function registerMedia($client) {
        $request = new vod\RegisterMediaRequest();
    
        $metaDataArray= array();
        $metaData= array();
        $metaData["Title"] = "registerMedia by url sample";
        $metaData["FileURL"] = "https://192.168.0.0/16/vod_sample.mp4";
        $metaDataArray[] = $metaData;
        $request->setRegisterMetadatas(json_encode($metaDataArray));
    
        return $client->getAcsResponse($request);
    }
    
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = registerMedia($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query the information about uploading data to URLs {#h2--url-div-id-geturluploadinfos-div-8}
--------------------------------------------------------------------------------------------

You can call the GetURLUploadInfos operation to query the information about uploading data to URLs.
For more information about the request and response parameters of this operation, see [GetURLUploadInfos](/intl.en-US/API Reference/Media upload/GetURLUploadInfos.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query the information about uploading data to URLs.
     * @param client The client that is used to send requests.
     * @return GetURLUploadInfosResponse The fields that must be contained in the response.
     */
    function getURLUploadInfos($client) {
        $request = new vod\GetURLUploadInfosRequest();
    
        // The URL list.
        $urls = array();
        $urls[] = "http://192.168.0.0/16/sample1.mp4";
        $urls[] = "http://192.168.0.0/16/sample2.mp4";
    
        // Encoded URLs.
        $uploadURLs = array();
        foreach ($urls as $url) {
           $uploadURLs[] = urlencode($url); 
        }
    
        // The URLs that you want to use to upload media files. Separate multiple URLs with commas (,).
        $request->setUploadURLs(implode(",", $uploadURLs));
    
        // The job IDs that you use to query URLs.
        //$request->setJobIds("jobId1****,jobId2****")
    
        return $client->getAcsResponse($request);
    }
    
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = getURLUploadInfos($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


