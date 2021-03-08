# Migrate resources to ApsaraVideo VOD

Users of ApsaraVideo VOD may want to migrate many existing videos that are stored on their personal websites or the cloud to ApsaraVideo VOD. This topic describes how to migrate videos to ApsaraVideo VOD.

## Preparations

-   [Register](https://account.aliyun.com/register/register.htm?spm=a2c4g.11186623.2.21.1d881e71wvM58e&oauth_callback=https%3A%2F%2Fvod.console.aliyun.com%2F&lang=zh) an Alibaba Cloud account, complete [real-name verification](https://help.aliyun.com/knowledge_list/37170.html?spm=a2c4g.11186623.2.22.1d881e71wvM58e), and activate [ApsaraVideo VOD](https://www.aliyun.com/product/vod?spm=a2c4g.11186623.2.23.1d881e71wvM58e).
-   Obtain an AccessKey to access ApsaraVideo VOD. You can create an AccessKey for your Alibaba Cloud account on the [AccessKey Management](https://ak-console.aliyun.com/?spm=a2c4g.11186623.2.24.1d881e71wvM58e#/accesskey) page in the Alibaba Cloud Management Console. Alternatively, you can create a RAM user in the [Resource Access Management \(RAM\) console](https://ram.console.aliyun.com/?spm=a2c4g.11186623.2.25.1d881e71wvM58e#/user/list) and grant the user the permission to access ApsaraVideo VOD. For more information, see [RAM user access](https://help.aliyun.com/document_detail/57056.html?spm=a2c4g.11186623.2.26.1d881e71wvM58e).

## Flowchart of uploading videos by using an upload SDK

-   **Upload without using ECS**

    ![Upload without using ECS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3823815161/p183910.png)

-   **Upload using ECS**

    ![Upload using ECS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3823815161/p183911.png)


**Note:** If the videos to be migrated are stored in Object Storage Service \(OSS\) or another Alibaba Cloud account in ApsaraVideo VOD and the video mezzanine files use an internal endpoint, you can download the files to Elastic Compute Service \(ECS\) instances by using the internal network. For more information, see the [Migrate videos by using an internal endpoint](https://help.aliyun.com/document_detail/163389.html?spm=a2c4g.11186623.6.1174.76c565ddFJlQvW#section-qhy-12b-f00) section.

## Procedure

1.  **Prepare videos to be migrated.**

    **Note:** You must prepare mezzanine file URLs for all videos to be migrated. If the mezzanine file URLs require signing, make sure that the URLs are valid for long enough to avoid invalid URLs during the download process.

    You can save the mezzanine file URLs of videos to be migrated based on your data processing habits. In this example, each mezzanine file URL is written in a separate line in a text file, as shown in the following figure.

    ![Videos to be migrated](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3823815161/p183913.png)

2.  **Write a video upload program.**

    **Note:** When you write the program, record the mappings between the mezzanine file URLs and the video IDs that are generated after videos are uploaded to ApsaraVideo VOD. After the videos are migrated, you can sort the videos based on the mappings.

    This section introduces two methods to upload videos. Choose an upload method based on your business needs. We recommend that you use method 1.

    1.  \(Recommended\) Method 1: use an upload SDK that is provided by ApsaraVideo VOD to upload videos

        This method does not change the migration process. Videos are uploaded in a synchronous way, ensuring timeliness. When you use the upload SDK, we recommend that you deploy the program on an ECS instance that resides in the same region as the bucket that is allocated by ApsaraVideo VOD. For Chinese domestic users, the default bucket that is allocated by ApsaraVideo VOD resides in the China \(Shanghai\) region. You must prepare the ECS instance in advance. After you specify the regionId parameter in the SDK, videos are automatically uploaded to ApsaraVideo VOD by using the internal network.

        For more information about the upload SDK, see [Overview](https://help.aliyun.com/document_detail/52200.html?spm=a2c4g.11186623.2.31.1d881e71wvM58e).

        ```
        import com.aliyun.vod.upload.impl.UploadVideoImpl;
        import com.aliyun.vod.upload.req.UploadStreamRequest;
        import com.aliyun.vod.upload.resp.UploadStreamResponse;
        import java.io.*;
        import java.net.URL;
        
        /**
         * Use an upload SDK to upload videos.
         */
        public class UploadStreamDemo {
            /**
             * The stream upload operation.
             *
             * @param accessKeyId
             * @param accessKeySecret
             * @param title
             * @param fileName
             * @param inputStream
             */
            private static void testUploadStream(String accessKeyId, String accessKeySecret, String title, String fileName, InputStream inputStream) {
                UploadStreamRequest request = new UploadStreamRequest(accessKeyId, accessKeySecret, title, fileName, inputStream);
                
                /* Customize the callback configuration for event notifications. For more information about the parameters, see https://help.aliyun.com/document_detail/86952.html#UserData. */
                //request.setUserData(""{\"Extend\":{\"test\":\"www\",\"localId\":\"xxxx\"},\"MessageCallback\":{\"CallbackURL\":\"http://test.test.com\"}}"");
                /* Optional. Specify the category ID of the video. */
                //request.setCateId(0);
                /* Optional. Specify the tags of the video. Separate multiple tags with commas (,). */
                //request.setTags("tag 1,tag 2");
                /* Optional. Specify the description of the video. */
                //request.setDescription("The video description");
                /* Optional. Specify the thumbnail of the video. */
                //request.setCoverURL("http://cover.sample.com/sample.jpg");
                /* Optional. Specify the ID of the template group. */
                //request.setTemplateGroupId("8c4792cbc8694e****fd5330e56a33d");
                /* Optional. Specify the ID of the workflow. */
                //request.setWorkflowId("d4430d07361f****1339577859b0177b");
                /* Optional. Specify the storage region. */
                //request.setStorageLocation("outin-20170323****266-5sejdln9o.oss-cn-shanghai.aliyuncs.com");
                /* Specify the access region of ApsaraVideo VOD. */
                request.setApiRegionId("cn-shanghai");
                /* Specify the region where the ECS instance is deployed. */
                // request.setEcsRegionId("cn-shanghai");
                UploadVideoImpl uploader = new UploadVideoImpl();
                UploadStreamResponse response = uploader.uploadStream(request);
                System.out.print("RequestId=" + response.getRequestId() + "\n");  // Specify the ID of the request that is sent to ApsaraVideo VOD.
                if (response.isSuccess()) {
                    System.out.print("VideoId=" + response.getVideoId() + "\n");
                } else { // If the callback URL that you set is invalid, video upload is not affected, and the video ID and error code are returned. If the upload fails in other cases, the video ID is empty. Analyze the cause based on the returned error code.
                    System.out.print("VideoId=" + response.getVideoId() + "\n");
                    System.out.print("ErrorCode=" + response.getCode() + "\n");
                    System.out.print("ErrorMessage=" + response.getMessage() + "\n");
                }
            }
        
            public static void main(String[] args) {
                /**
                 * Specify the video URL, pass in the media asset information of the video, and then upload the video.
                 */
                InputStream inputStream = null;
                String url = "http://test.aliyun.com/video/test.mp4";
                try {
                    inputStream = new URL(url).openStream();
                } catch (IOException e) {
                    e.printStackTrace();
                }
                testUploadStream("<Your AccessKeyId>", "<Your AccessKeySecret>", "title", "video-1.mp4", inputStream);
            }
        }
        ```

    2.  **\(Not recommended\) Method 2: upload videos by using URLs**

        [UploadMediaByURL](https://help.aliyun.com/document_detail/86311.html?spm=a2c4g.11186623.2.32.1d881e71wvM58e)

        You can refer to the following sample code to pass in the mezzanine file URLs of videos to be migrated one by one, and then submit the upload task. Alternatively, you can pass in the media asset information such as the title, category, and description of each video during the upload based on your business needs. This way, the migration process remains unchanged. However, you must design the specific behavior of the migration step based on your scenario.

        ```
        import com.alibaba.fastjson.JSON;
        import com.alibaba.fastjson.JSONArray;
        import com.alibaba.fastjson.JSONObject;
        import com.aliyuncs.DefaultAcsClient;
        import com.aliyuncs.exceptions.ClientException;
        import com.aliyuncs.profile.DefaultProfile;
        import com.aliyuncs.vod.model.v20170321.UploadMediaByURLRequest;
        import com.aliyuncs.vod.model.v20170321.UploadMediaByURLResponse;
        import java.net.URLEncoder;
        
        /**
         * Asynchronously upload multiple videos based on mezzanine file URLs.
         * Before you call the UploadMediaByURL operation, we recommend that you read the document of the operation to understand its advantages and disadvantages.
         * https://help.aliyun.com/document_detail/86311.html?spm=a2c4g.11186623.6.714.4d9d3dbdFBPe6k
         */
        public class UploadMediaByURLDemo {
            public static DefaultAcsClient initVodClient(String accessKeyId, String accessKeySecret) throws ClientException {
                String regionId = "cn-shanghai";  // Specify the access region of ApsaraVideo VOD.
                DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
                DefaultAcsClient client = new DefaultAcsClient(profile);
                return client;
            }
        
            /**
             * Upload multiple videos based on mezzanine file URLs.
             * @param client The client that sends a request.
             * @return UploadMediaByURLResponse The response to the request for uploading multiple videos based on mezzanine file URLs.
             * @throws Exception
             */
            public static UploadMediaByURLResponse uploadMediaByURL(DefaultAcsClient client,String url) throws Exception{
                UploadMediaByURLRequest request = new UploadMediaByURLRequest();
                //String url = "http://xxxx.mp4";
                String encodeUrl = URLEncoder.encode(url, "UTF-8");
                request.setUploadURLs(encodeUrl);
        
                // The metadata of the uploaded video. The value is a JSON string.
                JSONObject uploadMetadata = new JSONObject();
                uploadMetadata.put("SourceUrl", encodeUrl);
                uploadMetadata.put("Title", "upload by url sample");
                JSONArray uploadMetadataList = new JSONArray();
                uploadMetadataList.add(uploadMetadata);
                request.setUploadMetadatas(uploadMetadataList.toJSONString());
                JSONObject userData = new JSONObject();
                
            // The callback configuration. In the ApsaraVideo VOD console, select the Video Upload Completed event. When a video is uploaded, ApsaraVideo VOD sends a notification to the specified callback URL.
                JSONObject messageCallback = new JSONObject();
                messageCallback.put("CallbackURL", "http://xxxxx");// The URL that is used to receive callbacks.
                messageCallback.put("CallbackType", "http");
                userData.put("MessageCallback", messageCallback.toJSONString());
                JSONObject extend = new JSONObject();// The message object. The value is written to the callback message and is transparently transmitted.
                extend.put("MyId", "user-defined-id");
                userData.put("Extend", extend.toJSONString());
                request.setUserData(userData.toJSONString());
                return client.getAcsResponse(request);
            }
        
            // Call example
            public static void main(String[] argv) throws ClientException {
                DefaultAcsClient client = initVodClient("<Your AccessKeyId>", "<Your AccessKeySecret>");
                UploadMediaByURLResponse response = new UploadMediaByURLResponse();
                try { 
            // You can modify the code to read the prepared text file that records the mezzanine file URLs of videos to be migrated.
                    response = uploadMediaByURL(client,"http://xxxx.mp4"); The mezzanine file URL of the video to be uploaded.
                    System.out.print("UploadJobs = " + JSON.toJSONString(response.getUploadJobs()) + "\n");
                } catch (Exception e) {
                    System.out.print("ErrorMessage = " + e.getLocalizedMessage());
                }
                System.out.print("RequestId = " + response.getRequestId() + "\n");
            }
        }
        ```

3.  **Deploy the program to upload videos.**
    1.  After you write the program based on your scenario and upload the code, deploy the program to upload videos to ApsaraVideo VOD.
    2.  If you need to sort videos after the migration, configure the program to record the mappings between the mezzanine file URLs and the video IDs that are generated after videos are uploaded. You can record the mappings by selecting a method based on your business needs. For example, you can record the mappings in logs or write the mezzanine file URLs in the media asset information of videos during the upload.

        **Note:** The response of the UploadMediaByURL operation contains the mezzanine file URLs of videos. You can use the information based on your business needs.

4.  **Sort migrated videos based on video mappings before and after migration.**

    After the videos are migrated, you can sort the videos based on the recorded mappings between the mezzanine file URLs and the video IDs that are generated after videos are uploaded to ApsaraVideo VOD.


## Migrate videos between Alibaba Cloud accounts

If you need to copy your videos in ApsaraVideo VOD to provide services for users in more regions, you can migrate videos between Alibaba Cloud accounts across regions. Specifically, you can migrate videos from the bucket that is allocated by ApsaraVideo VOD for an Alibaba Cloud account to the bucket that is allocated for another Alibaba Cloud account.

To migrate videos between Alibaba Cloud accounts, perform the following steps:

-   Call the [SearchMedia](https://help.aliyun.com/document_detail/86044.html?spm=a2c4g.11186623.2.39.43cb448bfq3s1c) operation of ApsaraVideo VOD to query the IDs of videos to be migrated.
-   Based on the video IDs, call the [GetMezzanineInfo](https://help.aliyun.com/document_detail/59624.html?spm=a2c4g.11186623.6.734.49b46ad8SkcARX) operation of ApsaraVideo VOD to obtain the mezzanine file URLs of videos to be migrated. Then, save the result.

    **Note:** If the video mezzanine files are transcoded, you can use the [media asset export](https://help.aliyun.com/document_detail/86057.html?spm=5176.11065259.1996646101.searchclickresult.288c1a90mLpVit) feature of ApsaraVideo VOD to obtain the URLs of transcoded video files.

    ![Export media assets](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3823815161/p183918.png)

-   Repeat Step 2 to Step 4 in the Procedure section to migrate videos.

## Migrate videos by using an internal endpoint

If your ECS instance resides in the same region as the video mezzanine files, we recommend that you perform the following operations before you migrate videos: Call the GetMezzanineInfo operation to obtain the OSS endpoints of video files, and manually replace the domain name of the OSS endpoints with the [internal endpoint of OSS](https://help.aliyun.com/document_detail/31834.html?spm=a2c4g.11186623.2.37.58651e71GAQUmW#title-7oh-gcr-v98). For more information, see [Access to OSS resources from ECS instances by using the internal endpoint of OSS](https://help.aliyun.com/knowledge_detail/39584.html?spm=a2c4g.11186623.2.38.58651e71GAQUmW).

Assume that the OSS endpoint of a video is outin-67870fd5b29\*\*\*\*98a3900163e1c35d5.oss-cn-shanghai.aliyuncs.com/customerTrans/2a13b91506f9158f\*\*\*\*7317f4a9d4c9/30f24681-1718d5c6237-\*\*4bd.mp4.

Then, you can append -internal to the OSS region ID to download the video to your ECS instance by using the internal network. The new URL is outin-67870fd5b29\*\*\*\*98a3900163e1c35d5.oss-cn-shanghai-internal.aliyuncs.com/customerTrans/2a13b91506f9158f\*\*\*\*7317f4a9d4c9/30f24681-1718d5c6237-\*\*4bd.mp4.

![Migrate videos by using an internal endpoint](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4823815161/p183920.png)

