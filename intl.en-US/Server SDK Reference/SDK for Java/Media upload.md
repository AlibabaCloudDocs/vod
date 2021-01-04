Media upload 
=================================

This topic provides examples on how to use the API operations of the media upload module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to create upload URLs and credentials and register media assets. To upload complete media files, you can use the client or the upload SDK for Java.

Initialize a client {#h2-u521Du59CBu5316u5BA2u6237u7AEF1}
---------------------------------------------------------

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

Create a URL and a credential for uploading videos {#h2--div-id-createuploadvideo-div-2}
----------------------------------------------------------------------------------------

You can call the CreateUploadVideo operation to create a URL and a credential for uploading videos.

For more information about the request and response parameters of this operation, see [CreateUploadVideo](/intl.en-US/API Reference/Media upload/CreateUploadVideo.md). Example:

    import com.aliyuncs.vod.model.v20170321.CreateUploadVideoRequest;
    import com.aliyuncs.vod.model.v20170321.CreateUploadVideoResponse;
    
    /**
     * Create a URL and a credential for uploading videos.
     * @param client The client that is used to send requests.
     * @return CreateUploadVideoResponse The fields that must be contained in the response.
     * @throws Exception
    */
    public static CreateUploadVideoResponse createUploadVideo(DefaultAcsClient client) throws Exception {
        CreateUploadVideoRequest request = new CreateUploadVideoRequest();
        request.setTitle("this is a sample");
        request.setFileName("filename.mp4");
    
        // Optional. The user data that consists of user-defined parameters. If you need a callback URL and transparent data transmission, you can configure the user data.
        //JSONObject userData = new JSONObject();
    
        // The configuration of the callback in the user data.
        //JSONObject messageCallback = new JSONObject();
        //messageCallback.put("CallbackURL", "http://192.168.0.0/16");
        //messageCallback.put("CallbackType", "http");
        //userData.put("MessageCallback", messageCallback.toJSONString());
    
        // The configuration of transparent data transmission in the user data.
        //JSONObject extend = new JSONObject();
        //extend.put("MyId", "user-defined-id");
        //userData.put("Extend", extend.toJSONString());
    
        //request.setUserData(userData.toJSONString());
    
        return client.getAcsResponse(request);
    }
    
    // Call example
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        CreateUploadVideoResponse response = new CreateUploadVideoResponse();
        try {
            response = createUploadVideo(client);
            System.out.print("VideoId = " + response.getVideoId() + "\n");
            System.out.print("UploadAddress = " + response.getUploadAddress() + "\n");
            System.out.print("UploadAuth = " + response.getUploadAuth() + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Refresh the credential for uploading videos {#h2--div-id-refreshuploadvideo-div-3}
----------------------------------------------------------------------------------

You can call the RefreshUploadVideo operation to refresh the credential for uploading videos.

For more information about the request and response parameters of this operation, see [RefreshUploadVideo](/intl.en-US/API Reference/Media upload/RefreshUploadVideo.md). Example:

    import com.aliyuncs.vod.model.v20170321.RefreshUploadVideoRequest;
    import com.aliyuncs.vod.model.v20170321.RefreshUploadVideoResponse;
    
    /**
     * Refresh the credential for uploading videos.
     * @param client The client that is used to send requests.
     * @return RefreshUploadVideoResponse The fields that must be contained in the response.
     * @throws Exception
    */
    public static RefreshUploadVideoResponse refreshUploadVideo(DefaultAcsClient client) throws Exception {
        RefreshUploadVideoRequest request = new RefreshUploadVideoRequest();
        request.setVideoId("VideoId");
        return client.getAcsResponse(request);
    }
    
    // Call example
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        RefreshUploadVideoResponse response = new RefreshUploadVideoResponse();
        try {
            response = refreshUploadVideo(client);
            System.out.print("UploadAddress = " + response.getUploadAddress() + "\n");
            System.out.print("UploadAuth = " + response.getUploadAuth() + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Create a URL and a credential for uploading images {#h2--div-id-createuploadimage-div-4}
----------------------------------------------------------------------------------------

You can call the CreateUploadImage operation to create a URL and a credential for uploading images.

For more information about the request and response parameters of this operation, see [CreateUploadImage](/intl.en-US/API Reference/Media upload/CreateUploadImage.md). Example:

    import com.aliyuncs.vod.model.v20170321.CreateUploadImageRequest;
    import com.aliyuncs.vod.model.v20170321.CreateUploadImageResponse;
    
    /**
     * Create a URL and a credential for uploading images.
     * @param client The client that is used to send requests.
     * @return CreateUploadImageResponse The fields that must be contained in the response.
     * @throws Exception
    */
    public static CreateUploadImageResponse createUploadImage(DefaultAcsClient client) throws Exception {
        CreateUploadImageRequest request = new CreateUploadImageRequest();
        request.setImageType("default");
        request.setImageExt("gif");
        request.setTitle("this is a sample");
    
        JSONObject userData = new JSONObject();
    
        JSONObject messageCallback = new JSONObject();
        messageCallback.put("CallbackURL", "http://192.168.0.0/16");
        messageCallback.put("CallbackType", "http");
        userData.put("MessageCallback", messageCallback.toJSONString());
    
        JSONObject extend = new JSONObject();
        extend.put("MyId", "user-defined-id");
        userData.put("Extend", extend.toJSONString());
    
        request.setUserData(userData.toJSONString());
    
        return client.getAcsResponse(request);
    }
    
    // Call example
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        CreateUploadImageResponse response = new CreateUploadImageResponse();
        try {
            response = createUploadImage(client);
            System.out.print("ImageId = " + response.getImageId() + "\n");
            System.out.print("ImageURL = " + response.getImageURL() + "\n");
            System.out.print("UploadAddress = " + response.getUploadAddress() + "\n");
            System.out.print("UploadAuth = " + response.getUploadAuth() + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Create a URL and a credential for uploading attached media assets {#h2--div-id-createuploadattachedmedia-div-5}
---------------------------------------------------------------------------------------------------------------

You can call the CreateUploadAttachedMedia operation to create a URL and a credential for uploading attached media assets.

For more information about the request and response parameters of this operation, see [CreateUploadAttachedMedia](/intl.en-US/API Reference/Media upload/CreateUploadAttachedMedia.md). Example:

    import com.aliyuncs.vod.model.v20170321.CreateUploadAttachedMediaRequest;
    import com.aliyuncs.vod.model.v20170321.CreateUploadAttachedMediaResponse;
    /**
     * Create a URL and a credential for uploading attached media assets, such as watermarks and subtitle files.
     * @param client The client that is used to send requests.
     * @return CreateUploadAttachedMediaResponse The fields that must be contained in the response.
     * @throws Exception
     */
    public static CreateUploadAttachedMediaResponse createUploadAttachedMedia(DefaultAcsClient client) throws Exception {
        CreateUploadAttachedMediaRequest request = new CreateUploadAttachedMediaRequest();
        request.setBusinessType("watermark");
        request.setMediaExt("gif");
        request.setTitle("this is a sample");
    
        JSONObject userData = new JSONObject();
    
        JSONObject messageCallback = new JSONObject();
        messageCallback.put("CallbackURL", "http://192.168.0.0/16");
        messageCallback.put("CallbackType", "http");
        userData.put("MessageCallback", messageCallback.toJSONString());
    
        JSONObject extend = new JSONObject();
        extend.put("MyId", "user-defined-id");
        userData.put("Extend", extend.toJSONString());
    
        request.setUserData(userData.toJSONString());
    
        return client.getAcsResponse(request);
    }
    // Call example
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        CreateUploadAttachedMediaResponse response = new CreateUploadAttachedMediaResponse();
        try {
            response = createUploadAttachedMedia(client);
            System.out.print("mediaId = " + response.getMediaId() + "\n");
            System.out.print("mediaURL = " + response.getMediaURL() + "\n");
            System.out.print("UploadAddress = " + response.getUploadAddress() + "\n");
            System.out.print("UploadAuth = " + response.getUploadAuth() + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Upload media files by using a source file URL {#h2-url-div-id-uploadmediabyurl-div-6}
-------------------------------------------------------------------------------------

You can call the UploadMediaByURL operation to upload media files by using a source file URL.

For more information about the request and response parameters of this operation, see [UploadMediaByURL](/intl.en-US/API Reference/Media upload/UploadMediaByURL.md). Example:

    import com.alibaba.fastjson.JSON;
    import com.alibaba.fastjson.JSONArray;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.vod.model.v20170321.UploadMediaByURLRequest;
    import com.aliyuncs.vod.model.v20170321.UploadMediaByURLResponse;
    
    /**
     * Upload media files by using a source file URL.
     * @param client The client that is used to send requests.
     * @return UploadMediaByURLResponse The fields that must be contained in the response.
     * @throws Exception
    */
    public static UploadMediaByURLResponse uploadMediaByURL(DefaultAcsClient client) throws Exception {
        UploadMediaByURLRequest request = new UploadMediaByURLRequest();
        String url = "http://xxxx.mp4";
        String encodeUrl = URLEncoder.encode(url, "UTF-8");
        request.setUploadURLs(encodeUrl);
    
        JSONObject uploadMetadata = new JSONObject();
        uploadMetadata.put("SourceUrl", encodeUrl);
        uploadMetadata.put("Title", "upload by url sample");
    
        JSONArray uploadMetadataList = new JSONArray();
        uploadMetadataList.add(uploadMetadata);
        request.setUploadMetadatas(uploadMetadataList.toJSONString());
    
        JSONObject userData = new JSONObject();
    
        JSONObject messageCallback = new JSONObject();
        messageCallback.put("CallbackURL", "http://192.168.0.0/16");
        messageCallback.put("CallbackType", "http");
        userData.put("MessageCallback", messageCallback.toJSONString());
    
        JSONObject extend = new JSONObject();
        extend.put("MyId", "user-defined-id");
        userData.put("Extend", extend.toJSONString());
    
        request.setUserData(userData.toJSONString());
    
        return client.getAcsResponse(request);
    }
    // Call example
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        UploadMediaByURLResponse response = new UploadMediaByURLResponse();
        try {
            response = uploadMediaByURL(client);
            System.out.print("UploadJobs = " + JSON.toJSONString(response.getUploadJobs()) + "\n");
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Register media assets {#h2--div-id-registermedia-div-7}
-------------------------------------------------------

You can call the RegisterMedia operation to register media assets.

For more information about the request and response parameters of this operation, see [RegisterMedia](/intl.en-US/API Reference/Media upload/RegisterMedia.md). Example:

    import com.aliyuncs.vod.model.v20170321.RegisterMediaRequest;
    import com.aliyuncs.vod.model.v20170321.RegisterMediaResponse;
    import com.alibaba.fastjson.JSONArray;
    import com.alibaba.fastjson.JSONObject;
    
    /**
     * Register media assets.
     * @param client The client that is used to send requests.
     * @return RegisterMediaResponse The fields that must be contained in the response.
     * @throws Exception
    */
    public static RegisterMediaResponse registerMedia(DefaultAcsClient client) throws Exception {
        RegisterMediaRequest request = new RegisterMediaRequest();
        JSONArray metaDataArray = new JSONArray();
        JSONObject metaData = new JSONObject();
        metaData.put("Title", "this is a sample");
        metaData.put("FileURL", "https://192.168.0.0/16.oss-cn-shanghai.aliyuncs.com/vod_sample.mp4");
        metaDataArray.add((metaData));
        request.setRegisterMetadatas(metaDataArray.toJSONString());
        return client.getAcsResponse(request);
    }
    
    // Call example
    public static void main(String[] argv) throws Exception {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        RegisterMediaResponse response = new RegisterMediaResponse();
        try {
            response = registerMedia(client);
            if (response.getFailedFileURLs() ! = null && response.getFailedFileURLs().size() > 0) {
                for (String fileURL : response.getFailedFileURLs()) {
                    System.out.print("FailedFileURL = " + fileURL + "\n");
                }
            }
            if (response.getRegisteredMediaList() ! = null && response.getRegisteredMediaList().size() > 0) {
            for (RegisterMediaResponse.RegisteredMedia registeredMedia : response.getRegisteredMediaList()) {
                System.out.print("MediaId = " + registeredMedia.getMediaId());
                System.out.print("FileURL = " + registeredMedia.getFileURL());
                System.out.print("NewRegister = " + registeredMedia.getNewRegister());
                }
            }
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }



Query the information about uploading data to URLs {#h2--url-div-id-geturluploadinfos-div-8}
--------------------------------------------------------------------------------------------

You can call the GetURLUploadInfos operation to query the information about uploading data to URLs.

For more information about the request and response parameters of this operation, see [GetURLUploadInfos](/intl.en-US/API Reference/Media upload/GetURLUploadInfos.md). Example:

    import java.net.URLEncoder;
    import java.util.Arrays;
    import org.apache.commons.lang.StringUtils;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.profile.DefaultProfile;
    import com.aliyuncs.vod.model.v20170321.GetURLUploadInfosRequest;
    import com.aliyuncs.vod.model.v20170321.GetURLUploadInfosResponse;
    
    /**
     * Query the information about uploading data to URLs.
     * @param client The client that is used to send requests.
     * @return GetURLUploadInfosResponse The fields that must be contained in the response.
     * @throws Exception
     */
    public static GetURLUploadInfosResponse getURLUploadInfos(DefaultAcsClient client) throws Exception {
        GetURLUploadInfosRequest request = new GetURLUploadInfosRequest();
    
        String[] urls = {
            "http://xxx.cn-shanghai.aliyuncs.com/sample1.mp4",
            "http://xxx.cn-shanghai.aliyuncs.com/sample2.flv"
        };
        List<String> encodeUrlList = new ArrayList<String>();
        for(String url : urls){
            encodeUrlList.add(URLEncoder.encode(url, "UTF-8"));
        }
        request.setUploadURLs(StringUtils.join(encodeUrlList, ','));
        //request.setJobIds("xxx1,xxx2");
    
        return client.getAcsResponse(request);
    }
    // Call example
    public static void main(String[] argv) {
        DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
        GetURLUploadInfosResponse response = new GetURLUploadInfosResponse();
        try {
            response = getURLUploadInfos(client);
        } catch (Exception e) {
            System.out.print("ErrorMessage = " + e.getLocalizedMessage());
        }
        System.out.print("RequestId = " + response.getRequestId() + "\n");
    }


