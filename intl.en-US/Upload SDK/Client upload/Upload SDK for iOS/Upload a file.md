# Upload a file

This topic shows you how to use the upload SDK for iOS to upload a file.

## Procedure

1.  Request an upload URL and an upload credential or a Security Token Service \(STS\) token.

    **Note:** The `VODUploadClient` file upload object allows you upload files to ApsaraVideo VOD by using upload URLs and credentials or STS tokens. We recommend that you use upload URLs and credentials.

    -   Request an upload URL and an upload credential

        You must call different API operations to obtain the upload URLs and credentials for images and videos.

        -   Upload a video: The client sends an upload request to the AppServer. The AppServer calls the `CreateUploadVideo` operation to send a request to ApsaraVideo VOD to obtain an upload URL and an upload credential. If the request succeeds, the AppServer receives the upload URL, upload credential, and the VideoId parameter, and returns them to the client.
        -   Upload an image: The client sends an upload request to the AppServer. The AppServer calls the `CreateUploadImage` operation to send a request to ApsaraVideo VOD to obtain an upload URL and an upload credential. If the request succeeds, the AppServer receives the upload URL, upload credential, and the ImageURL parameter, and returns them to the client.
    -   Request an STS token

        The client sends an upload request to the AppServer. The AppServer sends a request to STS to obtain a temporary STS token. If the request succeeds, the AppServer receives the STS token and returns it to the client.

2.  Initialize an upload instance.

    1.  Declare a `VODUploadClient` object, which cannot be a local variable.

        ```
        @property (nonatomic, strong) VODUploadClient *uploader;
        ```

    2.  Initialize the upload instance by using one of the following methods:

        -   Use the upload URL and credential

            If you use the upload URL and credential, call the `init` method to initialize the upload instance.

            You do not need to specify the obtained upload URL and credential during initialization. Instead, specify them in the SDK by calling the `setUploadAuthAndAddress: uploadAuth:uploadAddress:` method in the `OnUploadStartedListener` callback that is fired when the upload starts.

            When the upload credential expires, the `OnUploadTokenExpiredListener` callback is fired. To resume the upload by using a new upload credential, call the `resumeWithAuth` method.

            ```
            //create VODUploadClient object
            self.uploader = [VODUploadClient new];
            //weakself
            __weak typeof(self) weakSelf = self;
            //setup callback
            OnUploadFinishedListener FinishCallbackFunc = ^(UploadFileInfo* fileInfo, VodUploadResult* result){
                NSLog(@&amp;quot;upload finished callback videoid:%@, imageurl:%@&amp;quot;, result.videoId, result.imageUrl);
            };
            OnUploadFailedListener FailedCallbackFunc = ^(UploadFileInfo* fileInfo, NSString *code, NSString* message){
                NSLog(@&amp;quot;upload failed callback code = %@, error message = %@&amp;quot;, code, message);
            };
            OnUploadProgressListener ProgressCallbackFunc = ^(UploadFileInfo* fileInfo, long uploadedSize, long totalSize) {
                NSLog(@&amp;quot;upload progress callback uploadedSize : %li, totalSize : %li&amp;quot;, uploadedSize, totalSize);
            };
            OnUploadTokenExpiredListener TokenExpiredCallbackFunc = ^{
                NSLog(@&amp;quot;upload token expired callback.&amp;quot;);
                // Specify a new upload credential to resume the upload upon credential expiration.
                [weakSelf.uploader resumeWithAuth:`new upload auth`];
            };
            OnUploadRertyListener RetryCallbackFunc = ^{
                NSLog(@&amp;quot;upload retry begin callback.&amp;quot;);
            };
            OnUploadRertyResumeListener RetryResumeCallbackFunc = ^{
                NSLog(@&amp;quot;upload retry end callback.&amp;quot;);
            };
            OnUploadStartedListener UploadStartedCallbackFunc = ^(UploadFileInfo* fileInfo) {
                NSLog(@&amp;quot;upload upload started callback.&amp;quot;);
                // Specify the upload URL and credential.
                [weakSelf.uploader setUploadAuthAndAddress:fileInfo uploadAuth:`upload auth` uploadAddress:`upload address`];
            };
            VODUploadListener *listener = [[VODUploadListener alloc] init];
            listener.finish = FinishCallbackFunc;
            listener.failure = FailedCallbackFunc;
            listener.progress = ProgressCallbackFunc;
            listener.expire = TokenExpiredCallbackFunc;
            listener.retry = RetryCallbackFunc;
            listener.retryResume = RetryResumeCallbackFunc;
            listener.started = UploadStartedCallbackFunc;
            //init with upload address and upload auth
            [self.uploader init:listener];
            ```

        -   Use the STS token

            If you use an STS token to upload a file to ApsaraVideo VOD, call the `init: accessKeySecret: secretToken: expireTime: listener` method to initialize the upload instance. Use the obtained temporary STS token as the initialization parameter.

            When the STS token expires, the `OnUploadTokenExpiredListener` callback is fired. To resume the upload by using a new STS token, call the `resumeWithToken: accessKeySecret: secretToken: expireTime` method.

            ```
            //create VODUploadClient object
            self.uploader = [VODUploadClient new];
            //weakself
            __weak typeof(self) weakSelf = self;
            //setup callback
            OnUploadFinishedListener FinishCallbackFunc = ^(UploadFileInfo* fileInfo,  VodUploadResult* result){
                NSLog(@&amp;quot;upload finished callback videoid:%@, imageurl:%@&amp;quot;, result.videoId, result.imageUrl);
            };
            OnUploadFailedListener FailedCallbackFunc = ^(UploadFileInfo* fileInfo, NSString *code, NSString* message){
                NSLog(@&amp;quot;upload failed callback code = %@, error message = %@&amp;quot;, code, message);
            };
            OnUploadProgressListener ProgressCallbackFunc = ^(UploadFileInfo* fileInfo, long uploadedSize, long totalSize) {
                NSLog(@&amp;quot;upload progress callback uploadedSize : %li, totalSize : %li&amp;quot;, uploadedSize, totalSize);
            };
            OnUploadTokenExpiredListener TokenExpiredCallbackFunc = ^{
                NSLog(@&amp;quot;upload token expired callback.&amp;quot;);
                // Specify a new STS token to resume the upload upon credential expiration.
                [weakSelf.uploader resumeWithToken:`STS Key Id` accessKeySecret:`STS Key Secret` secretToken:`STS Secret Token` expireTime:`STS Expire Time`];
            };
            OnUploadRertyListener RetryCallbackFunc = ^{
                NSLog(@&amp;quot;upload retry begin callback.&amp;quot;);
            };
            OnUploadRertyResumeListener RetryResumeCallbackFunc = ^{
                NSLog(@&amp;quot;upload retry end callback.&amp;quot;);
            };
            OnUploadStartedListener UploadStartedCallbackFunc = ^(UploadFileInfo* fileInfo) {
                NSLog(@&amp;quot;upload upload started callback.&amp;quot;);
            };
            //init
            VODUploadListener *listener = [[VODUploadListener alloc] init];
            listener.finish = FinishCallbackFunc;
            listener.failure = FailedCallbackFunc;
            listener.progress = ProgressCallbackFunc;
            listener.expire = TokenExpiredCallbackFunc;
            listener.retry = RetryCallbackFunc;
            listener.retryResume = RetryResumeCallbackFunc;
            listener.started = UploadStartedCallbackFunc;
            //init with STS
            [self.uploader init:`STS Key Id` accessKeySecret:`STS Key Secret` secretToken:STS Secret Token` expireTime:`STS Expire Time` listener:listener];
            ```

3.  Set callbacks.

    Set the `VODUploadListener` object, which belongs to the class of callbacks for upload statuses. You must set the following callbacks:

    ```
    /**
     This callback is fired when the upload succeeds.
     @param fileInfo The information about the file that you upload.
     @param result The upload result.
     */
    typedef void (^OnUploadFinishedListener) (UploadFileInfo* fileInfo, VodUploadResult* result);
    /**
     This callback is fired when the upload fails.
     @param fileInfo The information about the file that you upload.
     @param code The error code.
     @param message The error message.
     */
    typedef void (^OnUploadFailedListener) (UploadFileInfo* fileInfo, NSString *code, NSString * message);
    /**
     This callback is fired when the default or custom upload progress is reached.
     @param fileInfo The information about the file that you upload.
     @param uploadedSize The size of uploaded parts.
     @param totalSize The total size of the file that you upload.
     */
    typedef void (^OnUploadProgressListener) (UploadFileInfo* fileInfo, long uploadedSize, long totalSize);
    /**
     This callback is fired when the upload credential or STS token expires.
     If you use the upload URL and credential to upload a file, call the resumeWithAuth: method to resume the upload.
     If you use an STS token to upload a file, call the resumeWithToken:accessKeySecret:secretToken:expireTime: method to resume the upload.
     */
    typedef void (^OnUploadTokenExpiredListener) ();
    /**
     This callback is fired when the system retries the upload.
     */
    typedef void (^OnUploadRertyListener) ();
    /**
     This callback is fired when the system resumes the upload after the upload retry is complete.
     */
    typedef void (^OnUploadRertyResumeListener) ();
    /**
     This callback is fired when the upload starts.
     If you use the upload URL and credential to upload a file, call the setUploadAuthAndAddress:uploadAuth:uploadAddress: method to specify the upload URL and credential.
     @param fileInfo The information about the file that you upload.
     */
    typedef void (^OnUploadStartedListener) (UploadFileInfo* fileInfo);
    ```

4.  Add a file to the upload list.

    -   Add a file

        -   Add a video

            ```
            NSString *filePath = [[NSBundle mainBundle] pathForResource:@&amp;quot;test&amp;quot; ofType:@&amp;quot;mp4&amp;quot;];
            VodInfo *vodInfo = [[VodInfo alloc] init];
            vodInfo.title = @&amp;quot;title&amp;quot;;
            vodInfo.desc =@&amp;quot;desc&amp;quot;;
            vodInfo.cateId = @(19);
            vodInfo.tags = @&amp;quot;sports&amp;quot;;
            [self.uploader addFile:filePath vodInfo:vodInfo];
            ```

        -   Add an image

            ```
            NSString *filePath = [[NSBundle mainBundle] pathForResource:@&amp;quot;test&amp;quot; ofType:@&amp;quot;jpg&amp;quot;];
            VodInfo *imageInfo = [[VodInfo alloc] init];
            imageInfo.title = @&amp;quot;title&amp;quot;;
            imageInfo.desc =@&amp;quot;desc&amp;quot;;
            imageInfo.cateId = @(19);
            imageInfo.tags = @&amp;quot;sports&amp;quot;;
            [self.uploader addFile:filePath vodInfo:imageInfo];
            ```

        **Note:** The size of the file to be uploaded cannot exceed 4 GB.

        The VodInfo object has the following structure:

        ```
        // The title.
        @property (nonatomic, copy) NSString* title;
        // The tags.
        @property (nonatomic, copy) NSString* tags;
        // The description.
        @property (nonatomic, copy) NSString* desc;
        // The category ID.
        @property (nonatomic, strong) NSNumber* cateId;
        // The URL of the thumbnail. The value must be a complete URL that starts with https://.
        @property (nonatomic, copy) NSString* coverUrl;
        ```

        After you add a file to be uploaded, the SDK encapsulates the file in `UploadFileInfo` object that has the following structure:

        ```
        // The on-premises path of the file.
        @property (nonatomic, copy) NSString* filePath;
        //endpoint
        @property (nonatomic, copy) NSString* endpoint;
        //bucket
        @property (nonatomic, copy) NSString* bucket;
        //object
        @property (nonatomic, copy) NSString* object;
        //VodInfo
        @property (nonatomic, strong) VodInfo* vodInfo;
        ```

    -   Manage the upload list

        The `VODUploadClient` allows you to add multiple files to upload them in sequence. You can use the following methods to manage the upload list:

        **Note:** The `VODUploadClient` object allows you to upload multiple files. However, if you use upload URLs and credentials to upload media files, you must separately set the configuration for each file. The code for uploading multiple files at a time is complex. Therefore, we recommend that you add a single file to the upload list at a time.

        -   Remove a file from the upload list. If the file to be removed is being uploaded, the system cancels the upload and automatically starts to upload the next file in the list.

            ```
            - (BOOL)deleteFile:(int) index;
            ```

        -   Clear the upload list. If the upload list to be cleared contains a file that is being uploaded, the system cancels the upload.

            ```
            - (BOOL)clearFiles;
            ```

        -   Query the upload list.

            ```
            - (NSMutableArray&amp;lt;UploadFileInfo *&amp;gt; *)listFiles;
            ```

        -   Mark a file in the upload list as canceled without removing it from the upload list. If the file to be canceled is being uploaded, the system cancels the upload and automatically starts to upload the next file in the list.

            ```
            - (BOOL)cancelFile:(int)index;
            ```

        -   Resume a canceled file and automatically start to upload the file.

            ```
            - (BOOL)resumeFile:(int)index;
            ```

5.  Control the upload.

    -   Start the upload.

        ```
        [self.uploader start];
        ```

        When this method is called, the `OnUploadStartedListener` callback is fired. If you use an upload URL and an upload credential to upload a file, specify the upload URL and credential in this callback, as shown in the following code:

        ```
        [weakSelf.uploader setUploadAuthAndAddress:fileInfo uploadAuth:weakSelf.uploadAuth uploadAddress:weakSelf.uploadAddress];
        ```

    -   Stop the upload. If a file is being uploaded, the system cancels the upload.

        ```
        - (BOOL)stop;
        ```

        **Note:** If you need to resume the upload after you stop the upload, call the `resumeFile:` method to resume the file to be uploaded. Alternatively, clear the upload list and add the file again to upload it.

    -   Pause the upload.

        ```
        - (BOOL)pause;
        ```

    -   Resume the upload.

        ```
        - (BOOL)resume;
        ```

6.  Handle callbacks.

    -   Upload progress

        The `OnUploadProgressListener` callback is fired each time a part is uploaded. The callback parameters include `uploadedSize` and `totalSize`. The uploadedSize parameter indicates the size of uploaded parts, and the totalSize parameter indicates the total size of the file that you upload.

    -   Upload success

        The `OnUploadFinishedListener` callback is fired when the upload succeeds. The callback parameter includes `UploadFileInfo` and `VodUploadResult`, which indicate the information about the file that you upload and the upload result. The `VodUploadResult` contains the following attributes:

        ```
        @property (nonatomic, copy) NSString* videoId;
        @property (nonatomic, copy) NSString* imageUrl;
        ```

        **Note:** The `videoId` or `imageUr` parameter is returned only when a video or an image is uploaded to ApsaraVideo VOD by using an STS token. If you use an upload URL and an upload credential to upload a video or an image, the `videoId` or `imageUrl` parameter is not returned. You can obtain the parameter value when you request an upload URL and an upload credential.

        After a video is uploaded, the videoId parameter is returned, which indicates the video ID. Then, you must obtain the streaming URL to play the video. For more information, see [Obtain playback URLs to play videos](/intl.en-US/Developer Guide/Video play/Obtain playback URLs to play videos.md).

        After an image is uploaded, the imageUrl parameter is returned, which indicates the image URL. If URL signing is enabled, the image URL expires after a specific period of time. For more information, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md).

    -   Upload failure

        The `OnUploadFailedListener` callback is fired when the upload fails. You can view the cause of the failure based on the `code` and `message` callback parameters. In addition, a prompt is displayed on the web page. For more information about error codes, see [t1235485.md\#](/intl.en-US/API Reference/Error codes.md) and [Handle exceptions](/intl.en-US/SDK Reference/iOS/Handle exceptions.md).

    -   Credential or token expiration

        The `OnUploadTokenExpiredListener` callback is fired when the upload credential or STS token expires. You can send a request to the AppServer to obtain a new upload credential or STS token, and call the following method to resume the upload:

        -   Specify a new upload credential

            ```
            - (BOOL)resumeWithAuth:(NSString *)uploadAuth;
            ```

        -   Specify a new STS token

            ```
            - (BOOL)resumeWithToken:(NSString *)accessKeyId
                    accessKeySecret:(NSString *)accessKeySecret
                        secretToken:(NSString *)secretToken
                         expireTime:(NSString *)expireTime;
            ```

    -   Upload timeout

        When the upload times out, the `OnUploadRertyListener` callback is fired and the system automatically retries to upload the file. You can receive a prompt on the web page or call the `stop` method to stop the upload. In addition, you can set the `maxRetryCount` parameter to specify the maximum number of retries. If the retry result indicates that the upload can be resumed, the `OnUploadRertyResumeListener` callback is fired and the upload is resumed.


## Advanced settings

The `VODUploadClient` object supports the following advanced settings:

```
/**
 Specify whether to transcode a file after it is uploaded to ApsaraVideo VOD. Default value: YES.
 */
@property (nonatomic, assign) BOOL transcode;
/**
 Specify the maximum number of timeout retries allowed. Default value: INT_MAX.
 */
@property (nonatomic, assign) uint32_t maxRetryCount;
/**
 Specify the timeout period.
 */
@property (nonatomic, assign) NSTimeInterval timeoutIntervalForRequest;
/**
 Specify the path of the directory where cached data is stored.
 */
@property (nonatomic, copy) NSString * recordDirectoryPath;
/**
 Specify whether to record the upload progress for a resumable upload. Default value: YES.
 */
@property (nonatomic, assign) BOOL recordUploadProgress;
/**
 Specify the size of each part in multipart upload. Default value: 1024 × 1024.
*/
@property (nonatomic, assign) NSInteger uploadPartSize;
/**
 Specify the region of the ApsaraVideo VOD service. Default value: &amp;quot;cn-shanghai&amp;quot;.
 */
@property (nonatomic, copy) NSString *region;
```

