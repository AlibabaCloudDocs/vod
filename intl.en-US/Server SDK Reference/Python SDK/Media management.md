Media management 
=====================================

This topic provides examples on how to use the API operations of the media management module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to search for media asset information, modify video information, and query source file information. You can also query and delete videos and images.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Search for media asset information {#h2--div-id-searchmedia-div-2}
------------------------------------------------------------------

You can call the SearchMedia operation to search for media asset information.

For more information about the request and response parameters of this operation, see [SearchMedia](/intl.en-US/API Reference/Media management/Media Search/SearchMedia.md). Example:

    from aliyunsdkvod.request.v20170321 import SearchMediaRequest
    def search_media(clt):
        request = SearchMediaRequest.SearchMediaRequest()
        request.set_Fields('Title,CoverURL,Status');
        request.set_Match('Status in ("Normal","Checking") and CreationTime = ("2018-10-01T08:00:00Z","2018-12-25T08:00:00Z")')
        request.set_PageNo(1)
        request.set_PageSize(10)
        request.set_SearchType('video')
        request.set_SortBy('CreationTime:Desc')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        medias = search_media(clt)
        print(medias['MediaList'])
        print(json.dumps(medias, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query a video {#h2--div-id-getvideoinfo-div-3}
----------------------------------------------

You can call the GetVideoInfo operation to query details about a video.
For more information about the request and response parameters of this operation, see [GetVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetVideoInfoRequest
    def get_video_info(clt, videoId):
        request = GetVideoInfoRequest.GetVideoInfoRequest()
        request.set_accept_format('JSON')
        request.set_VideoId(videoId)
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        videoInfo = get_video_info(clt, '<videoId>')
        print(json.dumps(videoInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query videos {#h2--div-id-getvideoinfos-div-4}
----------------------------------------------

You can call the GetVideoInfos operation to query videos.
For more information about the request and response parameters of this operation, see [GetVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfos.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetVideoInfosRequest
    def get_video_infos(clt):
        request = GetVideoInfosRequest.GetVideoInfosRequest()
        videoIds = ['videoId1', 'videoId2']
        request.set_VideoIds(','.join(videoIds))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        videos = get_video_infos(clt)
        #print(videos['VideoList'])
        print(videos['NonExistVideoIds'])
        print(json.dumps(videos, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Modify the information about a video {#h2--div-id-updatevideoinfo-div-5}
------------------------------------------------------------------------

You can call the UpdateVideoInfo operation to modify the information about a video.
For more information about the request and response parameters of this operation, see [UpdateVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfo.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateVideoInfoRequest
    def update_video_info(clt, videoId):
        request = UpdateVideoInfoRequest.UpdateVideoInfoRequest()
        request.set_VideoId(videoId)
        request.set_Title('New Title') 
        request.set_Description('New Description')
        request.set_CoverURL('http192.168.0.0/16/tps/TB1qnJ1PVXXXXXCXXXXXXXXXXXX-700-700.png')  
        request.set_Tags('tag1,tag2') 
        #request.set_CateId(0) 
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        updateInfo = update_video_info(clt, '<videoId>')
        print(json.dumps(updateInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Modify the information about videos {#h2--div-id-updatevideoinfos-div-6}
------------------------------------------------------------------------

You can call the UpdateVideoInfos operation to modify the information about videos.
For more information about the request and response parameters of this operation, see [UpdateVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfos.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateVideoInfosRequest
    def update_video_infos(clt):
        request = UpdateVideoInfosRequest.UpdateVideoInfosRequest()
    
        updateContent = []
        updateItem1 = {'VideoId': '<VideoId1>', 'Title': 'New Sample Title1', 'Tags': 'NewTag1,NewTag2'}
        updateItem2 = {'VideoId': '<VideoId2>', 'Title': 'New Sample Title2', 'Tags': 'NewTag3,NewTag4'}
        updateContent.append(updateItem1)
        updateContent.append(updateItem2)
        request.set_UpdateContent(json.dumps(updateContent))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        update = update_video_infos(clt)
        print(update['NonExistVideoIds'])
        print(json.dumps(update, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete videos {#h2--div-id-deletevideo-div-7}
---------------------------------------------

You can call the DeleteVideo operation to delete videos.
For more information about the request and response parameters of this operation, see [DeleteVideo](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteVideo.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DeleteVideoRequest
    def delete_videos(clt):
        request = DeleteVideoRequest.DeleteVideoRequest()
        videoIds = ['videoId1', 'videoId2']
        request.set_VideoIds(','.join(videoIds)) # You can delete multiple videos. Separate multiple videos with commas (,).
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        delInfo = delete_videos(clt)
        print(json.dumps(delInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query source file information (including the file URL) {#h2--div-id-getmezzanineinfo-div-8}
-------------------------------------------------------------------------------------------

You can call the GetMezzanineInfo operation to query source file information.
For more information about the request and response parameters of this operation, see [GetMezzanineInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetMezzanineInfo.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetMezzanineInfoRequest
    def get_mezzanine_info(clt, videoId):
        request = GetMezzanineInfoRequest.GetMezzanineInfoRequest()
        request.set_VideoId(videoId)
        request.set_AuthTimeout(3600*5)
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        mezzanine = get_mezzanine_info(clt, '<videoId>')
        print(json.dumps(mezzanine, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query videos by using filter conditions {#h2--div-id-getvideolist-div-9}
------------------------------------------------------------------------

You can call the GetVideoList operation to query videos by using filter conditions.
For more information about the request and response parameters of this operation, see [GetVideoList](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoList.md). Example:
**Notice**
The time must be in UTC. For example, 2018-01-01T12:00:00Z indicates 20:00:00 on January 1, 2018 (UTC+8). {#h2--div-id-getvideolist-div-9}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetVideoListRequest
    def get_video_list(clt):
        request = GetVideoListRequest.GetVideoListRequest()
        # Take querying the video list in the last 30 days as an example.
        utcNow = datetime.datetime.utcnow().strftime("%Y-%m-%dT%H:%M:%SZ")
        utcMonthAgo = datetime.datetime.utcfromtimestamp(time.time() - 30*86400).strftime("%Y-%m-%dT%H:%M:%SZ")
        request.set_StartTime(utcMonthAgo) # The start time for video creation, in UTC.
        request.set_EndTime(utcNow) # The end time for video creation, in UTC.
        # request.set_Status('Uploading,Normal,Transcoding')  # The Video Status. Videos in all statuses are queried by default Separate multiple videos with commas (,).
        #request.set_CateId (0) # Filter by category.
        request.set_PageNo(1)
        request.set_PageSize(20)
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        videoList = get_video_list(clt)
        print(json.dumps(videoList, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete a media stream {#h2--div-id-deletestream-div-10}
-------------------------------------------------------

You can call the DeleteStream operation to delete a media stream.
For more information about the request and response parameters of this operation, see [DeleteStream](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteStream.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DeleteStreamRequest
    # Delete video or audio streams and their storage files. Multiple streams can be deleted at a time. The deleted streams cannot be played if the CDN cache expires. Delete streams with caution.
    def delete_stream(clt):
        request = DeleteStreamRequest.DeleteStreamRequest()
        request.set_VideoId('<videoId>')
        # Specify the IDs of media stream transcoding jobs. Separate multiple job IDs with commas (,). You can query the JobId by using the GetPlayInfo operation.
        jobIds = ['jobId1', 'jobId2']
        request.set_JobIds(','.join(jobIds))
        request.set_accept_format('JSON')
    
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        delStream = delete_stream(clt)
        print(json.dumps(delStream, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete source files {#h2--div-id-deletemezzanines-div-11}
---------------------------------------------------------

You can call the DeleteMezzanines operation to delete source files.
For more information about the request and response parameters of this operation, see [DeleteMezzanines](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteMezzanines.md). Example: 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DeleteMezzaninesRequest
    def delete_mezzanines(clt):
        request = DeleteMezzaninesRequest.DeleteMezzaninesRequest()
    
        videoIds = ['videoId1', 'videoId2']
        request.set_VideoIds(','.join(videoIds))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        delInfo = delete_mezzanines(clt)
        print(delInfo['NonExistVideoIds'])
        print(json.dumps(delInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Modify the information about images {#h2--div-id-updateimageinfos-div-12}
-------------------------------------------------------------------------

You can call the UpdateImageInfos operation to modify the information about images.
For more information about the request and response parameters of this operation, see [UpdateImageInfos](/intl.en-US/API Reference/Media management/Image Management/UpdateImageInfos.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UpdateImageInfosRequest
    def update_image_infos(clt):
        request = UpdateImageInfosRequest.UpdateImageInfosRequest()
    
        updateContent = []
        updateItem1 = {'ImageId': '<imageId1>', 'Title': 'New Sample Title1', 'Tags': 'NewTag1,NewTag2'}
        updateItem2 = {'ImageId': '<imageId2>', 'Title': 'New Sample Title2', 'Tags': 'NewTag3,NewTag4'}
        updateContent.append(updateItem1)
        updateContent.append(updateItem2)
        request.set_UpdateContent(json.dumps(updateContent))
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        update = update_image_infos(clt)
        print(update['NonExistImageIds']['ImageId'])
        print(json.dumps(update, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query an image {#h2--div-id-getimageinfo-div-13}
------------------------------------------------

You can call the GetImageInfo operation to query an image.
For more information about the request and response parameters of this operation, see [GetImageInfo](/intl.en-US/API Reference/Media management/Image Management/GetImageInfo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetImageInfoRequest
    def get_image_info(clt):
        request = GetImageInfoRequest.GetImageInfoRequest()
        request.set_ImageId('<imageId>')
        request.set_AuthTimeout(3600*24)
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        image = get_image_info(clt)
        print(image['ImageInfo'])
        print(json.dumps(image, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Delete images {#h2--div-id-deleteimage-div-14}
----------------------------------------------

You can call the DeleteImage operation to delete images.
For more information about the request and response parameters of this operation, see [DeleteImage](/intl.en-US/API Reference/Media management/Image Management/DeleteImage.md). Example: 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import DeleteImageRequest
    def delete_image(clt):
        request = DeleteImageRequest.DeleteImageRequest()
    
        # Delete image files based on ImageURL.
        request.set_DeleteImageType('ImageURL')
        request.set_ImageURLs('http://192.168.0.0/16/cover.jpg')
    
        # Delete image files based on ImageId.
        #request.set_DeleteImageType('ImageId')
        #request.set_ImageIds('ImageId1,ImageId2')
    
        # Delete image files based on VideoId and ImageType.
        #request.set_DeleteImageType('VideoId')
        #request.set_VideoId('VideoId')
        #request.set_ImageType('SpriteSnapshot')
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        delInfo = delete_image(clt)
        print(json.dumps(delInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


