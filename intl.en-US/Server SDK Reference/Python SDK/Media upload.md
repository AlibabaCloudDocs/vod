Media upload 
=================================

This topic provides examples on how to use the API operations of the media upload module. The API operations are encapsulated in ApsaraVideo VOD SDK for Python. You can call the API operations to create upload URLs and credentials, and register media assets. You can also upload media files by using a source file URL. To upload complete media files, you can use the client to upload the files or use the server-side upload SDK for Python to upload the files.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/Python SDK/Initialization.md).

Create a URL and a credential for uploading videos {#h2--div-id-createuploadvideo-div-2}
----------------------------------------------------------------------------------------

You can call the CreateUploadVideo operation to create a URL and a credential for uploading videos.
For more information about the request and response parameters of this operation, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import CreateUploadVideoRequest
    def create_upload_video(clt):
        request = CreateUploadVideoRequest.CreateUploadVideoRequest()
        request.set_Title('Video Title')
        request.set_FileName('/opt/video/sample/video_file.mp4')
        request.set_Description('Video Description')
     request.set_CoverURL('http://192.168.0.0/16/tps/TB1qnJ1PVXXXXXCXXXXXXXXXXXX-700-700.png')
        request.set_Tags('tag1,tag2')
        request.set_CateId(0)
    
        request.set_accept_format('JSON')
        response = json.loads(clt.do_action_with_exception(request))
        return response
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        uploadInfo = create_upload_video(clt)
        print(uploadInfo['UploadAuth'])
        print(json.dumps(uploadInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Refresh the credential for uploading videos {#h2--div-id-refreshuploadvideo-div-3}
----------------------------------------------------------------------------------

You can call the RefreshUploadVideo operation to refresh the credential for uploading videos.

For more information about the request and response parameters of this operation, see [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md). Example:

    from aliyunsdkvod.request.v20170321 import RefreshUploadVideoRequest
    def refresh_upload_video(clt, videoId):
        request = RefreshUploadVideoRequest.RefreshUploadVideoRequest()
        request.set_VideoId(videoId)
        request.set_accept_format('JSON')
        return json.loads(clt.do_action_with_exception(request))
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        uploadInfo = refresh_upload_video(clt, 'VideoId')
        print(json.dumps(uploadInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Create a URL and a credential for uploading images {#h2--div-id-createuploadimage-div-4}
----------------------------------------------------------------------------------------

You can call the CreateUploadImage operation to create a URL and a credential for uploading images.
For more information about the request and response parameters of this operation, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import CreateUploadImageRequest
    def create_upload_image(clt, imageType, imageExt):
        request = CreateUploadImageRequest.CreateUploadImageRequest()
        request.set_ImageType(imageType)
        request.set_ImageExt(imageExt)
        request.set_accept_format('JSON')
        return json.loads(clt.do_action_with_exception(request))
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        imageInfo = create_upload_image(clt, 'cover', 'jpg')
        print(json.dumps(imageInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Create a URL and a credential for uploading attached media assets {#h2--div-id-createuploadattachedmedia-div-5}
---------------------------------------------------------------------------------------------------------------

You can call the CreateUploadAttachedMedia operation to create a URL and a credential for uploading attached media assets.
For more information about the request and response parameters of this operation, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md). Example: 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import CreateUploadAttachedMediaRequest
    def create_upload_attached_media(clt):
        request = CreateUploadAttachedMediaRequest.CreateUploadAttachedMediaRequest()
        request.set_BusinessType("watermark");
        request.set_MediaExt("gif");
        request.set_Title("this is a sample");
        request.set_accept_format('JSON')
        return json.loads(clt.do_action_with_exception(request))
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        uploadInfo = create_upload_attached_media(clt)
        print(uploadInfo['UploadAuth'])
        print(json.dumps(uploadInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Upload media files by using a source file URL {#h2-url-div-id-uploadmediabyurl-div-6}
-------------------------------------------------------------------------------------

You can call the UploadMediaByURL operation to upload media files by using a source file URL.
For more information about the request and response parameters of this operation, see [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md). Example: 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import UploadMediaByURLRequest
    import sys,urllib
    def upload_media_by_url(clt):
        request = UploadMediaByURLRequest.UploadMediaByURLRequest()
    
        urls = ["http://xxx.cn-shanghai.aliyuncs.com/sample1.mp4",
                "http://xxx.cn-shanghai.aliyuncs.com/sample2.flv"]
        # Encode the urls and add metadata
        uploadUrls = []
        uploadMetadatas = []
        for url in urls:
            if sys.version_info[0] == 3:
                encodeUrl = urllib.parse.quote(url)
            else:
                encodeUrl = urllib.quote(url)
            uploadUrls.append(encodeUrl)
            uploadMetadatas.append({'SourceURL': encodeUrl, 'Title': 'Sample Title'})
    
        request.set_UploadURLs(','.join(uploadUrls))
        request.set_UploadMetadatas(json.dumps(uploadMetadatas))
    
        request.set_accept_format('JSON')
        return json.loads(clt.do_action_with_exception(request))
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        uploadInfo = upload_media_by_url(clt)
        print(uploadInfo['UploadJobs'])
        print(json.dumps(uploadInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Register media assets {#h2--div-id-registermedia-div-7}
-------------------------------------------------------

You can call the RegisterMedia operation to register media assets.
For more information about the request and response parameters of this operation, see [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md). Example: 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import RegisterMediaRequest
    def register_media(clt):
        request = RegisterMediaRequest.RegisterMediaRequest()
        metadatas = []
        metadatas.append({'FileURL':"https://192.168.0.0/16/vod_sample.mp4", "Title":"RegisterMedia sample Title"})
        request.set_RegisterMetadatas(json.dumps(metadatas))
        request.set_accept_format('JSON')
        return json.loads(clt.do_action_with_exception(request))
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        registerInfo = register_media(clt)
        print(registerInfo['RegisteredMediaList'])
        print(registerInfo['FailedFileURLs'])
        print(json.dumps(registerInfo, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())



Query the information about uploading data to URLs {#h2--url-div-id-geturluploadinfos-div-8}
--------------------------------------------------------------------------------------------

You can call the GetURLUploadInfos operation to query the information about uploading data to URLs.
For more information about the request and response parameters of this operation, see [GetURLUploadInfos](/intl.en-US/API Reference/Media upload/GetURLUploadInfos.md). Example: 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    from aliyunsdkvod.request.v20170321 import GetURLUploadInfosRequest
    import sys,urllib
    def get_url_upload_infos(clt):
        request = GetURLUploadInfosRequest.GetURLUploadInfosRequest()
        urls = ["http://192.168.0.0/16/sample1.mp4",
                "http://192.168.0.0/16/sample2.flv"]
    
        # Encode URLs.
        uploadUrls = []
        for url in urls:
            if sys.version_info[0] == 3:
                encodeUrl = urllib.parse.quote(url)
            else:
                encodeUrl = urllib.quote(url)
            uploadUrls.append(encodeUrl)
    
        # The URLs that you want to use to upload media files. Separate multiple URLs with commas (,).
        request.set_UploadURLs(','.join(uploadUrls))
    
        # The job IDs that you use to query URLs.
        #request.set_JobIds("jobId1,jobId2")
    
        request.set_accept_format('JSON')
        return json.loads(clt.do_action_with_exception(request))
    
    try:
        clt = init_vod_client('<AccessKeyId>', '<AccessKeySecret>')
        res = get_url_upload_infos(clt)
        print(res['NonExists'])
        print(json.dumps(res, ensure_ascii=False, indent=4))
    
    except Exception as e:
        print(e)
        print(traceback.format_exc())


