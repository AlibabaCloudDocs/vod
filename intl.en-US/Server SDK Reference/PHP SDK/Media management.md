Media management 
=====================================

This topic provides examples on how to use the API operations of the media management module. The API operations are encapsulated in ApsaraVideo VOD SDK for PHP. You can call the API operations to search for media asset information, modify video information, and query source file information. You can also query and delete videos and images.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/PHP SDK/Install the SDK/Initialization.md).

Search for media asset information {#h2--div-id-searchmedia-div-2}
------------------------------------------------------------------

You can call the SearchMedia operation to search for media asset information.

For more information about the request and response parameters of this operation, see [SearchMedia](/intl.en-US/API Reference/Media asset management/Media asset search/SearchMedia.md). Example:

    **
     * Search for media asset information.
     * @param client The client that is used to send requests.
     * @return SearchMediaResponse The fields that must be contained in the response.
     */
    function searchMedia($client) {
        $request = new vod\SearchMediaRequest();
        $request->setFields("Title,CoverURL,Status");
        $request->setMatch("Status in ('Normal','Checking') and CreationTime = ('2018-07-01T08:00:00Z','2018-08-01T08:00:00Z')");
        $request->setPageNo(1);
        $request->setPageSize(10);
        $request->setSearchType("video");
        $request->setSortBy("CreationTime:Desc");
    
        return $client->getAcsResponse($request);
    }
    
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = searchMedia($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query a video {#h2--div-id-getvideoinfo-div-3}
----------------------------------------------

You can call the GetVideoInfo operation to query details about a video.
For more information about the request and response parameters of this operation, see [GetVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfo.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query a video.
     * @param client The client that is used to send requests.
     * @return GetVideoInfoResponse The fields that must be contained in the response.
     */
    function getVideoInfo($client, $videoId) {
        $request = new vod\GetVideoInfoRequest();
        $request->setVideoId($videoId);
        $request->setAcceptFormat('JSON');
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $videoInfo = getVideoInfo($client, 'Your videoId');
        var_dump($videoInfo);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query videos {#h2--div-id-getvideoinfos-div-4}
----------------------------------------------

You can call the GetVideoInfos operation to query videos.
For more information about the request and response parameters of this operation, see [GetVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoInfos.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query videos.
     * @param client The client that is used to send requests.
     * @return GetVideoInfosResponse The fields that must be contained in the response.
     */
    function getVideoInfos($client) {
        $request = new vod\GetVideoInfosRequest();
        $request->setVideoIds("e67e761ec04342cd9ca5149c7488****,b19439abb9a94374b7f4d45f6988****");
    
        return $client->getAcsResponse($request);
    }
    
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = getVideoInfos($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify the information about a video {#h2--div-id-updatevideoinfo-div-5}
------------------------------------------------------------------------

You can call the UpdateVideoInfo operation to modify the information about a video.
For more information about the request and response parameters of this operation, see [UpdateVideoInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfo.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Modify the information about a video.
     * @param client The client that is used to send requests.
     * @return UpdateVideoInfoResponse The fields that must be contained in the response.
     */
    function updateVideoInfo($client, $videoId) {
        $request = new vod\UpdateVideoInfoRequest();
        $request->setVideoId($videoId);
        $request->setTitle('New Title');   // The new title of the video.
        $request->setDescription('New Description');    // the new description of the video.
        $request->setCoverURL('http://192.168.0.0/16/tps/TB1qnJ1PVXXXXXCXXXXXXXXXXXX-700-700.png');  // The new cover of the video.
        $request->setTags('tag1,tag2');    // The new video tags. The tags are separated with commas (,).
        $request->setCateId(0);       // The new video category. (You can log on to the ApsaraVideo for VOD console and choose Global Settings > Categories from the left-side navigation pane to view the category ID.)
        $request->setAcceptFormat('JSON');
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $videoInfo = updateVideoInfo($client, 'Your videoId');
        var_dump($videoInfo);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify the information about videos {#h2--div-id-updatevideoinfos-div-6}
------------------------------------------------------------------------

You can call the UpdateVideoInfos operation to modify the information about videos.
For more information about the request and response parameters of this operation, see [UpdateVideoInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfos.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Modify the information about videos.
     * @param client The client that is used to send requests.
     * @return UpdateVideoInfosResponse The fields that must be contained in the response.
    */
    function updateVideoInfos($client) {
        $request = new vod\UpdateVideoInfosRequest();
    
        $updateContentArray = array();
        $updateContent1 = array();
        $updateContent1["VideoId"] = "e67e761ec04342cd9ca5149c7485****";
        $updateContent1["Title"] = "new Title1";
        $updateContentArray[] = $updateContent1;
    
        $updateContent2 = array();
        $updateContent2["VideoId"] = "b19439abb9a94374b7f4d45f6985****";
        $updateContent2["Title"] = "new Title2";
        $updateContentArray[] = $updateContent2;
    
        $request->setUpdateContent(json_encode($updateContentArray));
    
        return $client->getAcsResponse($request);
    }
    
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = updateVideoInfos($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete videos {#h2--div-id-deletevideo-div-7}
---------------------------------------------

You can call the DeleteVideo operation to delete videos.
For more information about the request and response parameters of this operation, see [DeleteVideo](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteVideo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Delete videos
     * @param client The client that is used to send requests.
     * @return DeleteVideoResponse The fields that must be contained in the response.
     */
    function deleteVideos($client, $videoIds) {
        $request = new vod\DeleteVideoRequest();
        $request->setVideoIds($videoIds);   // The IDs of the videos to be deleted. These IDs are the value of the videoIds parameter. Multiple IDs are separated with a comma (,).
        $request->setAcceptFormat('JSON');
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $delInfo = deleteVideos($client, 'vid1,vid2');
        var_dump($delInfo);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query source file information (including the file URL) {#h2--div-id-getmezzanineinfo-div-8}
-------------------------------------------------------------------------------------------

You can call the GetMezzanineInfo operation to query source file information.
For more information about the request and response parameters of this operation, see [GetMezzanineInfo](/intl.en-US/API Reference/Media asset management/Audio and video management/GetMezzanineInfo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query source file information.
     * @param client The client that is used to send requests.
     * @return GetMezzanineInfoResponse The fields that must be contained in the response.
     */
    function getMezzanineInfo($client, $videoId) {
        $request = new vod\GetMezzanineInfoRequest();
        $request->setVideoId($videoId);
        $request->setAuthTimeout(3600*5);   // The expiration time of the file URL, in seconds. The default value is 3600 seconds.
        $request->setAcceptFormat('JSON');
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $mezzanine = getMezzanineInfo($client, 'Your videoId');
        var_dump($mezzanine);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query videos by using filter conditions {#h2--div-id-getvideolist-div-9}
------------------------------------------------------------------------

You can call the GetVideoList operation to query videos by using filter conditions.
For more information about the request and response parameters of this operation, see [GetVideoList](/intl.en-US/API Reference/Media asset management/Audio and video management/GetVideoList.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query videos by using filter conditions.
     * @param client The client that is used to send requests.
     * @return GetVideoListResponse The fields that must be contained in the response.
     */
    function getVideoList($client) {
        $request = new vod\GetVideoListRequest();
    
        // Example: Set the start time to one month ago (in UTC) and the end time to the current time (in UTC) to filter videos that are created in this period.
        $localTimeZone = date_default_timezone_get();
        date_default_timezone_set('UTC');
        $utcNow = gmdate('Y-m-d\TH:i:s\Z');
        $utcMonthAgo = gmdate('Y-m-d\TH:i:s\Z', time() - 30*86400);
        date_default_timezone_set($localTimeZone);
        $request->setStartTime($utcMonthAgo);   // The start time for video creation, in UTC.
        $request->setEndTime($utcNow);          // The end time for video creation, in UTC.
    
        #$request->setStatus('Uploading,Normal,Transcoding');  // The video Statuses. By default, videos in all statuses are obtained. Separate video statuses with commas (,).
        #$request->setCateId(0);               // The video category.
        $request->setPageNo(1);
        $request->setPageSize(20);
        $request->setAcceptFormat('JSON');
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $videoList = getVideoList($client);
        var_dump($videoList);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete a media stream {#h2--div-id-deletestream-div-10}
-------------------------------------------------------

You can call the DeleteStream operation to delete a media stream.
For more information about the request and response parameters of this operation, see [DeleteStream](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteStream.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Delete a media stream.
     * @param client The client that is used to send requests.
     * @return DeleteMezzaninesResponse The fields that must be contained in the response.
     */
    function deleteStream($client, $videoId, $jobIds) {
        $request = new vod\DeleteStreamRequest();
        $request->setVideoId($videoId);
        $request->setJobIds($jobIds);   // The IDs of media stream transcoding jobs. Separate job IDs with commas (,). You can obtain the job IDs by calling the GetPlayInfo operation.
        $request->setAcceptFormat('JSON');
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $delStream = deleteStream($client, 'videoId', 'jobId1,jobId2');
        var_dump($delStream);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete source files {#h2--div-id-deletemezzanines-div-11}
---------------------------------------------------------

You can call the DeleteMezzanines operation to delete source files.
For more information about the request and response parameters of this operation, see [DeleteMezzanines](/intl.en-US/API Reference/Media asset management/Audio and video management/DeleteMezzanines.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Delete source files.
     * @param client The client that is used to send requests.
     * @return DeleteMezzaninesResponse The fields that must be contained in the response.
    */
    function deleteMezzanines($client) {
        $request = new vod\DeleteMezzaninesRequest();
        $request->setVideoIds("b19439abb9a94374b7f4d45f6656****");
        $request->setForce(false);
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = deleteMezzanines($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Modify the information about images {#h2--div-id-updateimageinfos-div-12}
-------------------------------------------------------------------------

You can call the UpdateImageInfos operation to modify the information about images.
For more information about the request and response parameters of this operation, see [UpdateImageInfos](/intl.en-US/API Reference/Media asset management/Audio and video management/UpdateVideoInfos.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Modify the information about images.
     * @param client The client that is used to send requests.
     * @return UpdateImageInfosResponse The fields that must be contained in the response.
     */
    function updateImageInfos($client) {
        $request = new vod\UpdateImageInfosRequest();
    
        $updateContentArray = array();
        $updateContent1 = array();
        $updateContent1["ImageId"] = "7e66f99e1cb3419982275398159****";
        $updateContent1["Title"] = "new Title1";
        $updateContentArray[] = $updateContent1;
    
        $updateContent2 = array();
        $updateContent2["ImageId"] = "d2171a5656454c49a4f11a544c59****";
        $updateContent2["Title"] = "new Title2";
        $updateContentArray[] = $updateContent2;
    
        $request->setUpdateContent(json_encode($updateContentArray));
    
        return $client->getAcsResponse($request);
    }
    
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = updateImageInfos($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Query an image {#h2--div-id-getimageinfo-div-13}
------------------------------------------------

You can call the GetImageInfo operation to query details about an image.
For more information about the request and response parameters of this operation, see [GetImageInfo](/intl.en-US/API Reference/Media asset management/Image management/GetImageInfo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Query an image.
     * @param client The client that is used to send requests.
     * @return GetImageInfoResponse The fields that must be contained in the response.
     */
    function getImageInfo($client) {
        $request = new vod\GetImageInfoRequest();
        $request->setImageId("7e66f99e1cb341998227539812b4****");
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = getImageInfo($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }



Delete images {#h2--div-id-deleteimage-div-14}
----------------------------------------------

You can call the DeleteImage operation to delete images.
For more information about the request and response parameters of this operation, see [DeleteImage](/intl.en-US/API Reference/Media asset management/Image management/DeleteImage.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    /**
     * Delete images.
     * @param client The client that is used to send requests.
     * @return DeleteImageResponse The fields that must be contained in the response.
     */
    function deleteImage($client) {
        $request = new vod\DeleteImageRequest();
        // Delete an image file by ImageURL.
        $request->setDeleteImageType("ImageURL");
        $request->setImageURLs("http://192.168.0.0/16/cover.jpg");
    
        // Delete an image files by ImageId.
        //$request->setDeleteImageType("ImageId");
        //$request->setImageIds("ImageId1,ImageId2");
    
        // Delete image files of the specified image type based on a video ID.
        //$request->setDeleteImageType("VideoId");
        //$request->setVideoId("VideoId");
    
        return $client->getAcsResponse($request);
    }
    
    try {
        $client = initVodClient('<AccessKeyId>', '<AccessKeySecret>');
    
        $result = deleteImage($client);
        var_dump($result);
    } catch (Exception $e) {
        print $e->getMessage()."\n";
    }


