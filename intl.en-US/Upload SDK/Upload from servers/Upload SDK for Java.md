# Upload SDK for Java

You can use the upload SDKs of ApsaraVideo VOD to upload media files with efficiency. This topic provides an example to describe how to use the upload SDK for Java.

## Features

The upload SDK for Java provides the following major features:

-   Allows you to upload on-premises audio or video files to ApsaraVideo VOD: By default, multipart upload is used. A single file to upload can be up to 48.8 TB in size. Resumable upload is supported.
-   Allows you to upload online video or audio files to ApsaraVideo VOD: After you specify the URL of an online video or audio file, the upload SDK automatically downloads the video or audio file from the URL and uploads it to ApsaraVideo VOD. A single file to upload can be up to 48.8 TB in size.
-   Allows you to upload on-premises images to ApsaraVideo VOD: After you specify the on-premises directory of an image, the upload SDK automatically uploads the image to ApsaraVideo VOD.
-   Allows you to upload online images to ApsaraVideo VOD: After you specify the URL of an online image, the upload SDK automatically downloads the image from the URL and uploads it to ApsaraVideo VOD.
-   Allows you to upload on-premises M3U8 audio and video files, including all part files, to ApsaraVideo VOD: To upload the files, you must specify the on-premises directories of M3U8 index files and part files.
-   Allows you to upload online M3U8 audio and video files, including all part files, to ApsaraVideo VOD: To upload the files, you must specify the URLs of M3U8 index files and part files.
-   Allows you to upload on-premises auxiliary media assets to ApsaraVideo VOD: After you specify the on-premises directory of an auxiliary media asset, the upload SDK automatically uploads the asset to ApsaraVideo VOD.
-   Allows you to upload online auxiliary media assets to ApsaraVideo VOD: After you specify the URL of an auxiliary media asset, the upload SDK automatically downloads the asset from the URL and uploads it to ApsaraVideo VOD.

The upload SDK for Java provides the following additional features:

-   Provides an upload progress bar and supports the callbacks for default and custom upload progress. This feature is unavailable for the upload of M3U8 files.
-   Allows you to specify the region of an Elastic Compute Service \(ECS\) instance on which the upload script is to be deployed. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the specified file is automatically uploaded by using an internal network. This can accelerate the upload speed and save the public network traffic. The ApsaraVideo VOD provides only public endpoints for you to use the API. Therefore, you must use an ECS instance that can be accessed over the Internet to deploy an upload script.
-   Allows you to specify the VOD center and storage region to facilitate upload outside China. The default VOD center is in the China \(Shanghai\) region.
-   Allows you to set the metadata, such as the title, storage locations, user data, transcoding templates, and media workflows for the upload.
-   Supports playback based on Security Token Service \(STS\) tokens. Specific methods are required to obtain and specify STS tokens. During the upload, if the STS token expires, the SDK periodically requests a new STS token and sends it to the server to resume the upload.

For more information about the file formats that are supported by ApsaraVideo VOD, see the "Supported file formats" section of [Overview](/intl.en-US/Developer Guide/Upload Medias/Overview.md).

## Install the SDK

1.  Download the VODUploadDemo-java-1.4.13.zip package, which contains the upload SDK for Java and sample code. For more information, see the "Download server upload SDKs" section of [SDK download](/intl.en-US/SDK Downloads/SDK download.md).

    **Note:** In this topic, Java 1.8 and SDK V1.4.13 are used as an example. You can use other versions based on your business requirements.

2.  Decompress the VODUploadDemo-java-1.4.13.zip package and copy all the JAR packages in the lib directory to your project.

    **Note:** Only the versions of specific dependent JAR packages are listed below. You can add a Maven dependency to your project. Alternatively, you can copy all JAR packages in the VODUploadDemo-java-1.4.13.zip package to your project. Take note of the following rules on JAR packages:

    -   When you use the aliyun-java-vod-upload-1.4.13.jar package to install the upload SDK for Java, aliyun-sdk-oss must be of the version 3.9.0 or later.
    -   ApsaraVideo VOD has been released in the China \(Shanghai\), China \(Beijing\), and China \(Shenzhen\) regions. To use the upload SDK for Java to upload files to these regions, you must use aliyun-java-sdk-vod V2.15.11 and aliyun-java-sdk-core V4.4.5 or later.
    ```
       <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-core</artifactId>
            <version>4.5.1</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun.oss</groupId>
            <artifactId>aliyun-sdk-oss</artifactId>
            <version>3.10.2</version>
        </dependency>
         <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-vod</artifactId>
            <version>2.15.11</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.28</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20170516</version>
        </dependency>
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.8.2</version>
        </dependency>
    ```

3.  Reference the JAR packages in an integrated development environment \(IDE\), such as Eclipse or IntelliJ IDEA.

    -   Right-click your project name in Eclipse and choose **Properties** \> **Java Build Path** \> **Add JARs**.
    -   In IntelliJ IDEA, select your project and choose **File** \> **Project Structure** \> **Modules**. On the right-side **Dependencies** tab, click the **+** icon, and select **JARs or directories**.
4.  Select all the JAR packages that you have copied in [Step 2](#step_cmy_ho2_gk9).

    After you perform the preceding steps, you can use the upload SDK for Java in your Eclipse or IntelliJ IDEA project.


## Sample code

-   Sample code of the upload SDK

    After you decompress the VODUploadDemo-java-1.4.13.zip package, the UploadVideoDemo.java file generated in the sample directory provides the sample program for uploading files. The following sample code is for your reference:

    ```
    public class UploadVideoDemo {
        // Required. The AccessKey ID of your Alibaba Cloud account.
        private static final String accessKeyId = "";
        // Required. The AccessKey secret of your Alibaba Cloud account.
        private static final String accessKeySecret = "";
    
        public static void main(String[] args) {
            //1. Upload an on-premises video or audio file.
            // Required. The title of the file.
            String title = "Test title";
            // When you upload an on-premises file or a file stream, set the file name to the absolute path of the file, such as /User/sample/file name.mp4. This parameter is required.
            // The file name must contain an extension.
            String fileName = "Test file name.mp4";
            // Upload the on-premises file.
            testUploadVideo(accessKeyId, accessKeySecret, title, fileName);
    
            //2. Upload an on-premises image.
            testUploadImageLocalFile(accessKeyId, accessKeySecret);
        }
    
        /**
         * Set the method for uploading on-premises files.
         *
         * @param accessKeyId
         * @param accessKeySecret
         * @param title
         * @param fileName
         */
        private static void testUploadVideo(String accessKeyId, String accessKeySecret, String title, String fileName) {
            UploadVideoRequest request = new UploadVideoRequest(accessKeyId, accessKeySecret, title, fileName);
            /* Specify the size of each part in multipart upload. Default value: 1. Unit: MB. */
            request.setPartSize(1 * 1024 * 1024L);
            /* Specify the number of concurrent threads for multipart upload. The default value is 1. Note that this setting consumes CPU resources of the server. You can set a value based on your server load. */
            request.setTaskNum(1);
            /* Specify whether to enable resumable upload. By default, resumable upload is disabled. If the upload is paused upon a network disconnection or when the program does not respond, you can send the upload request again to resume the upload. Resumable upload is applicable for large files that cannot be completely uploaded within the timeout period of 3,000 seconds.
            Note: If resumable upload is enabled, the upload progress is written to an on-premises disk file during the upload process. This affects the upload speed. Specify whether to enable resumable upload based on your business requirements. */
            request.setEnableCheckpoint(false);
            /* Specify the timeout period of Object Storage Service (OSS) slow requests for each part, in milliseconds. If the system takes more time than the specified timeout period to upload a part, a debug log is displayed. You can adjust the threshold to prevent displaying debug logs. Default value: 300000. */
            //request.setSlowRequestsThreshold(300000L);
            /* Specify the timeout period of slow requests for each part, in seconds. Default value: 300. */
            //request.setSlowRequestsThreshold(300000L);
            /* Optional. Specify whether to apply the default watermark. You can specify whether to apply the default watermark based on the template group configuration. */
            //request.setIsShowWaterMark(true);
            /* Customize the callback configuration for event notifications. For more information about the parameters, see https://help.aliyun.com/document_detail/86952.html#UserData. */
            // request.setUserData("{\"Extend\":{\"test\":\"www\",\"localId\":\"xxxx\"},\"MessageCallback\":{\"CallbackURL\":\"http://test.test.com\"}}");
    
            /* Optional. Specify the category ID of the video. */
            //request.setCateId(0);
            /* Optional. Specify the tags of the video. Separate multiple tags with commas (,). */
            //request.setTags("tag 1,tag 2");
            /* Optional. Specify the description of the video. */
            //request.setDescription("Video description");
            /* Optional. Specify the thumbnail of the video. */
            //request.setCoverURL("http://cover.sample.com/sample.jpg");
            /* Optional. Specify the ID of the template group used for the video. */
            //request.setTemplateGroupId("8c4792cbc8694*****d5330e56a33d");
            /* Specify the access region of ApsaraVideo VOD. */
            //request.setApiRegionId("cn-shanghai");
            /* The region of the ECS instance that is used for the upload. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the specified file is automatically uploaded by using an internal network. */
            // request.setEcsRegionId("cn-shanghai");
            /* Optional. Specify the storage region of ApsaraVideo VOD. */
            //request.setStorageLocation("in-2017032*****18266-5sejdln9o.oss-cn-shanghai.aliyuncs.com");
            /* Enable the default callback for upload progress. */
            // request.setPrintProgress(true);
            /* Customize the callback for upload progress. This callback must inherit ProgressListener. */
            // request.setProgressListener(new PutObjectProgressListener());
            UploadVideoImpl uploader = new UploadVideoImpl();
            UploadVideoResponse response = uploader.uploadVideo(request);
            System.out.print("RequestId=" + response.getRequestId()   "\n");  // Specify the ID of the request that is sent to ApsaraVideo VOD.
            if (response.isSuccess()) {
                System.out.print("VideoId="   response.getVideoId()   "\n");
            } else {
                // If the callback URL that you set is invalid, video upload is not affected, and the video ID and error code are returned. If the upload fails in other cases, the video ID is empty. Analyze the cause based on the returned error code.
                System.out.print("VideoId="   response.getVideoId()   "\n");
                System.out.print("ErrorCode="   response.getCode()   "\n");
                System.out.print("ErrorMessage="   response.getMessage()   "\n");
            }
        }
    
        /**
         * Set the method for uploading on-premises images.
         * For more information about the parameters, see https://help.aliyun.com/document_detail/55619.html.
         *
         * @param accessKeyId
         * @param accessKeySecret
         */
        private static void testUploadImageLocalFile(String accessKeyId, String accessKeySecret) {
            // Required. Specify the type of the image. Valid values: default, cover, and watermark.
            String imageType = "cover";
            UploadImageRequest request = new UploadImageRequest(accessKeyId, accessKeySecret, imageType);
            /* Optional. Specify the file name extension of the image. Valid values: png, jpg, and jpeg. */
            //request.setImageExt("png");
            /* Optional. Specify the title of the image. The value cannot exceed 128 bytes in length. Encode the title in UTF-8. */
            // request.setTitle("Image title");
            /* Optional. Specify the tags of the image. A tag can be up to 32 bytes in length. You can enter a maximum of 16 tags. Separate multiple tags with commas (,). Encode the tags in UTF-8. */
            //request.setTags("tag 1,tag 2");
            /* Optional. Specify the storage region of ApsaraVideo VOD. */
            //request.setStorageLocation("out-4f3952f78c021*****013e7.oss-cn-shanghai.aliyuncs.com");
            /* Optional. In streaming upload, the InputStream parameter is required. Set the fileName parameter to the name of the mezzanine file. The file name must contain an extension, such as .png. */
            //request.setFileName("Test file name.png");
            /* Enable the default callback for upload progress. */
            // request.setPrintProgress(true);
            /* Customize the callback for upload progress. This callback must inherit ProgressListener. */
            // request.setProgressListener(new PutObjectProgressListener());
            /* Specify the access region of ApsaraVideo VOD. */
            //request.setApiRegionId("cn-shanghai");
            /* The region of the ECS instance that is used for the upload. If the region of the ECS instance is the same as the storage region in ApsaraVideo VOD, the specified file is automatically uploaded by using an internal network. */
            // request.setEcsRegionId("cn-shanghai");
    
            UploadImageImpl uploadImage = new UploadImageImpl();
            UploadImageResponse response = uploadImage.upload(request);
            System.out.print("RequestId="   response.getRequestId()   "\n");
            if (response.isSuccess()) {
                System.out.print("ImageId="   response.getImageId()   "\n");
                System.out.print("ImageURL="   response.getImageURL()   "\n");
            } else {
                System.out.print("ErrorCode="   response.getCode()   "\n");
                System.out.print("ErrorMessage="   response.getMessage()   "\n");
            }
    
    
        }
    }
    ```

-   Example of the upload progress bar

    After you decompress the VODUploadDemo-java-1.4.13.zip package, the PutObjectProgressListener.java file generated in the sample directory provides the sample program for the callback for upload progress. This class must inherit the VoDProgressListener class. ProgressEvent indicates an event generated to notify you of the upload progress when you upload a file to OSS. You can customize the business processing logic of different event notifications. The following sample code is for your reference:

    ```
    import com.aliyun.oss.event.ProgressEvent;
    import com.aliyun.oss.event.ProgressEventType;
    
    /**
     * Specify the class of callbacks for upload progress.
     * The callback takes effect only when you enable the callback for upload progress.
     * A callback is fired when the upload of a part to OSS succeeds or fails. You can handle event callbacks based on the business processing logic.
     * After the video or audio information is created, the videoId parameter in the callback for upload progress indicates the video ID generated in the current upload. You can manage video and audio files based on the video ID.
     * After the image information is created, the ImageId parameter in the callback for upload progress indicates the image ID generated in the current upload. You can manage images based on the image ID.
     */
    
    public class PutObjectProgressListener implements VoDProgressListener {
        /**
         * The number of bytes that have been uploaded to OSS.
         */
        private long bytesWritten = 0;
        /**
         * The total size of the mezzanine file, in bytes.
         */
        private long totalBytes = -1;
        /**
         * Indicates whether the upload succeeds.
         */
        private boolean succeed = false;
        /**
         * The ID of the video.
         */
        private String videoId;
        /**
         * The ID of the image.
         */
        private String imageId;
    
        public void progressChanged(ProgressEvent progressEvent) {
            long bytes = progressEvent.getBytes();
            ProgressEventType eventType = progressEvent.getEventType();
            switch (eventType) {
                // The event notification indicating that the upload starts.
                case TRANSFER_STARTED_EVENT:
                    if (videoId ! = null) {
                        System.out.println("Start to upload videoId "   videoId   "......");
                    }
                    if (imageId ! = null) {
                        System.out.println("Start to upload imageId "   imageId   "......");
                    }
                    break;
                // The event notification indicating the total size of the file to be uploaded, in bytes. This event is supported only in the upload of on-premises files.
                case REQUEST_CONTENT_LENGTH_EVENT:
                    this.totalBytes = bytes;
                    System.out.println(this.totalBytes   "bytes in total will be uploaded to OSS.");
                    break;
                // The event notification indicating the size of uploaded parts, in bytes.
                case REQUEST_BYTE_TRANSFER_EVENT:
                    this.bytesWritten  = bytes;
                    if (this.totalBytes ! = -1) {
                        int percent = (int) (this.bytesWritten * 100.0 / this.totalBytes);
                        System.out.println(bytes   " bytes have been written at this time, upload progress: "  
                                percent   "%("   this.bytesWritten   "/"   this.totalBytes   ")");
                    } else {
                        System.out.println(bytes   " bytes have been written at this time, upload sub total : "  
                                "("   this.bytesWritten   ")");
                    }
                    break;
                // The event notification indicating that all files have been uploaded.
                case TRANSFER_COMPLETED_EVENT:
                    this.succeed = true;
                    if (videoId ! = null) {
                        System.out.println("Succeed to upload videoId "   videoId   " , "   this.bytesWritten   " bytes have been transferred in total.");
                    }
                    if (imageId ! = null) {
                        System.out.println("Succeed to upload imageId "   imageId   " , "   this.bytesWritten   " bytes have been transferred in total.");
                    }
                    break;
                // The event notification indicating that the upload fails.
                case TRANSFER_FAILED_EVENT:
                    if (videoId ! = null) {
                        System.out.println("Failed to upload videoId "   videoId   " , "   this.bytesWritten   " bytes have been transferred.");
                    }
                    if (imageId ! = null) {
                        System.out.println("Failed to upload imageId "   imageId   " , "   this.bytesWritten   " bytes have been transferred.");
                    }
                    break;
    
                default:
                    break;
            }
        }
    
        public boolean isSucceed() {
            return succeed;
        }
    
        public void onVidReady(String videoId) {
            setVideoId(videoId);
        }
    
        public void onImageIdReady(String imageId) {
            setImageId(imageId);
        }
    
        public String getVideoId() {
            return videoId;
        }
    
        public void setVideoId(String videoId) {
            this.videoId = videoId;
        }
    
        public String getImageId() {
            return imageId;
        }
    
        public void setImageId(String imageId) {
            this.imageId = imageId;
        }
    }
    ```


