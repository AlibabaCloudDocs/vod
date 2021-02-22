Upload a file 
==================================

This topic shows you how to use the upload SDK for Android to upload a file.

Procedure 
------------------------------

1. Request an upload URL and an upload credential or a Security Token Service (STS) token.

   **Note**

   The `VODUploadClient` object allows you to upload media files by using the upload URL and credential or the STS token. We recommend that you use the upload URL and credential.

   * Request an upload URL and an upload credential

     You must call different API operations to obtain the upload URLs and credentials for images and videos.

     Upload a video: The client sends an upload request to the AppServer. The AppServer calls the CreateUploadVideo operation to send a request to ApsaraVideo VOD. If the request succeeds, the AppServer receives the upload URL, upload credential, and the VideoId parameter, and returns them to the client.

     Upload an image: The client sends an upload request to the AppServer. The AppServer calls the CreateUploadImage operation to send a request to ApsaraVideo VOD. If the request succeeds, the AppServer receives the upload URL, upload credential, and the ImageURL parameter, and returns them to the client.
     
   
   * Request an STS token

     The client sends an upload request to the AppServer. The AppServer sends a request to STS to obtain a temporary STS token. If the request succeeds, the AppServer receives the STS token and returns it to the client.
     
   

   

2. Initialize an upload instance.

   1. Declare a `VODUploadClient` initialization callback.

          uploader = new VODUploadClientImpl(getApplicationContext());

      
   
   2. Initialize the upload instance by using one of the following methods:

      * Use the upload URL and credential

        If you use an upload URL and an upload credential to upload a file, call the `init` method for initialization.

        You do not need to specify the obtained upload URL and credential during initialization. Instead, specify them in the SDK by calling the `setUploadAuthAndAddress(uploadFileInfo, uploadAuth, uploadAddress)` method in the `onUploadStarted` callback that is fired when the upload starts.

        When the credential expires, the `onUploadTokenExpired` callback is fired. Call the `resumeWithAuth(uploadAuth)` method to resume the upload by using a new upload credential.

            // create VODUploadClient
            final VODUploadClient uploader = new VODUploadClientImpl(getApplicationContext());
            // setup callback
            VODUploadCallback callback = new VODUploadCallback() {
                        public void onUploadSucceed(UploadFileInfo info) {
                            OSSLog.logDebug("onsucceed ------------------" + info.getFilePath());
                        }
                        public void onUploadFailed(UploadFileInfo info, String code, String message) {
                            OSSLog.logError("onfailed ------------------ " + info.getFilePath() + " " + code + " " + message);
                        }
                        public void onUploadProgress(UploadFileInfo info, long uploadedSize, long totalSize) {
                            OSSLog.logDebug("onProgress ------------------ " + info.getFilePath() + " " + uploadedSize + " " + totalSize);
                                }
                            }
                        }
                        public void onUploadTokenExpired() {
                            OSSLog.logError("onExpired ------------- ");
                                // Call the RefreshUploadVideo operation to update the upload credential.
                                uploadAuth = "The new upload credential";
                                uploader.resumeWithAuth(uploadAuth);
                        }
                        public void onUploadRetry(String code, String message) {
                            OSSLog.logError("onUploadRetry ------------- ");
                        }
                        public void onUploadRetryResume() {
                            OSSLog.logError("onUploadRetryResume ------------- ");
                        }
                        public void onUploadStarted(UploadFileInfo uploadFileInfo) {
                            OSSLog.logError("onUploadStarted ------------- ");
                            uploader.setUploadAuthAndAddress(uploadFileInfo, uploadAuth, uploadAddress);
                        }
                    };
            // Initialize the upload instance.
            uploader.init(callback);

        
      
      * Use the STS token

        If you use STS tokens to upload media files, call the `init(accessKeyId, accessKeySecret, secretToken, expireTime, callback)` method for initialization. Use the obtained temporary STS token as the initialization parameter.

        When the STS token expires, the `OnUploadTokenExpired` callback is fired. Call the `resumeWithToken(accessKeyId, accessKeySecret, secretToken, expireTime)` method to resume the upload by using a new STS token.

            // create VODUploadClient object
            uploader = new VODUploadClientImpl(getApplicationContext());
            // setup callback
            // setup callback
            VODUploadCallback callback = new VODUploadCallback() {
                        public void onUploadSucceed(UploadFileInfo info) {
                            OSSLog.logDebug("onsucceed ------------------" + info.getFilePath());
                        }
                        public void onUploadFailed(UploadFileInfo info, String code, String message) {
                            OSSLog.logError("onfailed ------------------ " + info.getFilePath() + " " + code + " " + message);
                        }
                        public void onUploadProgress(UploadFileInfo info, long uploadedSize, long totalSize) {
                            OSSLog.logDebug("onProgress ------------------ " + info.getFilePath() + " " + uploadedSize + " " + totalSize);
                                }
                            }
                        }
                        public void onUploadTokenExpired() {
                            OSSLog.logError("onExpired ------------- ");
                                // Call the resumeWithToken method after a new STS token is obtained.
                                uploader.resumeWithToken(accessKeyId, accessKeySecret, secretToken, expireTime);
                        }
                        public void onUploadRetry(String code, String message) {
                            OSSLog.logError("onUploadRetry ------------- ");
                        }
                        public void onUploadRetryResume() {
                            OSSLog.logError("onUploadRetryResume ------------- ");
                        }
                        public void onUploadStarted(UploadFileInfo uploadFileInfo) {
                            OSSLog.logError("onUploadStarted ------------- ");
                        }
                    };
            // Initialize the upload instance. When the STS token expires, the onUploadTokenExpired callback is fired. Call the resumeWithToken method to resume the upload by using a new STS token. By default, resumable upload is supported.
            uploader.init(accessKeyId, accessKeySecret, secretToken, expireTime, callback);

        
      

      
   

   

3. Set callbacks.

   Set the `VODUploadCallback` object. This object belongs to the class of callbacks for upload statuses. You must set the following callbacks:

       /**
        This callback is fired when the upload succeeds.
        @param info The information about the file that you upload.
        */
       void onUploadSucceed(UploadFileInfo info);
       /**
        This callback is fired when the upload fails.
        @param info The information about the file that you upload.
        @param code The error code.
        @param message The error message.
        */
        void onUploadFailed(UploadFileInfo info, String code, String message);
       /**
        This callback is fired when the default or custom upload progress is reached.
        @param fileInfo The information about the file that you upload.
        @param uploadedSize The size of uploaded parts.
        @param totalSize The total size of the file that you upload.
        */
        void onUploadProgress(UploadFileInfo info, long uploadedSize, long totalSize);
       /**
        This callback is fired when the upload credential or STS token expires.
        If you use the upload URL and credential to upload a file, call the resumeWithAuth method to resume the upload.
        If you use STS tokens to upload media files, call the resumeWithToken method to resume the upload.
        */
        void onUploadTokenExpired();
       /**
        This callback is fired when the system retries the upload.
        */
        void onUploadRetry(String code, String message);
       /**
        This callback is fired when the system resumes the upload after the upload retry is complete.
        */
        void onUploadRetryResume ();
       /**
        This callback is fired when the upload starts.
        If you use the upload URL and credential to upload a file, call the setUploadAuthAndAddress:uploadAuth:uploadAddress: method to specify the upload URL and credential.
        @param fileInfo The information about the file that you upload.
        */
         void onUploadStarted(UploadFileInfo uploadFileInfo);

   

4. Add a file to the upload list.

   * Add a file

     * Add a video

           String filePath = "The path of the video";
           VodInfo vodInfo = new VodInfo();
           vodInfo.setTitle("The title" + index);
           vodInfo.setDesc("The description" + index);
           vodInfo.cateId (19);
           vodInfo.tags("sports");
           uploader.addFile(filePath,vodInfo);

       
     
     * Add an image

           javaString filePath = "The path of the image";
           VodInfo vodInfo = new VodInfo();
           vodInfo.setTitle("The title" + index);
           vodInfo.setDesc("The description" + index);
           vodInfo.cateId (19);
           vodInfo.tags("sports");
           uploader.addFile(filePath,vodInfo);

       
     

     
     **Note**

     The size of the file to be uploaded cannot exceed 4 GB.

     The VodInfo object has the following structure:

     

         // The title.
         String title;
         // The tags.
         List tags;
         // The description.
         String desc;
         // The category ID.
         idInteger cateId;
         // The URL of the thumbnail. The value must be a complete URL that starts with https://.
         String coverUrl;

     

     After you add a file to be uploaded, the SDK encapsulates the file in `UploadFileInfo` object that has the following structure:

     

         // The on-premises path of the file.
         String filePath;
         //endpoint
         String endpoint;
         //bucket
         String bucket;
         //object
         String object;
         //VodInfo
         VodInfo vodInfo;

     

     
   
   * Manage the upload list

     The `VODUploadClient` object allows you to add multiple files to upload them in sequence. You can use the following methods to manage the upload list:
     **Note**

     The `VODUploadClient` object allows you to upload multiple files. However, if you use the upload URL and credential to upload files, you must specify an upload URL and an upload credential for each file. The code for uploading multiple files at a time is complex. Therefore, we recommend that you add a single file to the upload list at a time.
     * Remove a file from the upload list. If the file to be removed is being uploaded, the system cancels the upload and automatically starts to upload the next file in the list.

           void deleteFile(int index)

       
     
     * Clear the upload list. If the upload list to be cleared contains a file that is being uploaded, the system cancels the upload.

           void clearFiles()

       
     
     * Query the upload list.

           List<UploadFileInfo> listFiles()

       
     
     * Mark a file in the upload list as canceled without removing it from the upload list. If the file to be canceled is being uploaded, the system cancels the upload and automatically starts to upload the next file in the list.

           cancelFile(int index)

       
     
     * Resume a canceled file and automatically start to upload the file.

           resumeFile(int index)

       
     

     
   

   

5. Control the upload.

   * Start the upload.

         void start();

     

     When this method is called, the `onUploadStarted` callback is fired. If you use the upload URL and credential to upload a file, specify the upload URL and credential in this callback, as shown in the following code:

     

         void setUploadAuthAndAddress(UploadFileInfo uploadFileInfo, String uploadAuth, String uploadAddress)

     

     
   
   * Stop the upload. If a file is being uploaded, the system cancels the upload.

         void stop();

     
     **Note**

     If you need to resume the upload after you stop the upload, call the `resumeFile` method to resume the file to be uploaded. Alternatively, clear the upload list and add the file again to upload it.
     
   
   * Pause the upload.

         void pause();

     
   
   * Resume the upload.

         void resume();

     
   

   

6. Handle callbacks.

   * Upload progress

     The `onUploadProgress` callback is fired each time a part is uploaded. The callback parameters include `uploadedSize` and `totalSize`. The value of the uploadedSize parameter indicates the size of uploaded parts. The value of the totalSize parameter indicates the total size of the file that you upload.
     
   
   * Upload success

     The `onUploadSucceed` callback is fired when the upload succeeds. The callback parameter includes `videoId` or `imageUrl`.
     **Note**
     * After a video is uploaded, the videoId parameter is returned, which indicates the video ID. Then, you must obtain the streaming URL to play the video. For more information, see [Use playback credentials to play videos](/intl.en-US/Developer Guide/Video play/Use playback credentials to play videos.md).

       
     
     * After an image is uploaded, the imageUrl parameter is returned, which indicates the image URL. If URL signing is enabled, the image URL expires after a specific period of time. For more information, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md).

       
     

     
     
   
   * Upload failure

     The `onUploadFailed` callback is fired when the upload fails. You can view the cause of the failure based on the `code` and `message` callback parameters. In addition, a prompt is displayed on the web page. For more information about error codes, see [Error codes](/intl.en-US/API Reference/Error codes.md) and [Handle exceptions](/intl.en-US/SDK Reference/iOS/Handle exceptions.md).
     
   
   * Credential or token expiration

     The `onSTSTokenExpried` callback is fired when the upload credential or STS token expires. You can send a request to the AppServer to obtain a new upload credential or STS token and call the following method to resume the upload:

     

         refreshSTSToken(accessKeyId,accessKeySecret,securityToken,expriedTime);

     

     
   
   * Upload timeout

     When the upload times out, the `uploadRetry` callback is fired and the system automatically retries to upload files. You can receive a prompt on the web page or call the `cancelFile(int index)` method to cancel the upload. In addition, you can set the `maxRetryCount` parameter to specify the maximum number of retries. If the retry result indicates that the upload can be resumed, the `uploadRetryResume` callback is fired and the upload is resumed.
     
   

   






Advanced settings 
--------------------------------------

The `VODUploadClient` object supports the following advanced settings:

    /**
     Specify whether to transcode a file after it is uploaded to ApsaraVideo VOD. Default value: YES.
     */
    void setTranscodeMode(boolean bool);
    /**
     Specify the size of each part in multipart upload. Default value: 1024 × 1024.
    */
    void setPartSize(long partSize);
    /**
    * Specify the storage location for videos.
    */
    void setStorageLocation(String storageLocation);
    /**
    * Specify the ID of the transcoding template group.
    */
    void setTemplateGroupId(String templateGroupId);



