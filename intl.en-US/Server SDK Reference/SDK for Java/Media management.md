# Media management

This topic provides examples on how to use the API operations of the media management module. The API operations are encapsulated in ApsaraVideo VOD SDK for Java. You can call the API operations to search for media asset information, modify video information, and query source file information. You can also query and delete videos and images.

## Initialize a client

Before you can use the SDK, initialize a client. For more information, see [Initialization](/intl.en-US/Server SDK Reference/SDK for Java/Initialization.md).

## Search for media asset information

You can call the SearchMedia operation to search for media asset information.

For more information about the request and response parameters of this operation, see [SearchMedia](/intl.en-US/API Reference/Media management/Media Search/SearchMedia.md). Example:

```
import com.aliyuncs.vod.model.v20170321.SearchMediaRequest;
import com.aliyuncs.vod.model.v20170321.SearchMediaResponse;

/**
 * Search for media asset information.
 * @param client The client that is used to send requests.
 * @return SearchMediaResponse The fields that must be contained in the response.
 * @throws Exception

*/
public static SearchMediaResponse searchMedia(DefaultAcsClient client) throws Exception {
    SearchMediaRequest request = new SearchMediaRequest();
    request.setFields("Title,CoverURL,Status");
    request.setMatch("Status in ('Normal','Checking') and CreationTime = ('2018-07-01T08:00:00Z','2018-08-01T08:00:00Z')");
    request.setPageNo(1);
    request.setPageSize(10);
    request.setSearchType("video");
    request.setSortBy("CreationTime:Desc");
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    SearchMediaResponse response = new SearchMediaResponse();
    try {
        response = searchMedia(client);
        if (response.getMediaList() ! = null && response.getMediaList().size() > 0) {
            System.out.print("Total = " + response.getTotal() + "\n");
            System.out.print("ScrollToken = " + response.getScrollToken() + "\n");
            for (SearchMediaResponse.Media media : response.getMediaList()) {
                System.out.print("MediaId = " + media.getMediaId() + "\n");
                System.out.print("MediaType = " + media.getMediaType() + "\n");
                System.out.print("CreationTime = " + media.getCreationTime() + "\n");
                System.out.print("Title = " + media.getVideo().getTitle() + "\n");
                System.out.print("CoverURL = " + media.getVideo().getCoverURL() + "\n");
                System.out.print("Status = " + media.getVideo().getStatus() + "\n");
            }
        }
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Query a video

You can call the GetVideoInfo operation to query details about a video.

For more information about the request and response parameters of this operation, see [GetVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfo.md). Example:

```
import com.aliyuncs.vod.model.v20170321.GetVideoInfoRequest;
import com.aliyuncs.vod.model.v20170321.GetVideoInfoResponse;

/**
 * Query a video.
 * @param client The client that is used to send requests.
 * @return GetVideoInfoResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static GetVideoInfoResponse getVideoInfo(DefaultAcsClient client) throws Exception {
    GetVideoInfoRequest request = new GetVideoInfoRequest();
    request.setVideoId("VideoId");
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    GetVideoInfoResponse response = new GetVideoInfoResponse();
    try {
        response = getVideoInfo(client);
        System.out.print("Title = " + response.getVideo().getTitle() + "\n");
        System.out.print("Description = " + response.getVideo().getDescription() + "\n");
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Query videos

You can call the GetVideoInfos operation to query videos.

For more information about the request and response parameters of this operation, see [GetVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoInfos.md). Example:

```
import com.aliyuncs.vod.model.v20170321.GetVideoInfosRequest;
import com.aliyuncs.vod.model.v20170321.GetVideoInfosResponse;

/**
 * Query videos.
 * @param client The client that is used to send requests.
 * @return GetVideoInfosResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static GetVideoInfosResponse getVideoInfos(DefaultAcsClient client) throws Exception {
    GetVideoInfosRequest request = new GetVideoInfosRequest();
    request.setVideoIds("VideoId1,VideoId2");
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    GetVideoInfosResponse response = new GetVideoInfosResponse();
    try {
        response = getVideoInfos(client);
        if (response.getVideoList() ! = null && response.getVideoList().size() > 0) {
            System.out.print("===== exist video infos : ===== \n");
            for (GetVideoInfosResponse.Video video : response.getVideoList()) {
                System.out.print("VideoId = " + video.getVideoId() + "\n");
                System.out.print("Title = " + video.getTitle() + "\n");
                System.out.print("Description = " + video.getDescription() + "\n");
                System.out.print("Tags = " + video.getTags() + "\n");
                System.out.print("CreationTime = " + video.getCreationTime() + "\n");
            }
        }
        if (response.getNonExistVideoIds() ! = null && response.getNonExistVideoIds().size() > 0) {
            System.out.print("===== nonexistent videoIds : ===== \n");
            for (String videoId : response.getNonExistVideoIds()) {
                System.out.print(videoId + "\n");
            }
        }
    } catch (Exception e) {
      System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Modify the information about a video

You can call the UpdateVideoInfo operation to modify the information about a video.

For more information about the request and response parameters of this operation, see [UpdateVideoInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfo.md). Example:

```
import com.aliyuncs.vod.model.v20170321.UpdateVideoInfoRequest;
import com.aliyuncs.vod.model.v20170321.UpdateVideoInfoResponse;

/**
 * Modify the information about a video.
 * @param client The client that is used to send requests.
 * @return UpdateVideoInfoResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static UpdateVideoInfoResponse updateVideoInfo(DefaultAcsClient client) throws Exception {
    UpdateVideoInfoRequest request = new UpdateVideoInfoRequest();
    request.setVideoId("VideoId");
    request.setTitle("new Title");
    request.setDescription("new Description");
    request.setTags("new Tag1,new Tag2");
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    UpdateVideoInfoResponse response = new UpdateVideoInfoResponse();
    try {
        response = updateVideoInfo(client);
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Modify the information about videos

You can call the UpdateVideoInfos operation to modify the information about videos.

For more information about the request and response parameters of this operation, see [UpdateVideoInfos](/intl.en-US/API Reference/Media management/Audio&Video Management/UpdateVideoInfos.md). Example:

```
import com.aliyuncs.vod.model.v20170321.UpdateVideoInfosRequest;
import com.aliyuncs.vod.model.v20170321.UpdateVideoInfosResponse;
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;

/**
 * Modify the information about videos.
 * @param client The client that is used to send requests.
 * @return UpdateVideoInfosResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static UpdateVideoInfosResponse updateVideoInfos(DefaultAcsClient client) throws Exception {
    UpdateVideoInfosRequest request = new UpdateVideoInfosRequest();
    JSONArray updateContentArray = new JSONArray();
    JSONObject updateContent1 = new JSONObject();
    updateContent1.put("VideoId", "VideoId1");
    // updateContent1.put("Title", "new Title");
    // updateContent1.put("Tags", "new Tag1,new Tag2");
    updateContentArray.add((updateContent1));
    JSONObject updateContent2 = new JSONObject();
    updateContent2.put("VideoId", "VideoId2");
    // updateContent2.put("Title", "new Title");
    // updateContent2.put("Tags", "new Tag1,new Tag2");
    updateContentArray.add((updateContent2));
    request.setUpdateContent(updateContentArray.toJSONString());
    DefaultAcsClient client = init();
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    UpdateVideoInfosResponse response = new UpdateVideoInfosResponse();
    try {
        response = updateVideoInfos(client);
        if (response.getNonExistVideoIds() ! = null && response.getNonExistVideoIds().size() > 0) {
            System.out.print("======nonexistent VideoIds : ======\n");
            for (String videoId : response.getNonExistVideoIds()) {
                System.out.print(videoId + "\n");
            }
        }
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Delete videos

You can call the DeleteVideo operation to delete videos.

For more information about the request and response parameters of this operation, see [DeleteVideo](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteVideo.md). Example:

```
import com.aliyuncs.vod.model.v20170321.DeleteVideoRequest;
import com.aliyuncs.vod.model.v20170321.DeleteVideoResponse;

/**
 * Delete videos.
 * @param client The client that is used to send requests.
 * @return DeleteVideoResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static DeleteVideoResponse deleteVideo(DefaultAcsClient client) throws Exception {
    DeleteVideoRequest request = new DeleteVideoRequest();
    // The IDs of the videos that you want to delete. Separate multiple IDs with commas (,).
    request.setVideoIds("VideoId1,VideoId2");
    return client.getAcsResponse(request);
}

/* Call example */
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    DeleteVideoResponse response = new DeleteVideoResponse();
    try {
        response = deleteVideo(client);
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Query source file information \(including the file URL\)

You can call the GetMezzanineInfo operation to query source file information.

For more information about the request and response parameters of this operation, see [GetMezzanineInfo](/intl.en-US/API Reference/Media management/Audio&Video Management/GetMezzanineInfo.md). Example:

```
import com.aliyuncs.vod.model.v20170321.GetMezzanineInfoRequest;
import com.aliyuncs.vod.model.v20170321.GetMezzanineInfoResponse;

/**
 * Query source file information.
 * @param client The client that is used to send requests.
 * @return GetVideoInfoResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static GetMezzanineInfoResponse getMezzanineInfo(DefaultAcsClient client) throws Exception {
    GetMezzanineInfoRequest request = new GetMezzanineInfoRequest();
    request.setVideoId("VideoId");
    // The expiration time of the file URL.
    request.setAuthTimeout(3600L);
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    GetMezzanineInfoResponse response = new GetMezzanineInfoResponse();
    try {
        response = getMezzanineInfo(client);
        System.out.print("Mezzanine.VideoId = " + response.getMezzanine().getVideoId() + "\n");
        System.out.print("Mezzanine.FileURL = " + response.getMezzanine().getFileURL() + "\n");
        System.out.print("Mezzanine.Width = " + response.getMezzanine().getWidth() + "\n");
        System.out.print("Mezzanine.Height = " + response.getMezzanine().getHeight() + "\n");
        System.out.print("Mezzanine.Size = " + response.getMezzanine().getSize() + "\n");
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
            
```

## Query videos by using filter conditions

You can call the GetVideoList operation to query videos by using filter conditions.

For more information about the request and response parameters of this operation, see [GetVideoList](/intl.en-US/API Reference/Media management/Audio&Video Management/GetVideoList.md). Example:

```
import com.aliyuncs.vod.model.v20170321.GetVideoListRequest;
import com.aliyuncs.vod.model.v20170321.GetVideoListResponse;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;

// The function used to generate a time value based on the time of the DATE type. The generated time must be in UTC.
public static String generateUTCTime(Date time) {
    SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss'Z'");
    dateFormat.setTimeZone(new SimpleTimeZone(SimpleTimeZone.UTC_TIME, "UTC"));
    dateFormat.setLenient(false);
    return dateFormat.format(time);
}

/**
 * Query videos by using filter conditions.
 * @param client The client that is used to send requests.
 * @return GetVideoListResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static GetVideoListResponse getVideoList(DefaultAcsClient client) throws Exception {
    GetVideoListRequest request = new GetVideoListRequest();
    // Use the time one month before the current time and the current time as the beginning and end of the time range to query videos. The time must be in UTC.
    String monthAgoUTCTime = generateUTCTime(new Date(System.currentTimeMillis() - 30*86400*1000L));
    String nowUTCTime = generateUTCTime(new Date(System.currentTimeMillis()));
    // The beginning of the time range to query videos, in UTC.
    request.setStartTime(monthAgoUTCTime);
    // The end of the time range to query videos, in UTC.
    request.setEndTime(nowUTCTime);
    // The status of the video. Videos in all states are queried by default. Separate multiple states with commas (,).
    // request.setStatus("Uploading,Normal,Transcoding");
    request.setPageNo(1L);
    request.setPageSize(20L);
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    GetVideoListResponse response = new GetVideoListResponse();
    try {
        response = getVideoList(client);
        // The total number of videos that are returned based on the filter conditions.
        System.out.print("Total = " + response.getTotal() + "\n");
        for (GetVideoListResponse.Video video : response.getVideoList()) {
            System.out.print("Title = " + video.getTitle() + "\n");
            System.out.print("Description = " + video.getDescription() + "\n");
            System.out.print("Tags = " + video.getTags() + "\n");
            System.out.print("CreationTime = " + video.getCreationTime() + "\n");
        }
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}

            
```

## Delete a media stream

You can call the DeleteStream operation to delete a media stream.

For more information about the request and response parameters of this operation, see [DeleteStream](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteStream.md). Example:

```
import com.aliyuncs.vod.model.v20170321.DeleteStreamRequest;
import com.aliyuncs.vod.model.v20170321.DeleteStreamResponse;

/**
 * Delete a media stream.
 * @param client The client that is used to send requests.
 * @return DeleteMezzaninesResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static DeleteStreamResponse deleteStream(DefaultAcsClient client) throws Exception {
    DeleteStreamRequest request = new DeleteStreamRequest();
    request.setVideoId("VideoId");
    request.setJobIds("JobId1,JobId2");
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    DeleteStreamResponse response = new DeleteStreamResponse();
    try {
        response = deleteStream(client);
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Delete source files

You can call the DeleteMezzanines operation to delete source files.

For more information about the request and response parameters of this operation, see [DeleteMezzanines](/intl.en-US/API Reference/Media management/Audio&Video Management/DeleteMezzanines.md). Example:

```
import com.aliyuncs.vod.model.v20170321.DeleteMezzaninesRequest;
import com.aliyuncs.vod.model.v20170321.DeleteMezzaninesResponse;
/**
 * Delete source files.
 * @param client The client that is used to send requests.
 * @return DeleteMezzaninesResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static DeleteMezzaninesResponse deleteMezzanines(DefaultAcsClient client) throws Exception {
    DeleteMezzaninesRequest request = new DeleteMezzaninesRequest();
    // The IDs of the videos that you want to delete. Separate multiple IDs with commas (,).
    request.setVideoIds("VideoId1,VideoId2");
    request.setForce(false);
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    DeleteMezzaninesResponse response = new DeleteMezzaninesResponse();
    try {
        response = deleteMezzanines(client);
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}

            
```

## Modify the information about images

You can call the UpdateImageInfos operation to modify the information about images.

For more information about the request and response parameters of this operation, see [UpdateImageInfos](/intl.en-US/API Reference/Media management/Image Management/UpdateImageInfos.md). Example:

```
import com.aliyuncs.vod.model.v20170321.UpdateImageInfosRequest;
import com.aliyuncs.vod.model.v20170321.UpdateImageInfosResponse;
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;

/**
 * Modify the information about images.
 * @param client The client that is used to send requests.
 * @return UpdateImageInfosResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static UpdateImageInfosResponse updateImageInfos(DefaultAcsClient client) throws Exception{
        UpdateImageInfosRequest request = new UpdateImageInfosRequest();
        JSONArray updateContentArray = new JSONArray();
        JSONObject updateContent1 = new JSONObject();
        updateContent1.put("ImageId", "ImageId1");
//        updateContent1.put("Title", "new Title");
//        updateContent1.put("Tags", "new Tag1,new Tag2");
        updateContentArray.add((updateContent1));
        JSONObject updateContent2 = new JSONObject();
        updateContent2.put("ImageId", "ImageId2");
//        updateContent2.put("Title", "new Title");
//        updateContent2.put("Tags", "new Tag1,new Tag2");
        updateContentArray.add((updateContent2));
        request.setUpdateContent(updateContentArray.toJSONString());
        return client.getAcsResponse(request);
    }

// Call example
public static void main(String[] argv) throws Exception {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    UpdateImageInfosResponse response = new UpdateImageInfosResponse();
    try {
        response = updateImageInfos(client);
        if (response.getNonExistImageIds() ! = null && response.getNonExistImageIds().size() > 0) {
            System.out.print("======nonexistent ImageIds : ======\n");
            for (String imageId : response.getNonExistImageIds()) {
                System.out.print(imageId + "\n");
            }
        }
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Query an image

You can call the GetImageInfo operation to query details about an image.

For more information about the request and response parameters of this operation, see [GetImageInfo](/intl.en-US/API Reference/Media management/Image Management/GetImageInfo.md). Example:

```
import com.aliyuncs.vod.model.v20170321.GetImageInfoRequest;
import com.aliyuncs.vod.model.v20170321.GetImageInfoResponse;

/**
 * Query an image.
 *
 * @param client The client that is used to send requests.
 * @return GetImageInfoResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static GetImageInfoResponse getImageInfo(DefaultAcsClient client) throws Exception {
    GetImageInfoRequest request = new GetImageInfoRequest();
    request.setImageId("ImageId");
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) throws ClientException {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    GetImageInfoResponse response = new GetImageInfoResponse();
    try {
        response = getImageInfo(client);
        System.out.print("ImageId=" + response.getImageInfo().getImageId());
        System.out.print("Title=" + response.getImageInfo().getTitle());
        System.out.print("CreationTime=" + response.getImageInfo().getCreationTime());
        System.out.print("FileURL=" + response.getImageInfo().getMezzanine().getFileURL());
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

## Delete images

You can call the DeleteImage operation to delete images.

For more information about the request and response parameters of this operation, see [DeleteImage](/intl.en-US/API Reference/Media management/Image Management/DeleteImage.md). Example:

```
import com.aliyuncs.vod.model.v20170321.DeleteImageRequest;
import com.aliyuncs.vod.model.v20170321.DeleteImageResponse;

/**
 * Delete images.
 *
 * @param client The client that is used to send requests.
 * @return DeleteImageResponse The fields that must be contained in the response.
 * @throws Exception
*/
public static DeleteImageResponse deleteImage(DefaultAcsClient client) throws Exception {
    DeleteImageRequest request = new DeleteImageRequest();
    // Delete an image file based on ImageURL.
    request.setDeleteImageType("ImageURL");
    String url = "http://sample.aliyun.com/cover.jpg";
    String encodeUrl = URLEncoder.encode(url, "UTF-8");
    request.setImageURLs(encodeUrl);
    // Delete image files based on ImageId.
    //request.setDeleteImageType("ImageId");
    //request.setImageIds("ImageId1,ImageId2");
    // Delete image files based on VideoId and ImageType.
    //request.setDeleteImageType("VideoId");
    //request.setVideoId("VideoId");
    //request.setImageType("SpriteSnapshot");
    return client.getAcsResponse(request);
}

// Call example
public static void main(String[] argv) throws ClientException {
    DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
    DeleteImageResponse response = new DeleteImageResponse();
    try {
        response = deleteImage(client);
    } catch (Exception e) {
        System.out.print("ErrorMessage = " + e.getLocalizedMessage());
    }
    System.out.print("RequestId = " + response.getRequestId() + "\n");
}
```

