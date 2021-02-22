# Upload a short video

This topic shows you how to use the upload SDK for Android to upload a short video.

## Procedure

1.  Request a Security Token Service \(STS\) token. For more information, see [Use STS tokens to upload media files](/intl.en-US/Upload SDK/Upload from clients/Use STS.md).

    **Note:** The VODSVideoUploadClient object allows you to upload media files only by using STS. If you need to upload a short video to ApsaraVideo VOD by using the upload URL and credential, use the `VODUploadClient` object to upload the thumbnail and video.

2.  Initialize an upload instance.

    1.  Declare a `VODSVideoUploadClient` object. It must not be a local variable.

        ```
        // Initialize the VODSVideoUploadClient object.
        VODSVideoUploadClient vodsVideoUploadClient = new VODSVideoUploadClientImpl(this.getApplicationContext());
        vodsVideoUploadClient.init();
        ```

    2.  Construct upload parameters.

        ```
        // Construct upload parameters.
        // Make sure that the parameter settings are valid. Otherwise, an exception is thrown in the SDK.
        // Make sure that the path of the file to be uploaded is valid. In addition, you must obtain the read and write permissions on the file because sensitive permissions need to be dynamically requested in Android 6.0 or later.
        VodHttpClientConfig vodHttpClientConfig = new VodHttpClientConfig.Builder()
                .setMaxRetryCount(2)// Specify the maximum number of retries.
                .setConnectionTimeout(15 * 1000)// Specify the connection timeout period.
                .setSocketTimeout(15 * 1000)// Specify the timeout period for the socket connection.
                .build();
         // Construct the information about the short video, including the description, title, and details.
         SvideoInfo svideoInfo = new SvideoInfo();
         svideoInfo.setTitle(new File(videoPath).getName());// Specify the title.
         svideoInfo.setDesc("");// Specify the description.
         svideoInfo.setCateId(1);// Specify the category ID.
         // Construct parameters for uploading the short video to ApsaraVideo VOD. This step is important.
         VodSessionCreateInfo vodSessionCreateInfo =new    VodSessionCreateInfo.Builder()
        .setImagePath(imagePath)// Specify the path of the thumbnail.
        .setVideoPath(videoPath)// Specify the path of the video.
        .setAccessKeyId(accessKeyId)// Specify a temporary AccessKey ID.
        .setAccessKeySecret(accessKeySecret)// Specify a temporary AccessKey secret.
        .setSecurityToken(securityToken)//securityToken
        .setExpriedTime(expriedTime)// Specify the expiration time for the STS token.
        .setRequestID(requestID)// Specify the request ID. You can choose whether to obtain the request ID returned by STS.
        .setIsTranscode(true)// Specify whether to enable transcoding. If transcoding is enabled, you must register a listener on the AppServer to receive notifications when transcoding is successful on the ApsaraVideo VOD server.
        .setSvideoInfo(svideoInfo)// Specify the information about the short video.
        .setVodHttpClientConfig(vodHttpClientConfig)// Specify network parameters.
                                .build();
        ```

3.  Set callbacks.

    You must set the `VODSVideoUploadCallback` callback to start the upload.

    ```
    vodsVideoUploadClient.uploadWithVideoAndImg(vodSessionCreateInfo, new VODSVideoUploadCallback() {
                        @Override
                        public void onUploadSucceed(String videoId, String imageUrl) {
                        // This callback is fired when the upload succeeds. The video ID and image URL are returned.
                        Log.d(TAG,"onUploadSucceed"+ "videoId:"+ videoId + "imageUrl" + imageUrl);
                        }
                        @Override
                        public void onUploadFailed(String code, String message) {
                            // This callback is fired when the upload fails. The error code and error message are returned. You must carefully read the error code and error message.
                            Log.d(TAG,"onUploadFailed" + "code" + code + "message" + message);
                        }
                        @Override
                        public void onUploadProgress(long uploadedSize, long totalSize) {
                            // This callback is fired when the default or custom upload progress is reached. The current thread is not a UI thread.
                            Log.d(TAG,"onUploadProgress" + uploadedSize * 100 / totalSize);
                            progress = uploadedSize * 100 / totalSize;
                            handler.sendEmptyMessage(0);
                        }
                        @Override
                        public void onSTSTokenExpried() {
                            Log.d(TAG,"onSTSTokenExpried");
                            // This callback is fired when the STS token expires. If the file is being uploaded when the STS token expires, resumable upload is performed after the STS token is updated.
                            vodsVideoUploadClient.refreshSTSToken(accessKeyId,accessKeySecret,securityToken,expriedTime);
                        }
                        @Override
                        public void onUploadRetry(String code, String message) {
                            // This callback is fired when the system retries the upload.
                            Log.d(TAG,"onUploadRetry" + "code" + code + "message" + message);
                        }
                        @Override
                        public void onUploadRetryResume() {
                            // This callback is fired when the upload retry succeeds and the system resumes the upload. You are notified of the successful retry.
                            Log.d(TAG,"onUploadRetryResume");
                        }
                    });
    ```

4.  Start the upload.

    You can call the following methods to control the upload:

    -   Pause the upload.

        ```
        // This method must be set in pairs with the vodsVideoUploadClient.resume() method.
        vodsVideoUploadClient.pause();
        ```

    -   Resume the upload.

        ```
        // This method must be set in pairs with the vodsVideoUploadClient.pause() method.
        vodsVideoUploadClient.resume();
        ```

    -   Cancel the upload.

        ```
        // If you cancel the upload, the upload process ends and you cannot call the vodsVideoUploadClient.resume() method to resume the upload.
        vodsVideoUploadClient.cancel();
        ```

5.  Handle callbacks.

    -   Upload progress

        The `onUploadProgress` callback is fired each time a part is uploaded. The callback parameters include `uploadedSize` and `totalSize`. The value of the uploadedSize parameter indicates the size of uploaded parts. The value of the totalSize parameter indicates the total size of the file that you upload.

    -   Upload success

        The `onUploadSucceed` callback is fired when the upload succeeds. The callback parameters include `videoId` and `imageUrl`.

        **Note:**

        -   After a video is uploaded, the videoId parameter is returned, which indicates the video ID. Then, you must obtain the streaming URL to play the video. For more information, see [Obtain playback URLs to play videos](/intl.en-US/Developer Guide/Video play/Obtain playback URLs to play videos.md).
        -   After an image is uploaded, the imageUrl parameter is returned, which indicates the image URL. If URL signing is enabled, the image URL expires after a specific period of time. For more information, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md).
    -   Upload failure

        The `onUploadFailed` callback is fired when the upload fails. You can view the cause of the failure based on the `code` and `message` callback parameters. In addition, a prompt is displayed on the web page. For more information about error codes, see [t1235485.md\#](/intl.en-US/API Reference/Error codes.md) and [Handle exceptions](/intl.en-US/SDK Reference/iOS/Handle exceptions.md).

    -   Token expiration

        The `uploadTokenExpired` callback is fired when the STS token expires. You can send a request to the AppServer to obtain a new STS token and call the following method to resume the upload:

        ```
        refreshSTSToken(accessKeyId,accessKeySecret,securityToken,expriedTime);
        ```

    -   Upload timeout

        When the upload times out, the `uploadRetry` callback is fired and the system automatically retries to upload files. You can receive a prompt on the web page or call the `vodsVideoUploadClient.cancel()` method to cancel the upload. In addition, you can set the `maxRetryCount` parameter to specify the maximum number of retries. If the retry result indicates that the upload can be resumed, the `uploadRetryResume` callback is fired and the upload is resumed.


