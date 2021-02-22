# Upload a short video

This topic shows you how to use the upload SDK for Android to upload a short video.

## Procedure

1.  Request a Security Token Service \(STS\) token. For more information, see [t1959814.md\#](/intl.en-US/Upload SDK/Client upload/Use STS.md).

    **Note:** The VODSVideoUploadClient object allows you to upload media files only by using STS. If you need to upload a short video to ApsaraVideo VOD by using the upload URL and credential, use the `VODUploadClient` object to upload the thumbnail and video.

2.  Initialize an upload instance.

    1.  Declare a `VODUploadSVideoClient` object, which cannot be a local variable.

        ```
        @property (nonatomic, strong) VODUploadSVideoClient *client;
        ```

    2.  Initialize the upload instance and set the callback for the delegate.

        ```
        self.client = [[VODUploadSVideoClient alloc] init];
        self.client.delegate = self;
        ```

3.  Set callbacks.

    Set the delegate to implement `VODUploadSVideoClientDelegate` by using the following methods:

    ```
    /**
     This callback is fired when the upload succeeds.
     @param result The upload result.
     */
    - (void)uploadSuccessWithResult:(VodSVideoUploadResult *)result;
    /**
     This callback is fired when the upload fails.
     @param code The error code.
     @param message The error message.
     */
    - (void)uploadFailedWithCode:(NSString *)code message:(NSString *)message;
    /**
     This callback is fired when the default or custom upload progress is reached.
     @param uploadedSize The size of the uploaded parts.
     @param totalSize The total size of the short video that you upload.
     */
    - (void)uploadProgressWithUploadedSize:(long long)uploadedSize totalSize:(long long)totalSize;
    /**
     This callback is fired when the upload credential or STS token expires.
     */
    - (void)uploadTokenExpired;
    /**
     This callback is fired when the system retries the upload.
     */
    - (void)uploadRetry;
    /**
     This callback is fired when the system resumes the upload after the upload retry is complete.
     */
    - (void)uploadRetryResume;
    ```

4.  Start the upload.

    Short video upload does not support the upload list feature. You must call the media upload operation to upload each short video. To call the upload method, you must specify the video URL, thumbnail URL, STS token obtained in the first step, and set the VodSVideoInfo parameter.

    ```
    NSString *videoPath = [[NSBundle mainBundle] pathForResource:@"svideo" ofType:@"mp4"];
        NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"cover" ofType:@"png"];
        VodSVideoInfo *info = [VodSVideoInfo new];
        info.title = @"short video";
        info.desc = @"desc";
        info.cateId = @(10);
        info.tags = @"game";
        [self.client uploadWithVideoPath:videoPath imagePath:imagePath svideoInfo:info accessKeyId:self.keyId accessKeySecret:self.keySecret accessToken:self.token];
    ```

    **Note:** The size of the short video to be uploaded cannot exceed 4 GB.

    The VodSVideoInfo object has the following structure:

    ```
    // The title.
    @property (nonatomic, copy) NSString* title;
    // The tags.
    @property (nonatomic, copy) NSString* tags;
    // The description.
    @property (nonatomic, copy) NSString* desc;
    // The category ID.
    @property (nonatomic, strong) NSNumber* cateId;
    ```

    You can call the following methods to control the upload:

    -   Pause the upload.

        ```
        - (void)pause;
        ```

    -   Resume the upload.

        ```
        - (BOOL)resume;
        ```

    -   Cancel the upload.

        ```
        - (BOOL)cancel;
        ```

5.  Handle callbacks.

    -   Upload progress

        The `uploadProgressWithUploadedSize: totalSize:` callback is fired each time a part is uploaded. The callback parameters include `uploadedSize` and `totalSize`. The uploadedSize parameter specifies the size of uploaded parts, and the totalSize parameter specifies the total size of the short video that you upload.

    -   Upload success

        The `uploadSuccessWithResult:` callback is fired when the upload succeeds. The callback parameter includes `VodSVideoUploadResult`. The `VodSVideoUploadResult` parameter contains the following attributes:

        ```
        @property (nonatomic, copy) NSString* videoId;
        @property (nonatomic, copy) NSString* imageUrl;
        ```

        After a video is uploaded, the videoId parameter is returned, which indicates the video ID. Then, you must obtain the streaming URL to play the video. For more information, see [Obtain playback URLs to play videos](/intl.en-US/Developer Guide/Video play/Obtain playback URLs to play videos.md).

        After an image is uploaded, the imageUrl parameter is returned, which indicates the image URL. If URL signing is enabled, the image URL expires after a specific period of time. For more information, see [URL authentication](/intl.en-US/Developer Guide/Video security/URL authentication.md).

    -   Upload failure

        The `uploadFailedWithCode: message:` callback is fired when the upload fails. You can view the cause of the failure based on the `code` and `message` callback parameters. In addition, a prompt is displayed on the web page. For more information about error codes, see [t1235485.md\#](/intl.en-US/API Reference/Error codes.md) and [Handle exceptions](/intl.en-US/SDK Reference/iOS/Handle exceptions.md).

    -   Token expiration

        The `uploadTokenExpired` callback is fired when the STS token expires. You can send a request to the AppServer to obtain a new STS token and call the following method to resume the upload:

        ```
        - (void)refreshWithAccessKeyId:(NSString *)accessKeyId
                       accessKeySecret:(NSString *)accessKeySecret
                           accessToken:(NSString *)accessToken
                            expireTime:(NSString *)expireTime;
        ```

    -   Upload timeout

        When the upload times out, the `uploadRetry` callback is fired and the system automatically retries to upload files. You can receive a prompt on the web page or call the `cancel` method to cancel the upload. In addition, you can set the `maxRetryCount` parameter to specify the maximum number of retries. If the retry result indicates that the upload can be resumed, the `uploadRetryResume` callback is fired and the upload is resumed.


## Advanced settings

The `VODUploadSVideoClient` object supports the following advanced settings:

```
/**
 Specify whether to transcode a video after it is uploaded to ApsaraVideo VOD. Default value: YES.
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
 Specify the region of the ApsaraVideo VOD service. Default value: cn-shanghai.
 */
@property (nonatomic, copy) NSString *region;
```

